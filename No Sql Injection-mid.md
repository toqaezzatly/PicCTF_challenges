
## 🛡️ No SQL Injection (picoCTF)

this challenge is pretty easy tbh, especially since u get access to the **source code** right away.

after taking a quick look at it:

```js
const user = await User.findOne({ 
  email: email.startsWith("{") && email.endsWith("}") ? JSON.parse(email) : email, 
  password: password.startsWith("{") && password.endsWith("}") ? JSON.parse(password) : password, 
});
```

🔎 it’s checking if the input starts and ends with `{}` and then parses it as **JSON** — no whitelist or blacklist for allowed characters, so we can abuse that.

---

## 💥 The Bypass

we can just pass:

```json
{ "$ne": null }
```

in **both** fields: email and password.

why? because:
- `$ne` is MongoDB syntax for **"not equal"**
- `null` is never equal to anything real in the DB
- so the query turns into something like:  
  `findOne({ email: { "$ne": null }, password: { "$ne": null } })`  
  which basically returns **any user** that is not null — likely the first one, aka **admin**.

---

## 🚨 The /admin Thing

one more thing I noticed after digging around:

if you just hit:  
👉 [`http://atlas.picoctf.net:50758/admin`](http://atlas.picoctf.net:50758/admin)  
you get logged in even without submitting credentials 😅

so either:
- this challenge is misconfigured
- or it's just built like that to demo the concept super easily

either way, the flag is exposed there too — not really about "noSQL injection" as much as just exploring bad auth setups.

---

## 📦 Where’s the Flag?

when you successfully log in (either via the injection or hitting `/admin`), check:

**Dev Tools → Application Tab → Session Storage**

you’ll see a response object stored like this:

```json
{
  success: true,
  email: "admin@admin.com",
  token: "cGljb0NURntqQmhEMnk3WG9OelB2XzFZeFM5RXc1cUwwdUk2cGFzcWxfaW5qZWN0aW9uXzI1YmE0ZGUxfQ",
  firstName: "admin",
  lastName: "admin"
}
```

decode the **token** (base64):

```
picoCTF{jBhD2y7XoNzPv_1YxS9Ew5qL0uI6pasql_injection_25ba4de1}
```

✅ and there's your flag.

---

## 📚 Lesson Learned

this challenge shows how dangerous it is to **trust user input without validation**, especially when parsing with `JSON.parse()` directly. Also, letting users hit `/admin` without auth? 😅 yeah — **big red flag**. So whether it’s NoSQLi or just bad route protection — both are real-world issues.

