## 🔓 JAuth Walkthrough

So to mess with the JWT, normally you’d need the **secret key** to regenerate the signature — that’s what keeps it secure. But after digging through the lab, there’s **no way to get the secret key**.

So the thought was: *why not just get rid of the signature part altogether?*

And yep — that works 😏

---

### 🛠️ Steps:

1. Head over to [**jwt.one**](https://jwt.one/)
2. Paste the **JWT token** you got from the site into the editor.
3. In the **header**, change:

   ```json
   "alg": "HS256"
   ```

   to:

   ```json
   "alg": "none"
   ```
4. Now in the **payload**, change your role:

   ```json
   "role": "user"
   ```

   to:

   ```json
   "role": "admin"
   ```
5. **Remove the signature part** completely — just leave the dot at the end like this:

   ```
   <header>.<payload>.
   ```

---

### 🍪 Then:

Go to your browser's **Dev Tools → Application → Cookies**, find the JWT token, and **replace it** with your edited one.

---

### 🎉 Boom — you're admin.

And here's the flag:

![flag](https://github.com/user-attachments/assets/31097b97-64b6-4350-9f9f-8ece7389b622)
