# Outline
## Pseudocode/Notes

1. **Parse Command-Line Arguments**

   - [x] Ensure the program is executed with exactly two arguments.
   - Arguments:
     - [x] Length of password (`arg[1]`)
     - [x] Complexity level (`arg[2]`)

2. **Validation**

   - [x] Check if the number of arguments is greater than 2.
     - [x] If not, output an error message and terminate.
   - Validate password length:
     - [x] Must be between 8 and 32.
     - [x] If invalid, output an error message and terminate.
   - Validate complexity level:
     - [x] Must be between 1 and 3.
     - [x] If invalid, output an error message and terminate.

3. **Password Complexity Rules**

   - Complexity 1:
     - Includes lowercase letters.
   - Complexity 2:
     - Includes lowercase and uppercase letters.
   - Complexity 3:
     - Includes lowercase, uppercase, digits, and special characters.

4. **Generate Password**

   - Based on the validated length and complexity level:
     - Generate a random password string following the specified rules.

5. **Output Password**

   - Print the generated password to the console.

