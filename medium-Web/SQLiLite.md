# 🛡️ SQLiLite - SQLite Injection Walkthrough

As the name suggests, this challenge is about **SQLite injection**. So let's go inject some SQL! 😈

---

## 🧪 Initial Attempt

Let's try the **very basic injection**.

### Input:

* **Username**: `admin`
* **Password**: (any value)

> ![Initial Try](https://github.com/user-attachments/assets/7d1d1417-b6d2-4aab-a291-002fbf191c03)

Nothing happens... meh. 😒

---

## 💥 Time to Break Things

Why not go for the classic?

### Input:

* **Username**: `' or 1 = 1 -- `
* **Password**: `X` (any junk)

> ![Injection Try](https://github.com/user-attachments/assets/2b9dbacf-9a80-4b6d-85f0-8731543a986d)

And... **BOOM!** 💥 It worked. We’re in.

---

## 🔍 Checking the Source Code

Always a good move to peek under the hood.

> ![Source Code](https://github.com/user-attachments/assets/906e3882-8e8c-48ab-9958-825fd642833b)

The code directly embeds user input into the SQL query — textbook example of SQL Injection vulnerability.

---

## 🏁 Flag

```
picoCTF{L00k5_l1k3_y0u_solv3d_it_ec8a64c7}
```

Mission accomplished. ✅

---

## 🧠 Lesson Learned

Never — *and I mean never* — trust user input directly in SQL queries. Use **parameterized queries** or **prepared statements**.

What worked here:

```sql
SELECT * FROM users WHERE username='' OR 1=1 -- ' AND password='X'
```

This bypasses the password check entirely because `1=1` is always true.

---

## 🔎 Vulnerability Assessment

| Aspect            | Description                                                             |
| ----------------- | ----------------------------------------------------------------------- |
| **Vulnerability** | SQL Injection (Authentication Bypass)                                   |
| **Cause**         | User input directly embedded in SQL query                               |
| **Impact**        | Full bypass of authentication – any user can log in without valid creds |
| **Severity**      | 🔴 Critical                                                             |
| **Mitigation**    | Use parameterized queries / prepared statements, and sanitize inputs    |

---

Simple injection, huge impact. Stay safe out there. 🕵️‍♂️💻

