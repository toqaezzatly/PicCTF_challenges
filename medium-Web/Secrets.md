
# Secrets

This challenge is just about tracking the **Source tab** of Dev Tools.

---

### 🔍 Step-by-step

1. Start with the initial URL:
   **[http://saturn.picoctf.net:62989/secret/](http://saturn.picoctf.net:62989/secret/)**
   ![image](https://github.com/user-attachments/assets/512707a6-400c-4f9c-b50f-0ccf4919ff27)

2. You’ll be redirected here:
   **[http://saturn.picoctf.net:62989/secret/](http://saturn.picoctf.net:62989/secret/)**
   ![image](https://github.com/user-attachments/assets/b8a3fa26-1f56-4a7c-8e60-0b0503aeaeb4)

3. In the **Sources tab** of Dev Tools, you can see a clue pointing to:
   **[http://saturn.picoctf.net:62989/secret/hidden/](http://saturn.picoctf.net:62989/secret/hidden/)**
   ![image](https://github.com/user-attachments/assets/5acfb72e-0c1e-46f1-82c7-450b2f2f988d)

4. No login required. Just navigate directly to:
   **[http://saturn.picoctf.net:62989/secret/hidden/superhidden](http://saturn.picoctf.net:62989/secret/hidden/superhidden)**
   ![image](https://github.com/user-attachments/assets/07552931-1938-49c7-bdc4-ae5be424bee5)

5. Use the **Elements tab** in Dev Tools to inspect the page.
   ![image](https://github.com/user-attachments/assets/57787928-50a9-4c1b-a09d-746de3e48b4e)

---

### 🎯 Flag

`picoCTF{succ3ss_@h3n1c@10n_39849bcf}`

---

### 🔐 Vulnerability Assessment

* **Type**: Information Disclosure via Developer Tools
* **Vector**: Hardcoded URL path hints inside the JavaScript code or HTML elements that were not removed/obfuscated.
* **Impact**: Attackers can easily discover hidden endpoints or resources without authentication.
* **Ease of Exploitation**: **Very easy** – requires only browser Dev Tools.
* **Fix Recommendation**: Never expose sensitive paths in client-side code. Implement access control checks server-side and obfuscate or remove unnecessary comments/debug info in production.

---

### 📚 Lesson Learned

* Always check **Dev Tools** – especially the **Sources** and **Elements** tabs – for hidden clues or unprotected resources.
* Front-end security **does not equal** real security. If a secret path is exposed in JavaScript or HTML, it's **not secure**.
* Never trust security through obscurity. Always back it with **authentication and access controls**.
