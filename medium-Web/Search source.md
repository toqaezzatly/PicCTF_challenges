## 🔍 Search Source

As the name suggests, *search the source* – either manually or as hinted by the challenge.

> **💡 How could you mirror the website on your local machine so you could use more powerful tools for searching?**
> → So yeah, **Download it**.

```bash
wget -mpEk http://saturn.picoctf.net:54735/
cd saturn.picoctf.net:54735
grep -ir 'picoCTF' .
```

![image](https://github.com/user-attachments/assets/06f7835c-f06f-491e-b167-2b918374f73d)

---

### 🎯 Flag Obtained

```
picoCTF{1nsp3ti0n_0f_w3bpag3s_ec95fa49}
```

---

### 🛡️ Vulnerability Assessment

This challenge highlights a common oversight in web application deployment: **exposing sensitive information within the source code**. The flag was embedded in the HTML/CSS/JS files served to the client — something a simple `grep` can uncover once the site is mirrored locally. It demonstrates:

* Lack of content sanitization or secure flag storage.
* Client-side exposure of sensitive information.
* How attackers or CTF players can exploit such exposures using basic tools.

---

### 📚 Lesson Learned

* Always **inspect source code** — especially in CTFs, the flag is often hiding in plain sight.
* Use tools like `wget`, `curl`, `grep`, or browser dev tools to dig deeper.
* From a security perspective, **never trust the client** with sensitive data.
* Developers should **avoid including secrets, flags, or credentials** in client-facing code. Even if it’s "hidden," it’s accessible.

---

Simple recon wins again. 🕵️‍♂️💻

