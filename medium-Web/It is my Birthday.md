# 🎉 It is my Birthday

The whole idea of this project is about finding **two PDF files with the same MD5 hash**.
I asked ChatGPT for help and it pointed me to this sweet repo:

🔗 [https://github.com/corkami/collisions](https://github.com/corkami/collisions)

I ended up using these two files:

* [MD5-1](https://github.com/corkami/collisions/blob/master/examples/free/md5-1.pdf)
* [MD5-2](https://github.com/corkami/collisions/blob/master/examples/free/md5-2.pdf)

I tried a bunch of other files, but they were **too large** or bloated. These two were simple and **got the job done**.
Downloaded them, uploaded them as needed, and boom — got the flag. 🏴

> ![image](https://github.com/user-attachments/assets/bd928e54-bc8b-48f4-814c-c824fd52c2bf)

## 🏁 Flag

```
FLAG: picoCTF{c0ngr4ts_u_r_1nv1t3d_aebcbf39}
```

---

## 🧠 Lesson Learned

Even though MD5 spits out a quick hash, it’s **not safe** anymore. You can literally have **two totally different files with the exact same hash**.
That means you can’t trust MD5 to confirm if a file is authentic or unaltered. Wild, right?

> TL;DR: **Don’t use MD5 in anything security-related.** Ever.

---

## 🔎 Vulnerability Assessment

* **Algorithm**: MD5
* **Issue**: Vulnerable to **collision attacks**
* **Impact**: Can be used to forge digital signatures or bypass integrity checks
* **Fix**: Use secure hash algorithms like **SHA-256** or **SHA-3**

