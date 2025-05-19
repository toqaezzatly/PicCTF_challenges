
# Irish-Name-Repo 1 — PicoCTF Walkthrough

Let's break into this challenge 😈

![Login Page](https://github.com/user-attachments/assets/3c43a6cc-8b44-42b5-a2d2-2fa9df57d181)

---

## 🔐 Step 1: Login Attempt

Auh.. okay. Tried logging in as Admin with any random credentials. As expected — **it fails**. Nothing helpful in the description either.

At this point, maybe you’re thinking:

> *"Let’s mess with cookies?"*

Well… sorry to say, but **cookies have nothing to do with it**.  
So let's bring out the big guns — time to **intercept the traffic with BurpSuite** and see what’s under the hood.

---

## 🛠️ Step 2: Intercepting the Request

![Burp Intercept](https://github.com/user-attachments/assets/c621b2e2-2325-45e1-b848-0b9aa62670ee)

Boom 💣 — **Spotted something interesting**:

```

debug=0

````

This parameter is hidden from the form but still sent to the backend.  
AnyWay — whenever I see `0`, I always like to **flip it to `1`** just to see what happens 😏

---

## 👀 Step 3: Enabling Debug Mode

![Debug Enabled](https://github.com/user-attachments/assets/d7511b08-5949-4265-85cc-fa6b052a89bb)

As you can see — turning on debug mode **exposed the SQL query** being used on the backend.

Now we’re talking 💡  
We’re on the right track. Time to inject some SQL.

---

## 💉 Step 4: SQL Injection

I did the classic thing — basic boolean-based SQLi:

```sql
username=' or 1=1 --
password=admin77
debug=1
````

![Flag Obtained](https://github.com/user-attachments/assets/deaef9c1-2c53-4d53-b4de-68fad6d4b266)

And boom — we're in.

### 🎉 Flag: `picoCTF{s0m3_SQL_f8adf3fb}`

---

## 🧠 Lessons Learned

* Always **check hidden form fields** — don’t just rely on what's visible.
* **BurpSuite** is powerful, but sometimes you don’t even need it.
  In this case, checking the HTML using browser DevTools would’ve revealed the hidden `debug=0`.
* Debug flags or hidden params can **leak sensitive backend behavior**. Always experiment with those.

---

## 🔍 Vulnerability Assessment

* **Vulnerability Type**:

  * **SQL Injection** (Classic `OR 1=1 --`)
  * **Insecure Debug Mode Exposure**
* **Impact**:

  * Full authentication bypass
  * Backend logic and SQL queries exposed
* **Mitigations**:

  * Never expose debug parameters in production.
  * Use parameterized queries to prevent SQL injection.
  * Validate and sanitize user input properly.
  * Hide server-side logic from client requests.

---

## 📌 Final Thought

This could’ve been solved without BurpSuite. Just open up DevTools and inspect the login form.
I usually do that, but I like to avoid tools to some extent — so I was just reminding myself here.
CTFs are about thinking smart, not just throwing tools at a problem 😄


