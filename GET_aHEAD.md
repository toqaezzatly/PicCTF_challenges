# GET aHEAD - PicoCTF

## Lesson Learned
As the name suggests, we should **GET aHEAD**, aka **GET a header**, meaning we need to send a `HEAD` request instead of `POST`.

### How to Do It:
1. Click on **Use BurpSuite** or any other tool.
2. Check the request details.

![Image](https://github.com/user-attachments/assets/64529920-066a-4f2e-95e7-330787807fa4)

3. **Modify the request header**:
   - Change **`POST /index.php HTTP/1.1`** → **`HEAD /index.php HTTP/1.1`**.

![Image](https://github.com/user-attachments/assets/4d52e4d0-f221-4b2c-bcda-3597282ee812)

### The Flag:
```
picoCTF{r3j3ct_th3_du4l1ty_775f2530}
```

## Alternative Approach:
You can use **`curl`** to send a HEAD request:
```bash
curl -I <url>
```
This method will retrieve only the header, which contains the flag.

![image](https://github.com/user-attachments/assets/dab2ca6d-8bd9-488d-b395-3523b6de906e)
