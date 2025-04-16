# Secure Customer Portal - PicoCTF

After I noticed that there are subdirectories that can be viewed from the URL:

![Subdirectories](https://github.com/user-attachments/assets/3c57929f-a025-44c1-af47-b3c3f85ccbd5)

Immediately, I used `dirsearch` to crawl the application further:

```bash
dirsearch -x http://saturn.picoctf.net:52158/ -x 404,403
```

![Dirsearch Results](https://github.com/user-attachments/assets/5bd6b9fb-5b01-4e22-90f5-02d49bcd5099)

After reviewing the discovered pages, the most valuable one was `secure.js`:
[http://saturn.picoctf.net:52158/secure.js](http://saturn.picoctf.net:52158/secure.js)

![Secure.js Inspection](https://github.com/user-attachments/assets/62ba795f-113c-4b81-b028-de488f964955)

Inside the script, I found the credentials:

```js
username === 'admin' && password === 'strongPassword098765'
```

Using these credentials, I was able to retrieve the flag:

```txt
picoCTF{j5_15_7r4n5p4r3n7_b0c2c9cb}
```
