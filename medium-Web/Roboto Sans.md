
## 🤖 Roboto Sans

As the name and the description of the challenge suggest, it is about `robots.txt`.
So naturally, I went to:

```
url/robots.txt
```

📄
![robots.txt](https://github.com/user-attachments/assets/f55aa570-0a05-476b-8831-1803cf9b9ca3)

There I found a few encoded strings:

```
ZmxhZzEudHh0;anMvbXlmaW  
anMvbXlmaWxlLnR4dA==  
svssshjweuiwl;oiho.bsvdaslejg
```

These are in base64 (except maybe the last one). 🕵️‍♂️

So I decoded them:

* 📝 `ZmxhZzEudHh0` → `flag1.txt`
* 📂 `anMvbXlmaW` → `js/myfi`
* 📂 `anMvbXlmaWxlLnR4dA==` → `js/myfile.txt`
* ❓ `svssshjweuiwl;oiho.bsvdaslejg` → Unknown (probably junk)

With that, I went to:

```
url/js/myfile.txt
```

And boom! 🎉

![flag](https://github.com/user-attachments/assets/6a0cb0c0-0fe2-42c8-bebc-6fa2efc83634)

## 🏁 Flag

```
picoCTF{Who_D03sN7_L1k5_90B0T5_718c9043}
```

