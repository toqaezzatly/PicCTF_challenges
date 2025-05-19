## 🍪 Power Cookie

This challenge is *too easy* to be rated medium — but hey, just go with the flow.
It's all about **monitoring the browser's DevTools**.

> Head over to `DevTools > Application > Cookies`.

You’ll spot a cookie with a value of `0`.
Change it to `1`.

Boom. That’s it.

```text
picoCTF{gr4d3_A_c00k13_5d2505be}
```

![image](https://github.com/user-attachments/assets/e50a2e51-0dc4-4dae-97d4-cc7d7fbbfaa4)

---

### 🛡️ Vulnerability Assessment

This challenge illustrates a basic example of **client-side trust misuse**. The server is making an access decision based on a cookie stored on and modifiable by the client. Major red flags:

* No server-side validation.
* No signed or encrypted cookies.
* Direct reliance on user input for authorization.

In a real-world scenario, this could lead to **privilege escalation** or **unauthorized access**.

---

### 📚 Lesson Learned

* Never trust cookies from the client blindly.
* Always validate sensitive values on the server side.
* Use techniques like **signed cookies**, **JWTs**, or **sessions** with proper access controls.
* As a pentester or CTF player, **always check cookies**. They often carry clues or control mechanisms.

---

Sometimes, the weakest link is just a cookie away. 🍪😎
