# 🧮 Cryptography

**Cryptography** is the art and science of protecting information (**plaintext**) by transforming it into an unreadable format (**ciphertext**).  
Think of it as building a **secret language** that only the intended sender and receiver can understand.

---

## 🕵️ Cryptography in CTFs

In CTFs, we usually act as the **nosy people** trying to break **insecure encryption or encoding schemes** to reveal hidden messages.

- 🔓 **Easy challenges:**  
  You can often solve them manually or by using **basic cryptography tools** to decrypt or decode the ciphertext.

- 💻 **Harder challenges:**  
  These may require some **programming** or **mathematical** knowledge — but don’t worry, **Generative AI tools** (like ChatGPT or Gemini) can help!  
  For now, let’s focus on the **beginner-friendly ones**.

---

## 🧩 Key Cryptography Terms

| Term | Meaning | Example / Analogy |
|------|----------|-------------------|
| **Plaintext** | The original, unencrypted message you want to keep confidential. | ✉️ Like a love letter written in plain English. |
| **Ciphertext** | The scrambled, encrypted version of the plaintext. It looks like gibberish to anyone without the key. | 🔐 Like a coded message only secret agents can read. |
| **Key** | The secret ingredient used in encryption and decryption. | 🗝️ Like a password that unlocks the hidden message. |
| **Encryption** | The process of converting plaintext into ciphertext using an algorithm and key. | 🌀 Scrambling the love letter so teachers can’t read it in class. |
| **Decryption** | The process of reversing encryption — turning ciphertext back into readable plaintext using the correct key. | 💌 The receiver uses the secret code to reveal the romantic message. |

---

> 💡 **Tip:**  
> In CTFs, always check if a ciphertext looks like **Base64**, **Hex**, **ROT13**, or other common encoding/encryption methods before diving deeper.
