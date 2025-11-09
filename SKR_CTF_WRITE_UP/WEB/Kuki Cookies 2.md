# Cookie Flag Write-up

**Context:** Click **Get Flag** → page says *only admin can get flag*.
There is a cookie `admin=false`. Change it to `true` and reload to get the flag.

---

### Steps

1. Open **Developer Tools → Application → Cookies**.
2. Select the site, find the cookie named `admin`.
3. Edit the cookie value from:

   ```
   false
   ```

   to:

   ```
   true
   ```
4. Reload the page and click **Get Flag**.

> Alternative (Console):

```javascript
// If cookie is not HttpOnly
document.cookie = "admin=true; path=/";
location.reload();
```

**Note:** If the cookie is `HttpOnly` you cannot modify it from the console — use the browser devtools or a proxy to modify the response, or exploit another vulnerability to set it.

---

✅ **Final Flag:** `SKR{4dm1n_C00kiess_2df94d}`
