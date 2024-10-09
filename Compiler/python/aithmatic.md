## Summary
The code defines a function to extract arithmetic operators (`+`, `-`, `*`, `/`, `**`) from a given mathematical expression. It uses regular expressions to find these operators and returns them as a list. For example, it processes the statement `"x = 3 + 4 * (5 - 2)"` and prints the operators found: `['+', '*', '-']`.

## code

```
import re

def separate_arithmetic_operators(statement):
    # Regular expression to match arithmetic operators
    operator_pattern = r'[+\-*/]|\*\*'

    # Extract arithmetic operators from the statement
    operators = re.findall(operator_pattern, statement)

    return operators

# Example usage:
statement = "x = 3 + 4 * (5 - 2)"

result = separate_arithmetic_operators(statement)

print("Arithmetic Operators:")
print(result)

```
