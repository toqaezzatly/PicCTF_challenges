**WebSockFish 🐟♟️**

Okay, so I don't know how to play chess 🤷‍♂️, so I just kept moving randomly. While doing that, I was monitoring what’s happening on the WebSocket history 📜 in **BurpSuite** (something you should definitely keep an eye on, given the name of the challenge tab 😎). 

I noticed that after each move, I kept seeing `eval` with a positive or negative number 📈📉. So, I thought, why not mess around with huge random positive and negative numbers? 😆

After some trial and error (and a bit of intuition), I sent this **totally random huge value**: 

```
eval -1000000000000000
```

At this point, I wasn't sure, but I figured the **negative number** might be the key to cracking this, maybe because it aligns with some kind of processing in chess moves 🤔. 

And guess what? 🥳 After sending it, **boom**! The flag appeared like magic! 💥

Here’s the flag:

**picoCTF{c1i3nt_s1d3_w3b_s0ck3t5_1c70436a}** 🎉

---

**Lesson Learned 🧠**:
- **Don’t be afraid to experiment**! Even if you're not familiar with the game (like me with chess), you can always explore different angles, like inspecting the WebSocket traffic or looking at unusual behavior.  
- **Trust your instincts**! I guessed that the negative numbers were the right direction, and it paid off.  
- Sometimes, it's not about playing the game well — it's about understanding how the system reacts to different inputs! 💡

