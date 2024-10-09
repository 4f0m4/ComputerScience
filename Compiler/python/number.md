## Summary

The code defines a function to extract numeric literals from a string, including optional currency symbols and commas. It uses a regular expression to find matches, and when applied to an example string, it extracts and prints numbers like `25.99` and `100`.
## Code

```
import re

def separate_numbers(statement):
    # Regular expression to match numeric literals with optional commas and currency symbols
    number_pattern = r'(?<!\w)[\$\€\£]?[0-9,]+(?:\.[0-9]+)?(?!\w)'

    # Extract numbers from the statement
    numbers = re.findall(number_pattern, statement)

    return numbers

# Example usage:
statement = "The price is 25.99, and the quantity is 100."

result = separate_numbers(statement)

print("Numbers:")
print(result)
```
