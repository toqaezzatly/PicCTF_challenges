# 💥 More SQLi – PicoCTF Walkthrough

This challenge felt way too similar to the [SQLiLite challenge](https://github.com/toqaezzatly/PicoCTF_challenges/blob/main/medium-Web/SQLiLite.md),
but let’s dive into the **differences** and see what made this one fun.

---

## 🧪 First Attempt: Classic Injection

I started with the classic:

```text
username: ' or 1 = 1 --
password: anything
```

### Output:

![Login fail](https://github.com/user-attachments/assets/d62f31ea-2696-4017-94c7-4ae13fba2c3e)

It **didn’t work** — looks like the app is **checking password before username**, or trying to avoid comment-out abuse.

---

## 🔄 Flipping the Script

So I thought — if you swap them, I’ll swap them too 😎

### Tried:

```text
username: anything
password: ' or 1 == 1 --
```

And... it worked!

> Since `1 == 1` is always true, it doesn't matter where you inject it.

### Success!

![Login success](https://github.com/user-attachments/assets/0056c439-4181-470d-bd14-eb1f75902252)

---

## 🔎 Post-login Recon

Tried injecting into the **search bar** — didn’t get me anywhere useful.

But I noticed this in the browser:

```
http://saturn.picoctf.net:54865/welcome.php
```

So I thought: this URI might hint at something more 👀

---

## 🗂️ Directory Discovery

Ran `dirsearch` to hunt for hidden files and directories:

```bash
dirsearch -u http://saturn.picoctf.net:54865/ -x 403,404
```

### Output:

![dirsearch results](https://github.com/user-attachments/assets/5ec7de5b-0838-4524-8ac1-ab593a8dfac5)

**users.db** immediately stood out 🔥

---

## 📦 Extracting the Database

Downloaded the file with `curl`:

```bash
curl -O http://saturn.picoctf.net:58986/users.db
```

Then viewed it:

```bash
cat users.db
```

### Output:

![cat db](https://github.com/user-attachments/assets/b20df008-2c21-4946-9846-6e24339bf815)

---

## 🏁 Flag

```
picoCTF{G3tting_5QL_1nJ3c7I0N_l1k3_y0u_sh0ulD_3b0fca37}
```

GG 💀

---

## 🧠 Lesson Learned

* SQL Injection isn’t just about dumping payloads — **know the flow** of the backend.
* If they change the logic, **change your attack**. Flipping fields worked like a charm here.
* Always inspect URLs and file structures after login. You might find a goldmine like a `.db` file sitting exposed.
* Never trust client inputs, and for the love of security, **don’t leave database files public-facing**.

---

## 🔍 Vulnerability Assessment

| Category          | Details                                                               |
| ----------------- | --------------------------------------------------------------------- |
| **Vulnerability** | SQL Injection + Sensitive File Exposure                               |
| **Root Cause**    | Unsanitized inputs in SQL queries & publicly accessible database file |
| **Impact**        | Full login bypass + direct credential dump                            |
| **Severity**      | 🔥 Critical                                                           |
| **Fix**           | Parameterized queries, input validation, block public file access     |

---

Another SQLi in the bag.
Moving on to the next one 🔐💻


