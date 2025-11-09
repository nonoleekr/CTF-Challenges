# Secret URL
## Steps to solve

1. **Open the challenge port URL**  
   Visit the URL with the port number replacing `xxx`:  
   `https://skrctf.me/ports/xxx/`  
   You will see the message:  
   ```
   Welcome Guest!  
   Only Mr. Robots knows where's the flag...
   ```

2. **Access `robots.txt`**  
   Append `robots.txt` to the URL to check for hidden paths:  
   `https://skrctf.me/ports/xxx/robots.txt`  
   
   The file contains:  
   ```
   User-agent: *  
   Disallow: /xxx.html
   ```

3. **Open the disallowed HTML page**  
   Navigate to the disallowed page specified in `robots.txt`:  
   `https://skrctf.me/ports/xxx/xxx.html`

4. **Get the flag**  
   Upon loading, the page refreshes and shows:  
   ```
   Welcome Mr. Robots!  
   Flag: SKR{B33P_B00P_9ea32f}
   ```
   
