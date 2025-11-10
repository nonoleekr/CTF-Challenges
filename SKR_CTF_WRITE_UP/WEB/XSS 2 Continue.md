# My First XSS 2 Continued Write-Up

This challenge is a continuation of **My First XSS 2**.

Previously, you obtained the flag cookie by exploiting XSS and capturing cookies via a webhook. This time, the goal is to **log in as admin**.

### What You Have

Using the webhook technique (same as before), you will receive **two cookies**:

- **flag cookie**:  
  `flag=SKR{Ste4l1ng_4Dm1n_C0Ok135sss_330017}`  
- **session cookie**:  
  `session=xxx`

### What to Do

1. Use the session cookie from the webhook response.
2. Replace your current browser session cookie with this admin session cookie.
3. Reload the page.

After reloading, the **"Report to admin"** button will change to **"Secret"**.

### Final Step

Click the **"Secret"** button to reveal the final flag:

```
SKR{XSS_2_@Dm1N}
```
