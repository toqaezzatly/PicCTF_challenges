### 🛠 Java Code Analysis!?!

As the name suggests, we're diving into analyzing Java code. But let's be real—who wants to spend **15 minutes** on this? 😂 Let's take some shortcuts and rely on **hints** (because, let’s be honest, we forget to check them).

#### 🔑 **Understanding the Vulnerability**
The hint pointed straight to **JWT (JSON Web Token)**—a critical authentication mechanism. The key influencing fields in JWT (as seen in `jwtService.java`) are:
- **Role** 🏆 → Easily guessed; just change it to `"admin"`
- **Email** 📧 → Another simple guess
- **User ID** 🔢 → Requires a deeper look

Searching through the files, we hit **Roles.java**:
![Roles](https://github.com/user-attachments/assets/da4caf99-d82f-4745-8d2f-dc46647c0a13)

🚨 The comment reveals a major flaw: **Higher values mean higher privileges**. By tweaking `userId -> 2`, we escalate privileges.

### ✍️ **Where to Change the Values**
Boom! Here’s where the magic happens:
![Editing Values](https://github.com/user-attachments/assets/cce1b144-b585-4b3c-9eb1-1dd0c2833742)

And now, let's check the **auth-token**:
![Auth Token](https://github.com/user-attachments/assets/27257d5d-db9f-4ec5-b25b-dbcd4daca77f)

✅ Edited values, but wait—how did we get the **secret key**? **Easy**, it's **hardcoded** in `secretGenerator.java`:
![Secret Key](https://github.com/user-attachments/assets/c059e791-942e-462a-916c-ef72d3083149)

🔥 **Final Step**: Edit the tokens, refresh, and grab the **flag** from the flag book! 🎉
![Flag](https://github.com/user-attachments/assets/833fd715-5e0f-4f5e-ac97-5f27aea6b5d9)

🚩 **Flag**: `picoCTF{w34k_jwt_n0t_g00d_ca4d9701}`

---

### 🛡 **Vulnerability Assessment**
1. **Hardcoded Secrets** 🔒 → **Big NO!** If an attacker finds it, they can forge tokens.
2. **Predictable Privilege System** 📈 → Assigning roles based on user ID values is risky.
3. **JWT Manipulation** 🏴 → No proper validation? Easy to escalate privileges!

### 💡 **Lessons Learned**
- **🔐 Store secrets securely** → Use environment variables, not hardcoded values.
- **🚫 Prevent predictable privilege escalation** → Implement role-based access controls.
- **✅ Validate JWTs properly** → Ensure proper signing and verification.

### 🔄 **Patch it!**
```java
private String generateRandomString(int len) {
    SecureRandom random = new SecureRandom();
    StringBuilder sb = new StringBuilder();
    String chars = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789";
    for (int i = 0; i < len; i++) {
        sb.append(chars.charAt(random.nextInt(chars.length())));
    }
    return sb.toString();
}
```
💡 **Stronger secret keys = Harder to crack!** 🚀

🔎 **Security first!** Next time, don't leave the door unlocked. **Happy hacking (ethically)!** 😆✨
