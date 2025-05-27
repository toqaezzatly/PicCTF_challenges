
## 🧩 Client-side-again — CTF Challenge Write-up

To be honest, I did not exert much effort in this challenge.
I’m not lazy — I’m **smart** 😎.

As the hint suggests, it's all about **obfuscation**, and the challenge title says it all: "**Client-side-again**". So the flag must be in the client-side code.

---

### 🔍 Step 1: View the Source Code

I popped open the browser dev tools and took a look at the source.

![source code screenshot](https://github.com/user-attachments/assets/bcd83bce-0bff-4439-a996-3f0c0758388c)

Boom — there's the obfuscated JavaScript.

---

### 🧠 Step 2: Obfuscation? Let’s Not Overthink It

The code was using a classic obfuscation trick:

```js
var _0x5a46 = ['f49bf}', '_again_e', 'this', 'Password Verified', 'Incorrect password', 'getElementById', 'value', 'substring', 'picoCTF{', 'not_this'];
```

And this function rotates and maps index values:

```js
(function(_0x4bd822,_0x2bd6f7){...})(_0x5a46, 0x1b3);
var _0x4b5b = function(_0x2d8f05, _0x4b81bb){ ... };
```

So yeah — just some annoying variable names and array mapping to hide plain strings. Easy enough to decode or just swap in manually.

---

### 🧼 Step 3: Cleaned-Up Code (Thanks to ChatGPT)

No shame — I asked ChatGPT to help deobfuscate it (why waste time when I can get answers fast 💡).

Final readable version:

```js
function verify() {
  var checkpass = document.getElementById('pass').value;

  if (checkpass.substring(0, 8) === 'picoCTF{'
      && checkpass.substring(7, 9) === '{n'
      && checkpass.substring(8, 16) === 'not_this'
      && checkpass.substring(3, 6) === 'oCT'
      && checkpass.substring(24, 32) === 'f49bf}'
      && checkpass.substring(6, 11) === 'F{not'
      && checkpass.substring(16, 24) === '_again_e'
      && checkpass.substring(12, 16) === 'this') {
    
    alert('Password Verified');
  } else {
    alert('Incorrect password');
  }
}
```

---

### 🧩 Step 4: Substring Mapping

I just mapped out the substring conditions, filled them in like a puzzle, and reconstructed the flag:

```txt
picoCTF{not_this_again_ef49bf}
```

---

### 🎯 Final Flag

```
picoCTF{not_this_again_ef49bf}
```

---

### 📚 Lessons Learned

* **Client-side validation** is never secure. If the logic runs in the browser, users can see it — no matter how obfuscated it is.
* **Obfuscation ≠ Security**. It only slows people down slightly (or makes them reach for ChatGPT 😅).
* Reading code backwards (from logic to data) is often faster than trying to fully deobfuscate it.

---

### 🔐 Vulnerability Assessment

* **Type**: Insecure Client-Side Validation
* **Risk**: Anyone can bypass the validation logic and extract the secret (flag) without guessing.
* **Fix**: Never trust the client. Move validation logic to the backend or use hashing with server-side checks.

---

### 😎 Final Thoughts

Why brute-force or waste time decoding obfuscation manually when I can **analyze smart**, delegate to tools, and save energy for harder challenges?

I work smarter — not harder 💻⚡.

