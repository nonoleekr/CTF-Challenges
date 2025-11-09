# Character-Shifted Password Checker in C

## Overview
This C program validates a user-entered password by comparing it against a character-shifted reference string. If the entered password satisfies the condition, it welcomes the user and reveals a flag; otherwise, it denies access.

## Code Explanation

### Function `checkPassword`

- **Input:** A C-style string `pass` representing the password input by the user.
- **Length Check:** The function checks if the password length is exactly 14 characters. If not, it returns 0 to indicate failure.
- **Password Validation Logic:**  
  - A reference string is defined as:  
    ```
    "BTDJJ`Qmvt`1o4"
    ```
  - For each character at index `i` in the input password, the function checks whether it matches the character at the same index in `correct_pass` shifted **one ASCII value down** (i.e., `pass[i] == correct_pass[i] - 1`).
  - If any character fails this check, the function returns 0.
- If all characters satisfy the condition, the function returns 1, indicating the password is valid.

### Function `main`

- Prompts the user to enter a password (up to 19 characters).
- Calls `checkPassword` to validate the input.
- If valid, prints:
  ```
  Welcome admin!
  Flag: SKR{<password>}
  ```
- Otherwise, prints:
  ```
  Login failed!
  ```

## Understanding the Password Validation

The program expects a password where each character is exactly one less than the corresponding character in the given string `"BTDJJ`Qmvt`1o4"`. This effectively means the valid password is the string you get by subtracting 1 from each character's ASCII code in `"BTDJJ`Qmvt`1o4"`.

### Deriving the Valid Password

| Index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 |
|-------|---|---|---|---|---|---|---|---|---|----|----|----|----|----|
| `correct_pass` Char | B | T | D | J | J | ` | Q | m | v | t | `  | 1  | o  | 4  |
| ASCII (decimal)      | 66| 84| 68| 74| 74| 96| 81|109|118|116| 96 | 49 |111 | 52 |
| Valid password char = ASCII - 1 | A | S | C | I | I | _ | P | l | u | s | _  | 0  | n  | 3  |

Thus, the valid password is:
```
ASCII shifted password: "ASCII_Plus_0n3"
```

## Output Behavior

- On entering the valid password `ASCII_Plus_0n3`, the program prints:
  ```
  Welcome admin!
  Flag: SKR{ASCII_Plus_0n3}
  ```
- Otherwise, it prints:
  ```
  Login failed!
  ```

## Summary

This password checker uses a simple character-shift comparison against a predefined string. It expects the user password to be the reference string with each character’s ASCII value decreased by one. This approach is a basic obfuscation method that ensures only the correctly shifted password passes validation.

---
*This write-up clarifies the working of the password validation program, the password format required, and the expected program output.*
```
This Markdown write-up covers the program's logic, how the password is derived using ASCII shifts, and the expected output behavior.
