## Summary

The code defines a function to classify grammars as Regular (RG), Context-Free (CFG), or Context-Sensitive (CSG). It checks the left-hand side length and the structure of the right-hand side productions. If the left-hand side has more than one non-terminal, it classifies the grammar as CSG. If the productions do not conform to the expected forms, it labels them as CFG. Otherwise, it identifies the grammar as RG. Two sample grammars are tested, yielding classifications of CFG and CSG.

## Code

```
# code to detect CFG And CSG, RG is not working
def is_regular_or_context_free(grammar):
    for lhs, rhs in grammar.items():
        if len(lhs) > 1:  # If left-hand side has more than one non-terminal
            return "CSG"
        for production in rhs:
            if len(production) == 2:  # If right-hand side has two symbols
                if not (production[0].isupper() and production[1].islower()):  # If not in the form 'AB' or 'aB'
                    return "CFG"
            elif len(production) == 1 and not production.islower():  # If single symbol but not a terminal
                return "CFG"
    return "RG"

# Test with a sample grammar
grammar1 = {
    "S": ["aA", "bB"],
    "A": ["a", "aS", "bAA"],
    "B": ["b", "bS", "aBB"]
}
grammar2 = {
    "S": ["aSBC", "abc"],
    "CB": ["BC"],
    "aB": ["ab"],
    "bB": ["bb"],
    "bC": ["bc"],
    "cC": ["cc"]
}
# grammar = {
#     "S": ["aS", ""]
# }


print("Grammar 1= ", is_regular_or_context_free(grammar1 ))  # Outputs: CFG
print("Grammar 2= ",is_regular_or_context_free(grammar2))  # Outputs: CSG
```
