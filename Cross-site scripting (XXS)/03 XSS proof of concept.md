# 03. XSS proof of concept

### ✅ Using `alert()` for Proof of Concept (PoC)

You can confirm most kinds of XSS vulnerability by injecting a **payload that causes your own browser to execute some arbitrary JavaScript**.

It’s long been common practice to use the `alert()` function for this purpose because it is:

- 🟢 **Short**
- 🟢 **Harmless**
- 🟢 **Hard to miss** when it successfully executes

> 💡 In fact, you solve the majority of our XSS labs by invoking alert() in a simulated victim's browser.
> 

---

### ⚠️ Chrome's Security Change (v92+)

Unfortunately, there's a slight hitch if you use **Chrome**.

From **version 92 onward (July 20th, 2021)**, **cross-origin iframes are prevented from calling `alert()`**.

🔒 This change affects some advanced XSS attacks that rely on iframe contexts.

---

### 🔁 Recommended Alternative: `print()`

In this scenario, we recommend using the `print()` function as an alternative PoC payload.

📄 If you're interested in learning more about this change and why we like `print()`,

👉 [Check out blog post](https://portswigger.net/research/alert-is-dead-long-live-print) on the subject.

---

### 🧑‍💻 Important Note for Lab Users

As the **simulated victim in our labs uses Chrome**, we've amended the affected labs so that they can also be solved using `print()`.

We've **indicated this in the instructions wherever relevant**.