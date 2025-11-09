# Password Validation with Substring Checks

## Challenge Description
This challenge involves analyzing a C program that validates a password string before granting access. The program reads a password input (up to 19 characters) and uses a `checkPassword` function to test specific conditions on the string. The program prints a flag if the password passes all checks.

## Analysis

The `checkPassword` function validates the password according to these rules:

- The password length must be exactly 14 characters.
- Characters at position 0-1 must be `"S3"`.
- Characters at position 2-5 must be `"cur3"`.
- Characters at position 6-9 must be `"Pa$$"`.
- Characters at position 10-13 must be `"w0rd"`.

The validation is done using `strlen()` for length and `strncmp()` at fixed offsets for substring matching.

From these conditions, the password is constructed as:

```
S3cur3Pa$$w0rd
```

## Solution

When the user inputs the above string, the program passes all validation checks and prints the flag in the format:

```
SKR{S3cur3Pa$$w0rd}
```

## Technical Notes

- The program carefully limits input size in `scanf` with `%19s` to avoid buffer overflow in the 20-character buffer.
- The validation logic uses straightforward substring matches at known positions.
- This method illustrates a simple but effective approach to rigid password validation based on fixed substrings.

## Flag

```
SKR{S3cur3Pa$$w0rd}
```

## Summary

This challenge tests the ability to reverse-engineer string validation logic by analyzing length and substring constraints in C code. The solution is the concatenation of all required substrings in order and of the exact length. Printing the flag reveals successful exploitation of the validation mechanism.
