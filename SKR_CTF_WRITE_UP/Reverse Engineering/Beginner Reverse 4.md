# Custom Password Checker in C

## Overview
This program implements a custom password validation function in C that checks if the entered password meets specific length and character sequence criteria. If the password is correct, it outputs a welcome message along with a flag containing the password; otherwise, it denies access.

## Code Explanation

### Function `checkPassword`

- **Input:** A string `pass` representing the user-entered password.
- **Length Check:** The function first verifies that the password length is exactly 15 characters using `strlen`. If not, it returns 0, indicating failure.
- **Character Checks:**  
  - It defines a reference string `part1` with the value `"Spr3ue45"`.  
  - It then compares every character at even indices (0, 2, 4, ...) of the password with the corresponding characters in `part1`.  
  - Next, a second reference string `part2` is defined as `"5PrcS3u"`.  
  - The function compares characters at even indices counted backward from the second last character of the password (indices 13, 11, 9, ...) against `part2`.  
- If any character comparison fails, the function returns 0. If all checks pass, it returns 1 indicating the password is valid.

### Function `main`

- Prompts the user for a password input (up to 19 characters).
- Calls `checkPassword` to validate the input.
- If valid, prints the message:  
  ```
  Welcome admin!
  Flag: SKR{<password>}
  ```
- Otherwise, prints:  
  ```
  Login failed!
  ```

## Password Validation Logic

- The password must be exactly 15 characters long.
- Characters at the even indices (0, 2, 4, ..., 14) must match the string `"Spr3ue45"`.
- Characters at the even indices starting from index 13 down to 1 (stepping backwards by 2) must match `"5PrcS3u"` in that order.
- This means the password is interleaved between these two strings.

## Example of a Valid Password

| Index  | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 |
|--------|---|---|---|---|---|---|---|---|---|---|----|----|----|----|----|
| Char   | S | u | p | 3 | r | S | 3 | c | u | r | e  | P  | 4  | 5  | 5  |

- Even indices (0, 2, 4, ...) spell `"Spr3ue45"`.
- Even indices backward (13, 11, 9, ...) spell `"5PrcS3u"`.
- The rest of the characters fill the odd indices.

## Output

- If the password entered by the user matches the criteria above, the program outputs:  
  ```
  Welcome admin!
  Flag: SKR{<password>}
  ```
- If not, it outputs:  
  ```
  Login failed!
  ```

## Summary

This program uses a somewhat unconventional password check by verifying two interleaved character sequences at even indices forwards and backwards. The dual check enforces a strong pattern requirement for the password, making it difficult to guess without knowledge of the sequence rules.

---

*This write-up helps understand the password check logic, expected input format, and program output behavior for the given C code snippet.*
