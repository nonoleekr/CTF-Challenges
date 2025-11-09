# Password Validator

## Challenge Description
This challenge presents a simple C program that prompts the user to enter a password. The input is read as a string and then converted to an integer. The program validates the password by applying a mathematical check:

```
int pass = atoi(password);
if ((pass * 2) - 666 == 2008)
{
    printf("Welcome admin!\nFlag: SKR{%s}", password);
} 
else 
{
    printf("Login failed!");
}
```

If the condition holds true, it prints a welcome message with the password in the flag format `SKR{password}`.

## Analysis

- The program reads the input using `scanf("%s", password);` into a fixed-size buffer of 16 characters.
- The input string is converted to an integer using `atoi()`.
- The password is valid if the integer `pass` satisfies the equation:  
  \[
  (pass \times 2) - 666 = 2008
  \]
  
Solving for `pass`:
\[
pass \times 2 = 2674 \implies pass = 1337
\]

Thus, the input string `"1337"` makes the condition true.

## Vulnerabilities and Risks

- **Buffer Overflow Risk:** The use of `scanf("%s", password);` without length limit opens the program up to potential buffer overflow if the user inputs more than 15 characters (leaving room for the terminating null byte).
- **Input Validation:** Using `atoi()` blindly converts the input to an integer without validation, treating invalid inputs as 0, which might cause bypass or undefined behavior in more complex scenarios.
- Such coding practices are discouraged in secure programming.

## Flag

The flag for this challenge is:

```
SKR{1337}
```

Entering `1337` as the password triggers the welcome message and reveals this flag.

## Summary

This challenge tests basic understanding of input handling, simple math conditions, and integer conversion in C. The password was directly derived by solving the arithmetic condition given. Attention should be given to the buffer handling and input conversion for more robust and secure implementations.
