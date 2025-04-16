# 🕵️ Scavenger Hunt - PicoCTF

## Challenge Overview
This CTF is very similar to **Insp3ct0r - PicoCTF** but requires deeper searching to uncover the flag. You will find the **first two parts** in **HTML & CSS**.

### 🔍 Step 1: Checking HTML & CSS
![HTML Part](https://github.com/user-attachments/assets/0d4a9f8b-368c-4171-bf06-a9e47aa25311)

![CSS Part](https://github.com/user-attachments/assets/4c83ca29-abaa-41ed-8b74-2471a9d3d32e)

---

### 📜 Step 2: Inspecting JavaScript
The **JS file** contains a comment hinting at further exploration:

![JS Comment](https://github.com/user-attachments/assets/52c8d446-f1fe-400c-9418-b9357cb80d0a)

---

### 🤖 Step 3: Checking `robots.txt`
A clue suggests checking `robots.txt` for additional information:

![robots.txt Hint](https://github.com/user-attachments/assets/2945a1c6-dd32-44be-be79-1ed3a75e3956)

But as you see, **we are not done yet**—where do we look next?

---

### 📂 Step 4: Using `dirsearch`
To find more hidden files, I used `dirsearch`, and here are the results:

![dirsearch Results](https://github.com/user-attachments/assets/49bb3b90-7d87-4d4b-b8c0-0fc99bffe85a)

---

### 🔄 Step 5: Curling the Hidden Files
Curling the discovered files gave us additional flag fragments:

![curl Results](https://github.com/user-attachments/assets/51da0c46-a789-4812-9385-e47f453cda05)

---

### 🔑 Step 6: Retrieving the Last Part
⚠️ **Note: File names are case-sensitive!**  
To find the last part, pay close attention to the exact casing of filenames:

![Final Part](https://github.com/user-attachments/assets/62829d88-caf2-4ffc-aa60-744059f58d2a)

---

### 🏁 **Final Flag**
```
picoCTF{th4ts_4_l0t_0f_pl4c3s_2_lO0k_f7ce8828}
```

🔹 **Challenge Complete!** This walkthrough highlights how **persistent searching** in different areas—HTML, CSS, JS, `robots.txt`, and hidden directories—can uncover the full flag. 🚀
