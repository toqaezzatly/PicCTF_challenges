## 🧠 Irish-Name-Repo 3 – Walkthrough

This challenge builds upon the ideas from **Irish-Name-Repo 1** and **2**, but with an extra layer of hardening.

We notice quickly that **only the password is accepted** — and something is happening to it before reaching the backend.

---

### 🔍 Observations:

* You input a password
* It gets **encrypted before being sent to the SQL query**
* The encryption? **ROT13**

---

### 🧪 Trial & Error:

After throwing some payloads at it, I noticed that:

```sql
' or 1=1 --
```

gets transformed into:

```sql
' be 1=1 --
```

Which is a ROT13 transformation.

So the trick here is:

> Submit the **ROT13 version of your injection payload**, so it gets decrypted server-side before being used in the SQL query.

---

### ✅ Final Payload:

```sql
' be 1=1 --
```

Which the server decrypts to:

```sql
' or 1=1 --
```

And boom 💥

![image](https://github.com/user-attachments/assets/831e8b57-b27d-47a1-bd38-9a53f293921c)


**Flag:**

```
picoCTF{3v3n_m0r3_SQL_4424e7af}
```

---

## 🔎 Vulnerability Assessment

* **Input Filtering**: While direct injection is blocked, the input is weakly protected by client-side ROT13, which is easily reversible.
* **SQL Injection Still Possible**: Encoding-based filters are ineffective if the backend decrypts without validation.
* **No Input Sanitization or Parameterization**: The server still embeds raw input into SQL, making it vulnerable.

---

## 💡 Lesson Learned

* **Obfuscation ≠ Security** – ROT13 is trivial to decode. It should never be used as a security measure.
* **Always Validate Inputs Server-Side** – Even if you encrypt, sanitize and validate *after* decryption.
* **Use Parameterized Queries** – Prevent SQL injection by using safe query structures.
