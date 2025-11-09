# Complex Password Validation in C

## Overview
This C program implements a multi-condition password validator that verifies a 17-character password based on intricate ASCII and character checks. Upon successful validation, it displays a welcome message and a flag containing the password.

## Code Breakdown

### Password Length Check
- The password length must be exactly 17 characters. If not, validation fails.

### Specific Character Checks
- First character (`pass[0]`) must be `'R'`.
- The second character (`pass[1]`) must satisfy two conditions:
  - It differs from the first character by -31 in ASCII (`pass[1] - pass[0] == -31`).
  - It equals the fourth character (`pass[1] == pass[3]`).
- The fifth character (`pass[4]`) must be the lowercase version of the first character (`tolower(pass[0])`).
- The third and fifth characters must differ by 4 (`pass[2] - pass[4] == 4`).
- The sixth character (`pass[5]`) must be `'5'`.
- The sixth and seventh characters differ by 4 (`pass[5] - pass[6] == 4`).
- The eighth character (`pass[7]`) equals the first character plus 28 in ASCII (`pass[7] == pass[0] + 28`).
- The third and ninth characters differ by 47 (`pass[2] - pass[8] == 47`).
- The tenth character (`pass[9]`) must be `'_'`.
- The tenth and thirteenth characters are equal (`pass[9] == pass[12]`).
- From the fourteenth character onward (`pass+13`), the substring must be `"Fun!"`.
- From the eleventh character onward (`pass+10`), the substring must be `"1s"`.

### Validation Outcome
- If all conditions pass, the password is considered valid.
- Otherwise, validation fails.

## Deriving the Password

1. `pass[0] = 'R'` (given)
2. `pass[1] = pass[3]` and `pass[1] - pass[0] = -31`
   - `pass[1] = 'R' - 31 = 'R'(82) - 31 = 51` ASCII code 51 is `'3'`
   - So `pass[1] = '3'` and `pass[3] = '3'`
3. `pass[4] = tolower('R') = 'r'`
4. `pass[2] - pass[4] = 4` → `pass[2] = pass[4] + 4 = 'r' + 4`
   - ASCII `'r'` is 114, plus 4 is 118 → `'v'`  
   So `pass[2] = 'v'`
5. `pass[5] = '5'`
6. `pass[5] - pass[6] = 4` → `pass[6] = pass[5] - 4 = '5'(53) - 4 = 49` = `'1'`
7. `pass[7] = pass[0] + 28 = 'R'(82) + 28 = 110` → `'n'`
8. `pass[2] - pass[8] = 47` → `pass[8] = pass[2] - 47 = 'v'(118) - 47 = 71` → `'G'`
9. `pass[9] = '_'`
10. `pass[12] = pass[9] = '_'`
11. `pass[10..11] = "1s"`
12. `pass[13..16] = "Fun!"`

## Final Password

Index | Character
---|---
0 | R
1 | 3
2 | v
3 | 3
4 | r
5 | 5
6 | 1
7 | n
8 | G
9 | _
10 | 1
11 | s
12 | _
13 | F
14 | u
15 | n
16 | !

Password:  
```
R3v3r51nG_1s_Fun!
```

## Program Output

- On inputting:  
  ```
  R3v3r51nG_1s_Fun!
  ```
  
- The output will be:  
  ```
  Welcome admin!
  Flag: SKR{R3v3r51nG_1s_Fun!}
  ```

- On any other input, the output will be:  
  ```
  Login failed!
  ```

---

This comprehensive explanation covers all logical steps, ASCII calculations, and expected program behavior.
