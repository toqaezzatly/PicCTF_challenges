# 🔑 Logon - PicoCTF

## Challenge Summary
Just login with any credentials—Joe’s or anyone else’s—then inspect the **DevTools** 🔍.

### Step 1: Login
![Login Attempt](https://github.com/user-attachments/assets/3d9e15ba-09fa-4b76-8630-42430e825632)

### Step 2: Inspect Cookies 🍪
Check the **Developer Tools**, and you’ll notice something interesting!

![Cookie Inspection](https://github.com/user-attachments/assets/d227d742-e49a-437a-a462-a08d40e3d07c)

### Step 3: Modify Cookie 🛠️
Change `admin=false` → `admin=True` in the **cookies** and refresh the page.

### Flag 🏁
```
picoCTF{th3_c0nsp1r4cy_l1v3s_0c98aacc}
```

---

## 🔍 Side Note: Why Did "True" Work?
You can try **different variations**:
- `admin=TRUE`
- `admin=True`
- `admin=true`
- `admin=1`

### 🧐 Explanation:
The reason **`admin=true`** failed while **`admin=True`** worked is due to **case sensitivity** and how the application processes boolean values.

### **Possible Reasons:**
1. **Strict String Comparison 📏**  
   - Some web applications store **cookie values as strings** instead of actual booleans.  
   - If the server expects `"True"` (capitalized), `"true"` (lowercase) **won’t match**, causing authentication failure.

2. **Hardcoded Validation 💾**  
   - The backend might validate like this:
     ```python
     if cookie_admin == "True":
         grant_access()
     ```
   - Instead of evaluating it as `True/False`, it only matches the exact **string** `"True"`.

3. **Improper Type Handling ⚠️**  
   - Some languages (like Python) distinguish between **`True` (boolean)** and **`"True"` (string)**, leading to unexpected behavior.

4. **Intentional Security Misconfiguration 🔐**  
   - In some **CTF challenges** or insecure applications, developers implement **case-sensitive checks**, unintentionally allowing simple bypass methods like **changing the case**.

Would you like more insights on web security techniques? 🚀
