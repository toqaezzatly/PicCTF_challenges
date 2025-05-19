## 🧩 Some Assembly Required 1

Okay, so the only thing *"assembly"* here is the `.wasm` file listed in the **DevTools > Sources** panel.

You don’t even need to touch actual WebAssembly knowledge for this one. Just:

* Open DevTools
* Head to `Sources`
* Scroll down in the `.wasm` file

Eventually… boom 💥 — there’s your flag right in the text.

![image](https://github.com/user-attachments/assets/6b13fedf-2678-49a6-bdcd-0d02df9ca920)

---

### 🎯 Flag Obtained

```
picoCTF{d88090e679c48f3945fcaa6a7d6d70c5}
```

---

### 🛡️ Vulnerability Assessment

This challenge shows another example of **client-side exposure** of sensitive data. The WebAssembly (WASM) file is downloadable and readable — no obfuscation, no encryption, just... sitting there.

Key issues:

* Sensitive data (like flags) hardcoded into client-delivered files.
* No runtime protection or server validation.
* Assuming WASM = secure = nope ❌.

---

### 📚 Lesson Learned

* **WebAssembly is not secure by default**. It’s just like JavaScript — if it runs on the client, it can be reverse-engineered.
* Always inspect `.wasm` files in challenges or in real-world bug bounty hunting.
* Do **not** hardcode secrets in frontend files — regardless of tech stack.

---

Assembly? Not quite.
Snooping around the frontend? Always worth it. 🔍💻
