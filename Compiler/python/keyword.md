## Summary
The code identifies Python keywords in a given statement using regular expressions. It defines the `separate_keywords` function, which constructs a pattern to match reserved keywords and extracts them from the input statement. An example statement is provided, and the found keywords are printed as a list.

## Code

```
import re
import keyword

def separate_keywords(statement):
    # Get the set of reserved keywords in Python
    keywords_set = set(keyword.kwlist)

    # Regular expression to match keywords as whole words
    keyword_pattern = r'\b(?:' + '|'.join(map(re.escape, keywords_set)) + r')\b'

    # Extract keywords from the statement
    keywords = re.findall(keyword_pattern, statement)

    return keywords

# Example usage:
statement = "if x == 5 and y < 10: print('Hello') else: print('Goodbye')"

result = separate_keywords(statement)

print("Keywords:")
print(result)

```
