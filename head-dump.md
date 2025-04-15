

# 🧠 head-dump - PicoCTF

As we have a beautiful UI, let's check it first.

I tried clicking around all the things, but nothing was useful except for `#API Documentation` in the pic:

![image](https://github.com/user-attachments/assets/b68123d5-9e52-49d1-88e1-7484359bbef4)

But it might not redirect you directly to that, so I used **dirsearch** — and it worked *really* well 🔥

![image](https://github.com/user-attachments/assets/8bb6d9e1-7426-460e-8494-67fa6100c33c)

As u see, there are 3 subdirectories that didn’t have links and weren’t visible on the home page at first:

- `http://verbal-sleep.picoctf.net:59148/api-docs/`
- `http://verbal-sleep.picoctf.net:59148/img/` → not important
- `http://verbal-sleep.picoctf.net:59148/headdump/`

So I followed the first link (✨ **note:** the port changes every time you launch the challenge):

You’ll see this:

![image](https://github.com/user-attachments/assets/e960354e-9485-4474-9322-b514c349b92f)

Turns out it also leads to the third link:

👉 `http://verbal-sleep.picoctf.net:59148/heapdump/`

A file will be downloaded — this file is called a **heapdump** 🧾

---

## 🧐 What is a Heap Dump?

A heap dump is basically a **snapshot of the memory (heap segment)** of a program at a specific moment in time. It captures:

- 📦 Objects and their types  
- 🧩 Fields and values  
- 🔗 References between objects  
- 🧵 Threads in some formats  
- 📊 Memory usage

---

### 🛡️ And for **security** → *WHICH IS OUR CASE*

Heap dumps can **leak sensitive information**, like:
- 🔐 Passwords  
- 🔑 Tokens  
- 🔑 API keys  
- 🧠 Full object state  

---

### 🎯 Why is it important?

It’s important for diagnosing:
- 🐏 Memory leaks  
- 🐌 Performance issues  
- 💥 OutOfMemory crashes  

---

### 🧵 Let's analyze it:

After downloading the file, run:

```bash
cat heapdump-1744731441371.heapsnapshot
```

You’ll see *a lot* of data — but don’t panic 😅

We usually search for keywords like:
```
password
email
username
```

But in **PicoCTF**, we’re looking for a **flag** — so:

```bash
grep -i picoctf heapdump-1744731441371.heapsnapshot
```

And boom 💥:

![image](https://github.com/user-attachments/assets/984dc140-64ff-468f-a4da-b5f01a0f62c3)

### 🏁 Flag →  
```
picoCTF{Pat!3nt_15_Th3_K3y_ad7ea5ae}
```

---

Hope that adds something cool to your methodology 🛠️💙  
