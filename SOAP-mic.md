**SOAP 🧼**

I thought the name of the challenge might be a hint for something, and I was right! SOAP is a protocol that uses XML format to transmit data. Even though the name was a strong hint, it’s okay if you didn’t get it at first. Let’s dig into the challenge. 🕵️‍♂️

This is the first thing you see when you click on the link:

![image](https://github.com/user-attachments/assets/3d63519b-099d-4f34-97a7-a1710a19342d)

Now, let’s inspect the sources in the dev tools:

![image](https://github.com/user-attachments/assets/88062dc9-1ac8-4970-af2b-3e6a0ec4a6dd)

At this point, we’re pretty sure we’re dealing with XML injection. 💻💥

So, what do we do? 🤔

![image](https://github.com/user-attachments/assets/c4549db0-40ff-4a92-b91d-f8639c557846)

As you saw in the previous challenge, there’s zero sanitization in the code. This code is responsible for converting the data passed to it into XML on the front end, preparing it to be sent to the backend. 🚀

Let’s now check what gets sent to the backend:

![image](https://github.com/user-attachments/assets/a2330b3c-7dd5-4e81-8e61-94c8d0fee242)

After intercepting the data and injecting something malicious:

![image](https://github.com/user-attachments/assets/71dd523e-129b-4cc7-b086-056058e2d1d1)

This is what we get:

**Flag:** `picoCTF{XML_3xtern@l_3nt1t1ty_55662c16}` 🎉

**Note:**

```xml
<!DOCTYPE data [
  <!ENTITY file SYSTEM "file:///etc/passwd">
]>
```

This code snippet means we’re requesting to show something from the same hosting server using the protocol `file://`. But it could be more complex, like executing something more advanced, such as requesting the server to fetch something via `http://` from the internet or `ftp://` from a remote server. 🌐🔍

---

### Lesson Learned 📚:

- Always **sanitize** input data to prevent attacks like **XML injection**! 🛡️
- **XML External Entity (XXE) attacks** can expose sensitive data, like files from the server, or even allow more complex exploits like remote file fetching. 🚨
- **Security best practice**: Never trust user input, especially when constructing XML or other data formats. Validate and sanitize everything before processing. ✅

