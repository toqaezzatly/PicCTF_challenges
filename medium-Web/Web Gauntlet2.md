

# 🧩 Web Gauntlet 2 — picoCTF

This challenge is **pretty cool**, because it's all about **one shot, one flag**. You don’t get multiple tries to fiddle around — you **have to know exactly what you’re doing**.

If I could summarize it in one line:

> 💬 *"If you can’t skip the password, then just bring all the passwords you have."*

---

## 🧨 What's the setup?

Same SQL injection vibes as Web Gauntlet 1 — but with **tighter filters** and a **harder goal**.

The app filters out:

> `or`, `and`, `union`, `like`, `=`, `>`, `<`, `--`, `/*`, `*/`, `admin`, etc.

But here’s the twist:

* We **can't skip** the password check...
* So instead, we **make the query pull all rows**, then let it **match against one that works**.

---

## 🎯 Goal: Login as admin — without ever typing "admin"

We can still use:

* `||` for string concatenation
* `GLOB` as an alternative to `=`
* Clever logic like `'a' is not 'b'` — which is **always true**

---

## ✅ Solution #1: Wildcard Match with `GLOB`

### Payload:

```sql
ad'||'min' GLOB '*'
```

### Why it works:

* `'ad'||'min'` builds `"admin"` dynamically
* `GLOB '*'` matches **any** non-empty string
* So the condition is **always true**, and returns the **admin** user

---

## ✅ Solution #2: Truthy password condition

### Username:

```sql
ad'||'min'
```

### Password:

```sql
a' is not 'b
```

### Why it works:

* The username becomes `admin` through string concatenation
* The password check becomes `'a' is not 'b'` — which is always **true**
* Boom 💥 — you’re in.

---

## 💥 Result:

Flag 🎉:

```
picoCTF{0n3_m0r3_t1m3_86f3e77f3c5a076866a0fdb3b29c52fd}
```

![flag screenshot](https://github.com/user-attachments/assets/9de724f3-8e19-4226-909c-3e706d67cb5a)

---


## 🧠 Lesson Learned

Even when classic SQLi payloads are blocked, you can still:

* Build any forbidden string using string concatenation or `char()`
* Use alternate operators (`GLOB`, `IS`, `IS NOT`, `IN`)
* Outsmart filters — think like the DB, not like the app

> 🧠 **Smart injection > brute force**
> 👣 One step ahead, always.

