# Best practices of working with data types

### Numbers in General

* Avoid “magic numbers” Magic numbers are literal numbers, such as 100 or 47524, that appear in the middle of a program without explanation.
* Use hard-coded 0s and 1s if you need to
* Anticipate divide-by-zero errors
* Make type conversions obvious
* Heed your compiler’s warnings

### Floating-Point Numbers

* Avoid additions and subtractions on numbers that have greatly different magnitudes  With a 32-bit floating-point variable, 1,000,000.00 + 0.1 probably produces an answer of 1,000,000.00 because 32 bits don’t give you enough significant digits to encompass the range between 1,000,000 and 0.1.
*  Avoid equality comparisons
*  Anticipate rounding errors

### Characters and Strings

* Avoid magic characters and strings
* Watch for off-by-one errors Because substrings can be indexed much as arrays are, watch for off-by-one errors that read or write past the end of a string.
* Decide on an internationalization/localization strategy early in the lifetime of a program
* If you know you only need to support a single alphabetic language, consider using an ISO 8859 character set
* If you need to support multiple languages, use Unicode

### Boolean Variables

* Use boolean variables to document your program Instead of merely testing a boolean expression, you can assign the expression to a variable that makes the implication of the test unmistakable.
* Use boolean variables to simplify complicated tests

### Enumerated Types

* Use enumerated types for readability
* Use enumerated types for reliability
* Use enumerated types for modifiability
* Use enumerated types as an alternative to boolean variables
* Check for invalid values

### Integers

* Check for integer division \(the integer division \(7/10\) equals 0\)
* Check for integer overflow
* Check for overflow in intermediate results

