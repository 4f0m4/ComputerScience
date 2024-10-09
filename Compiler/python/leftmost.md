## Summary
The code implements a function for performing leftmost derivation in a context-free grammar. The leftmost_derivation function recursively replaces the leftmost non-terminal in a string with its productions from the grammar, printing each step of the derivation.

## Code

```
def leftmost_derivation(grammar, current_symbol, current_string, derivation_steps):
    if current_symbol not in grammar:
        return

    for production in grammar[current_symbol]:
        if current_string.startswith(production):
            new_string = current_string.replace(production, current_symbol, 1)
            new_step = (current_symbol, new_string)
            print(f"{new_step[0]} => {new_step[1]}")
            derivation_steps.append(new_step)
            leftmost_derivation(grammar, current_symbol, new_string, derivation_steps)

# Example usage
grammar = {
    'S': ['A'],
    'A': ['aB'],
    'B': ['b', ''],
}

start_symbol = 'S'
input_string = 'abb'

derivation_result = []
leftmost_derivation(grammar, start_symbol, input_string, derivation_result)

```
