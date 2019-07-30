# Regular Expressions

**Regular expressions** are extremely useful in extracting information from text such as code, log files, spreadsheets, or even documents. The first thing to recognize when using regular expressions is that **everything is essentially a character**, and we are writing patterns to match a specific sequence of characters \(also known as a string\).

Generally, the key part to process the text with regular expressions is regular expression engine and it is represented by **`Regex`** class in c\#. The `Regex` class is available with **System.Text.RegularExpressions** namespace.

|  |  |
| :--- | :--- |
| abc… | Letters |
| 123… | Digits |
| \d | Any Digit |
| \D | Any Non-digit character |
| . | Any Character |
| \. | Period |
| \[abc\] | Only a, b, or c |
| \[^abc\] | Not a, b, nor c |
| \[a-z\] | Characters a to z |
| \[0-9\] | Numbers 0 to 9 |
| \w | Any Alphanumeric character |
| \W | Any Non-alphanumeric character |
| {m} | m Repetitions |
| {m,n} | m to n Repetitions |
| \* | Zero or more repetitions |
| + | One or more repetitions |
| ? | Optional character |
| \s | Any Whitespace |
| \S | Any Non-whitespace character |
| ^…$ | Starts and ends |
| \(…\) | Capture Group |
| \(a\(bc\)\) | Capture Sub-group |
| \(.\*\) | Capture all |
| \(abc\|def\) | Matches abc or def |

#### Example

Following is the example of validating whether the given text is in proper email format or not using `Regex` class in C\#.

```csharp
using System;
using System.Text.RegularExpressions;

namespace TutlaneExamples
{
    class Program
    {
        static void Main(string[] args)
        {
            string email = "support@tutlane.com";
            var result = Regex.IsMatch(email, @"^[\w-\.]+@([\w-]+\.)+[\w-]{2,4}$");
            
            Console.Write("Is valid: {0} ", result);
            Console.ReadLine();
        }
    }
}
```

#### C\# Regex Class Methods

| Method | Description |
| :--- | :--- |
| IsMatch | It will determine whether the given input string matching with regular expression pattern or not. |
| Matches | It will return one or more occurrences of text that matches the regular expression pattern. |
| Replace | It will replace the text that matches the regular expression pattern. |
| Split | It will splits the string into an array of substrings at the positions that matches the regular expression pattern. |

