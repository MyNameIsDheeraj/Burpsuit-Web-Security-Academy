# 06. Impact of reflected XSS attacks

## 🛡️ Impact of Reflected XSS Attacks

If an attacker can control a script that is executed in the victim's browser, then they can typically fully **compromise that user**. Amongst other things, the attacker can:

- 🔧 Perform any action within the application that the user can perform.
- 👁️ View any information that the user is able to view.
- ✏️ Modify any information that the user is able to modify.
- 🔄 Initiate interactions with other application users, including malicious attacks, that will appear to originate from the initial victim user.

---

## 🎯 Delivery Mechanisms

There are various means by which an attacker might induce a victim user to make a request that they control, to deliver a **reflected XSS attack**. These include:

- 🌐 Placing links on a website controlled by the attacker.
- 📝 Injecting content into another website that allows user-generated content.
- ✉️ Sending a crafted link via email, tweet, or other messaging platforms.

> The attack could be targeted at a known user or broadcasted indiscriminately to all users of the application.
> 

---

## ⚖️ Severity Compared to Stored XSS

Due to the need for an **external delivery mechanism**, the impact of **reflected XSS** is generally **less severe** than that of **stored XSS**, where the attack payload is persistently stored and executed directly within the vulnerable application.