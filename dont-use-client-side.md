# Don't Use Client-Side - PicoCTF

## Lesson Learned
As the name suggests, the solution to this challenge lies **on the client side**. Inspect the webpage source code, and you'll find the JavaScript validation logic.

### Extracting the Flag
By analyzing the JavaScript logic, we can reconstruct the flag from different password segments.

### Code Inspection
![Image](https://github.com/user-attachments/assets/fbcde829-4eae-4f5d-9fbe-d314f44343ce)
### **Breakdown**
The script checks different parts of the password using the `substring()` function. Each condition verifies specific segments:

| Condition | Extracted String |
|-----------|-----------------|
| `substring(0, split) == 'pico'` | `pico` |
| `substring(split, split*2) == 'CTF{'` | `CTF{` |
| `substring(split*2, split*3) == 'no_c'` | `no_c` |
| `substring(split*3, split*4) == 'lien'` | `lien` |
| `substring(split*4, split*5) == 'ts_p'` | `ts_p` |
| `substring(split*5, split*6) == 'lz_7'` | `lz_7` |
| `substring(split*6, split*7) == '723c'` | `723c` |
| `substring(split*7, split*8) == 'e}'` | `e}` |

![Image](https://github.com/user-attachments/assets/89e6a561-972d-48cd-92d4-49184dcb22c7)

### **Breakdown**
The script checks different parts of the password using the `substring()` function. Each condition verifies specific segments:

| Condition | Extracted String |
|-----------|-----------------|
| `substring(0, split) == 'pico'` | `pico` |
| `substring(split, split*2) == 'CTF{'` | `CTF{` |
| `substring(split*2, split*3) == 'no_c'` | `no_c` |
| `substring(split*3, split*4) == 'lien'` | `lien` |
| `substring(split*4, split*5) == 'ts_p'` | `ts_p` |
| `substring(split*5, split*6) == 'lz_7'` | `lz_7` |
| `substring(split*6, split*7) == '723c'` | `723c` |
| `substring(split*7, split*8) == 'e}'` | `e}` |

### **Final Flag**
```
picoCTF{no_clients_plz_7723ce}
```
