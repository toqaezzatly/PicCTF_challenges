# 🧠 SQL Direct – PicoCTF

This one isn’t about injection — it’s purely a **PostgreSQL basics** challenge.

> The goal: Learn how to use `psql`, no tricks, no payloads — just good old SQL.

---

## 🛠️ Accessing the Server

We’re given direct access to the PostgreSQL server:

```bash
psql -h saturn.picoctf.net -p 56784 -U postgres pico
```

**Password:**

```text
postgres
```

---

## 🧭 What To Do

Once inside, it's all about **exploring**:

1. `\l` – list all databases
2. `\c pico` – connect to the `pico` database (already connected in this case)
3. `\dt` – list tables
4. `SELECT * FROM flags;` – grab the flag
   ![image](https://github.com/user-attachments/assets/c7001620-aead-42aa-9535-64769ebddf01)


> This challenge is **meant to teach**, not trick you.

---

## 🏁 Flag

```
picoCTF{L3arN_S0m3_5qL_t0d4Y_73b0678f}
```

---

## 🎓 Lesson Learned

* PostgreSQL basics are essential, especially in real-life assessments.
* `psql` commands are powerful tools for direct database interaction.
* Not all SQL challenges are about injections — some are about **control** and **exploration**.

