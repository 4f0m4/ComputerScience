## Summary
The code defines a function to extract relational operators from a given string using a regular expression. It matches operators like `<`, `<=`, `>`, `>=`, `==`, and `!=`. When applied to an example statement, it identifies and prints the relational operators found, such as `==` and `<`.

## Code
```
import re

def separate_relational_operators(statement):
    # Regular expression to match relational operators
    relational_operator_pattern = r'[<>]=?|==|!='

    # Extract relational operators from the statement
    operators = re.findall(relational_operator_pattern, statement)

    return operators

# Example usage:
statement = "if x == 5 and y < 10: print('Hello')"

result = separate_relational_operators(statement)

print("Relational Operators:")
print(result)

```
