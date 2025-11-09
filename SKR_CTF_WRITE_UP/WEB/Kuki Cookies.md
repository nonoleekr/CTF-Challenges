## Cookie Flag Write-up

**Hint:** What is URL encoding?  
**Task:** Get the cookie named `flag`, then decode it.

---

### Step 1: Find the Cookie
- Open **Developer Tools → Application → Cookies**.
- Look for a cookie with **Name:** `flag`.
- Value found:
```

SKR%7BI_L0v35_C00k13ssss%21_6d933b%7D

````

---

### Step 2: Decode the Value
URL encoding replaces special characters with `%` + hex code.  
Use any decoder (e.g. browser console, Python, or online tool):

```js
decodeURIComponent('SKR%7BI_L0v35_C00k13ssss%21_6d933b%7D')
````

**Decoded result:**

```
SKR{I_L0v35_C00k13ssss!_6d933b}
```
