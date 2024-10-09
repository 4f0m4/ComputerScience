## Summary
The code defines a function to tokenize a given statement into identifiable components. It uses regular expressions to match various token types, including identifiers (words), numbers, delimiters (commas and semicolons), and operators (like plus signs). The function collects all matches and returns a list of tokens, each labeled with its type. An example demonstrates its usage by tokenizing a sample statement and printing each token alongside its type.


## code

```
import re

def tokenize_statement(statement):
    # Define regular expressions for common tokens
    regex_patterns = [
        (r'\b\w+\b', 'IDENTIFIER'),  # Word tokens (identifiers)
        (r'\d+', 'NUMBER'),          # Number tokens
        (r'[,;]', 'DELIMITER'),      # Delimiter tokens
        (r'\+', 'OPERATOR'),         # Example operator token
        # Add more patterns for operators, keywords, etc.
    ]

    tokens = []

    for pattern, token_type in regex_patterns:
        matches = re.findall(pattern, statement)
        tokens.extend([(match, token_type) for match in matches])

    return tokens

# Example usage:
statement = "x = 10; y = 20, z = x + y;"
tokens = tokenize_statement(statement)

print("Tokens:")
for token, token_type in tokens:
    print(f"{token}: {token_type}")

```
