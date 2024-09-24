
**24) JAVA CODING GUIDELINES:**


#### **I) Naming Conventions:**



* Classes & Interfaces: Use Pascal case (e.g., MyClass, UserDetails).
* Methods: Use camel case starting with lowercase (e.g., getName, calculateTotal).
* Variables: Must have meaningful names (e.g., userName, totalAmount), avoiding single-character names.
* Constants: Use uppercase letters with underscores (e.g., MAX_LIMIT, PI_VALUE).

Interview Tip: Emphasize clarity in naming for maintainability and readability.


#### **II) Curly Braces:**



* Inline Style: Place the opening brace on the same line as the declaration (e.g., class ClassName { ... }).
* New Line Style: Place the opening brace on a new line aligned with the closing brace.

Interview Tip: Discuss consistency in using one style across the codebase to enhance readability.


#### **III) Indentation:**



* 4 spaces per indentation level.
* Use spaces, not tabs.
* Place spaces around operators and after semicolons and commas (e.g., a = b + c).

Interview Tip: Highlight how proper indentation helps prevent errors and makes the code more readable.


#### **IV) White Space:**



* Use white spaces to enhance readability:
    * Operators: Surround them with spaces (e.g., a = b + c).
    * Keywords: Add space between keywords like if, for, and opening parentheses (e.g., if (condition)).
    * Commas, colons, and semicolons: Add space for clarity (e.g., fun(a, b, c)).

Interview Tip: Mention how well-formatted code avoids confusion and is easier to debug.


#### **V) Comment Line:**



* Implementation Comments:
    * Block Comments: Used for large descriptions of classes or methods.
    * Single-line Comments: Aligned with code for quick notes (//).
    * Trailing Comments: Kept short and spaced far from the code.
    * Temporary Code: Comment out code using //, but ensure it’s removed when no longer needed.
* Documentation Comments:
    * Use /**…*/ for Javadoc on public classes and methods.
    * Provide detailed explanations of parameters and return values.

Example Javadoc:

/**

 * Fetches employee details based on ID.

 * @param employeeId unique identifier of employee.

 * @return Employee object.

 */

public Employee getEmployeeById(int employeeId) { ... }
