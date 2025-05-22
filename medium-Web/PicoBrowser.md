

# 🕵️‍♂️ PicoBrowser

This challenge is pretty easy ngl 😅
Actually, it's even simpler than I expected.

---

## 🧠 What’s the idea?

Basically, you just need to intercept the request going to `/flag`
And all you gotta do is **edit the User-Agent header** to:

```
PicoBrowser
```

Yep, that's it.

---

## 🛑 Important Note

Don't get tricked by the **307 redirect**.
It **looks** like you're going somewhere… but it's actually leading you away from the flag.

You want the response that gives you:

```
Status Code: 200 OK
```

> That’s the one carrying the treasure 🏴‍☠️

---

## 📸 Screenshots

### SEE !
![image](https://github.com/user-attachments/assets/8ba379fc-483f-481f-b390-81d579ac1124)

---

### Intercepting Response - 200 OK (That's the one 😎)

![image](https://github.com/user-attachments/assets/33422afe-e12a-4216-a6cc-b1b3e9f0721e)

---

## 🏁 Flag

```
picoCTF{p1c0_s3cr3t_ag3nt_e9b160d0}
```

---

## 📚 Lesson Learned

Sometimes, challenges aren’t about complex logic — just paying attention to **headers** and **response codes** can be enough.
User-Agent can be a sneaky way to gate content or behavior, so don't ignore it in CTFs.

---

## 🔒 Vulnerability Assessment

This is a classic example of **security through obscurity** — relying on the `User-Agent` string to hide or gate access to something sensitive (like a flag).
In real-world applications, this isn’t secure at all:

* **User-Agent headers are easily spoofed** by attackers or even regular users with tools like Burp, Postman, or browser extensions.
* No sensitive info or decision-making should rely on it alone.

**Takeaway**: Never trust the client blindly. Headers can lie.


