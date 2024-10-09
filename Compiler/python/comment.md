## Summary
The code defines a function that removes comments from a given statement while extracting them. It uses a regular expression to identify both single-line (//) and multi-line (/* ... */) comments. The function returns the cleaned statement without comments and a list of the extracted comments. An example is provided to demonstrate its usage, displaying the statement without comments and the identified comments separately.

## code

```
import re

def separate_comments(statement):
    # Regular expression to match comments (both single-line and multi-line)
    comment_pattern = r'(\/\/[^\n]*|\/\*[\s\S]*?\*\/)'

    # Remove comments from the statement
    statement_without_comments = re.sub(comment_pattern, '', statement)

    # Extract comments from the statement
    comments = re.findall(comment_pattern, statement)

    return statement_without_comments, comments

# Example usage:
statement = """
// This is a single-line comment
x = 10; // Another comment at the end
/* This is a
   multi-line comment */
y = 20;
"""

result, comments = separate_comments(statement)

print("Statement without comments:")
print(result)

print("\nComments:")
for comment in comments:
    print(comment)

```
