# findme – PicoCTF Writeup

I liked this challenge a lot — simple as water, sharp as a bullet. So let's get straight to the point. 🔍

---

### 🧩 Initial Recon

After logging in using the given credentials, I was greeted with… basically nothing. Just a boring search bar.

But, if you paid attention to the hint, it mentioned **redirection**. That was the key.

---

### 🛠️ Using Dev Tools Like a Pro

I cracked open the **Network tab** in DevTools (a must-use move in CTFs like this), and started monitoring the requests.

Boom. I caught this redirection pattern in action:

![network-tab](https://github.com/user-attachments/assets/e52960cb-5ad7-423a-812b-5bd4eaff95ef)

This right here was our lead. Two base64-encoded IDs in the request URL. Suspicious enough to decode them.

---

### 🔓 The Decode & The Flag

I took those two values and ran them through a base64 decoder. Nothing fancy — just some payload IDs pointing to internal resources.

And just like that, I got the flag:

```
picoCTF{proxies_all_the_way_25bbae9a}
```

---

### 🧠 Lesson Learned

* **Don't ignore DevTools** — Network tab tells a story that the UI hides.
* **Base64 ≠ encryption** — If it's encoded, try decoding. It's often just obfuscation.
* **Pay attention to redirections** — URLs don’t lie. They often reveal the inner mechanics of the web app.

---

### 🔍 Vulnerability Assessment

* **Unvalidated Redirects** – The challenge relies on redirection logic that’s visible and manipulable via URLs.
* **Information Disclosure via Base64** – Sensitive data or internal paths should never be exposed through base64 alone. That’s just security through obscurity.
* **Improper Access Control** – The flag was accessible without further authentication once the correct resource was identified and decoded.

---

Clean and neat challenge. Learned something. Logged the flag. On to the next. 🚀
