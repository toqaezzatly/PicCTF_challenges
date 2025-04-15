# IntroToBurp - PicoCTF 🔍

## Step 1: Register with Dummy Data
Start by registering with any **dummy credentials**.

![Registration](https://github.com/user-attachments/assets/811932ae-10e1-4eef-8a16-bf46e0925310)

---

## Step 2: Enter the OTP (Wait... What OTP?! 🤔)
You didn’t receive an OTP? **Exactly!** So go ahead and enter a **dummy OTP** instead.

![Dummy OTP Entry](https://github.com/user-attachments/assets/dc49cf5c-dd37-4119-8821-a785125ee616)

---

## Step 3: The OTP Validation Issue
No matter what you enter, it’s marked as **Invalid**. So, what if we **cancel** the OTP requirement?

### How to Cancel the OTP?
- Open **Burp Suite**.
- Locate the **request and response** data.

![Request & Response](https://github.com/user-attachments/assets/b73db866-d948-4c44-8394-e7ae3fa374c2)

- Send the request to the **Repeater**.
- **Remove the entire OTP validation line**.
- Click **Send**.

**Et Voila!** 🎉

---

## Flag Found! 🏆
```
picoCTF{#0TP_Bypvss_SuCc3$S_2e80f1fd}
```

![Flag](https://github.com/user-attachments/assets/1e2f6131-7ea3-4809-a0c5-020414769194)

**Challenge solved successfully!** 🚀


