# 🛡️ picoCTF: Web Gauntlet Walkthrough

This challenge was all about doing the **same thing in different ways** — classic SQL injection dodging with some twists.
Let’s walk through what went down round-by-round.

---

## 🔗 Two Links: Inject + Filter Monitor

We had two URLs:

1. The **form** to inject SQL payloads.
2. A **filter page** (`filter.php`) that shows which SQL keywords/operators were currently **blocked**.

So we kept an eye on `filter.php` every round to adapt our attack.

---

## 🌀 Round 1: Easy Mode

Filter just said `or` is not allowed.

### 🔹 Payload:

```
admin' -- 
```

✅ **Worked perfectly.**
Bypassed login since `--` commented out the password check.

---

## 🔁 Round 2: Restrictions Tighten

The filter blocked:

```
or and like = --
```

So none of these are usable anymore.

Tried `#` to comment — didn’t work.

### 🔹 Payload:

```
admin' /*
```

✅ Worked.
`/*` started a block comment and got rid of the password clause.

---

## 🔁 Round 3: Keep it Rolling

Didn’t see `/*` in the banned list this time either.

### 🔹 Tried again:

```
admin' /*
```

✅ Boom. Same trick, same success.

---

## 🔐 Round 4: Admin is Banned!?

Now it gets tricky — you can’t use **`admin`** as a word.

Trying to be a normal user? Nope — you **must** be `admin`.

So... how do we input `admin` **without actually typing it directly**?

### 🔹 Trick: SQL String Concatenation

Used:

```
adm'||'in'/*
```

✅ This builds `admin` dynamically with SQL string concatenation.
We used `||` to join `'adm'` and `'in'`.

---

## ✅ Final Payload (and Win):

```
adm'||'in'/*
```

Logged in successfully.
🎉 Got the flag:

```
picoCTF{y0u_m4d3_1t_16f769e719ab9d3e310fd13dc1262ee1}
```

---

## 🧠 Lesson Learned

* SQL injection **isn't always about the classic `OR 1=1`**. Sometimes it's about being creative with what **is** allowed.
* When key functions (`=`, `LIKE`, `--`, `admin`) are blocked:

  * Use **comment blocks** (`/* */`) to kill the query safely.
  * Use **concatenation** (`'||'`) to bypass word filters.
  * Watch for **filter logic leaks** via filter.php or error messages.

---

## 🔍 Vulnerability Assessment

| Type                    | Details                                                                 |
| ----------------------- | ----------------------------------------------------------------------- |
| SQL Injection           | Input not sanitized; direct string injection into SQL query.            |
| Weak Filtering          | Relying on blacklists (`or`, `=`, `--`) is bypassable and fragile.      |
| String Filtering Bypass | Word like `admin` blocked literally, but allowed via SQL concatenation. |
| No Prepared Statements  | Core issue — backend is not using parameterized queries.                |

---

### 💡 Real Defense Tips:

* Use **prepared statements** / **parameterized queries**.
* Don’t rely on keyword blacklisting — it’s easy to defeat.
* Validate input types (e.g., enforce that `username` is alphanumeric, no quotes).
* Sanitize both input **and output** to avoid further injection or reflection.



