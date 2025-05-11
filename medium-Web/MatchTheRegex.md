
## MatchTheRegex

This challenge's simplicity really depends on whether you've ever messed with regex before — if you have, you don’t need anything else to solve it.
At first, I thought it would be a bit tricky and maybe deserve a “medium” tag, but nah, turns out it’s pretty straightforward.

Anyway, just inspect the source code → look inside the `<script>` tag, and here’s what I found:

```javascript
function send_request() {
	let val = document.getElementById("name").value;
	// ^p.....F!?
	fetch(`/flag?input=${val}`)
		.then(res => res.text())
		.then(res => {
			const res_json = JSON.parse(res);
			alert(res_json.flag)
			return false;
		})
	return false;
}
```

Now take a look at this line:

```js
// ^p.....F!?
```

What does that remind you of?
Exactly — **picCTF** 👀

So I typed `picCTF` in the input field, and boom — here's your flag:

![image](https://github.com/user-attachments/assets/c64fb57b-243e-4845-a13a-db15ec643bc3)

```
picoCTF{succ3ssfully_matchtheregex_8ad436ed}
```

---

### 🧠 Lesson Learned

* Sometimes the answer is **literally in the comment**.
* The regex `^p.....F!?` matches `picCTF` perfectly — don’t overcomplicate it.
* Always check **script tags** and **inline comments** when you're stuck on a web challenge.
* Keep it simple — trust your first instinct when something looks too obvious.

