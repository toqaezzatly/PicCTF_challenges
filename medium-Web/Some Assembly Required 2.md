## 🧩 Some Assembly Required 2

okay, so this is slightly more involved than part 1. You’ll see a `.wasm` file in the page source — pop that open in DevTools > Sources, or just download and convert it using:

```bash
wasm2wat chall.wasm -o chall.wat
```

### 👀 What’s in there?

Inside the `.wat` (WebAssembly Text) file, we find:

```wasm
(data (i32.const 1024) "xakgK\\5cNs9=8:9l1?im8i<89?00>88k09=nj9kimnu\00\00")
```

That’s a flag-looking string, but it's encoded. Then we see this:

```wasm
(global $input (export "input") i32 (i32.const 1072))
...
(func $check_flag
  ...
  call $strcmp
)
```

So the flag is stored at memory address `1024`, and it’s compared to user input at `1072` using a custom `strcmp`.

### 🔎 Analysis

In `copy_char`, we see:

```wasm
i32.xor with 8
```

That’s our key. The flag was XOR’d byte-by-byte with `8`. So we just reverse it.

### 🔓 Decryption

We take the encoded string:

```
xakgK\5cNs9=8:9l1?im8i<89?00>88k09=nj9kimnu
```

XOR each byte with `8`, and we get:

```
picoCTF{15021d97ae0a401788600c815fb1caef}
```

### 🎯 Final Flag

```
picoCTF{15021d97ae0a401788600c815fb1caef}
```

---

### 🛡 Vulnerability Assessment

* **Sensitive data hardcoded** in WASM memory.
* **XOR obfuscation is weak** and reversible.
* **WebAssembly is not secure by design** — anything in memory can be dumped or decompiled.

---

### 💡 Lesson Learned

* If you see a `.wasm` file and a hidden string at a memory offset, think: decode and compare.
* `wasm2wat` is a game-changer for reversing.
* XOR obfuscation ≠ encryption — if it’s reversible, it’s readable.
