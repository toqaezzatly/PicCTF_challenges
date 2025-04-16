# Where Are The Robots - PicoCTF

## Lesson Learned
The **robots.txt** file (`/robots.txt`) is a common entry point for web security challenges. It tells search engines which pages **should not** be crawled, but sometimes developers accidentally list **sensitive directories**, making them easy to find.

### Challenge Investigation
#### Step 1: Check `robots.txt`
URL: [robots.txt file](https://jupiter.challenges.picoctf.org/problem/60915/robots.txt)

![Image](https://github.com/user-attachments/assets/f0f9fe22-8d81-4467-a345-e01a9c17911b)

#### Step 2: Follow the Hidden Path
URL: [Hidden Page](https://jupiter.challenges.picoctf.org/problem/60915/8028f.html)

![Image](https://github.com/user-attachments/assets/76a881d0-b10c-45bb-a539-1928bd2a29f3)

### **Final Flag**
```
picoCTF{ca1cu1at1ng_Mach1n3s_8028f}
```
