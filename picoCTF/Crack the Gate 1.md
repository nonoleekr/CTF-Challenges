# picoCTF Challenge Writeup: Secret Header Bypass

## Challenge Overview

In this challenge, you are tasked with accessing a restricted web portal where a user with the email `ctf-player@picoctf.org` is suspected of hiding sensitive data. The challenge provides two important hints:

### Hint 1
Developers sometimes leave notes in the code; but not always in plain text.

### Hint 2
A common trick is to rotate each letter by 13 positions in the alphabet (ROT13 cipher).

## Approach

### Step 1: Investigate Page Source for Clues

Visiting the challenge web portal and viewing the page source reveals a hidden comment:

```
<!-- ABGR: Wnpx - grzcbenel olcnff: hfr urnqre "K-Qri-Npprff: lrf" -->
```

This looks like gibberish but hints at being encoded.

### Step 2: Decode ROT13 Cipher

Applying ROT13 decoding (shifting letters 13 places) to the comment reveals the message:

```
NOTE: Jack - temporary bypass: use header "X-Dev-Access: yes"
```

This suggests that the developer left a secret bypass by checking for a custom HTTP header.

### Step 3: Add Custom Header in Request

To exploit this bypass, you need to send the HTTP request with the header:

```
X-Dev-Access: yes
```

### Step 4: Using ModHeader to Inject the Header

I used the ModHeader browser extension to add this header to requests:

1. Click the ModHeader icon in the browser toolbar.
2. Click the "+" button to add a new request header.
3. Enter the name: `X-Dev-Access`
4. Enter the value: `yes`
5. Ensure the header is enabled (toggle should be green).
6. (Optional) Add a URL filter to restrict the header to the challenge site domain (e.g., `amiable-citadel.picoctf.net`).
7. Refresh the login page so that the modified header is sent with each request.

### Step 5: Logging In

With the header injected, I logged in using the provided email:

```
ctf-player@picoctf.org
```

and a dummy password such as `123`. The server accepted the request because of the special header, granting access or revealing further data.

## Summary

The key to solving this challenge was understanding that:

- The hidden comment was ROT13 encoded.
- The decoded message provided the bypass method using a secret request header.
- Using a tool like ModHeader, you can inject this header into browser requests to exploit the backdoor left by the developer.

This challenge highlights the importance of carefully inspecting page source and knowing common encoding tricks like ROT13 that developers sometimes use to hide hints or credentials.

---

*Happy hacking!*
