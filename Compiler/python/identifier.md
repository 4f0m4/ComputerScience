## Summary
The code extracts valid identifiers from a given statement using a regular expression. It defines a function `separate_identifiers` that finds identifiers matching the pattern of starting with a letter or underscore, followed by word characters. An example statement is processed, and the identified names are printed as a list.

## Code

```
import re

def separate_identifiers(statement):
    # Regular expression to match valid identifiers
    identifier_pattern = r'\b[a-zA-Z_]\w*\b'

    # Extract identifiers from the statement
    identifiers = re.findall(identifier_pattern, statement)

    return identifiers

# Example usage:
statement = " temp = 10; temp2 = 3.14;"

result = separate_identifiers(statement)

print("Identifiers:")
print(result)
```
