## Summary
This C++ program identifies and prints identifiers from a file named `p5.txt`, while excluding keywords.

### Key Features:
- **File Handling**: The program reads from `p5.txt`.
- **Identifier Validation**:
  - Identifiers must start with a letter or an underscore (`_`).
  - Subsequent characters can be alphanumeric or underscores.
- **Keyword Exclusion**: The program maintains a list of keywords (e.g., `int`, `float`, `if`, etc.) and ensures that identified words are not part of this list.
  
### Overall Functionality:
The program serves as a simple lexical analyzer, helping to identify valid identifiers in source code while filtering out reserved keywords. It can be useful for understanding code structure and variable usage.

## File(p5.txt)
```
int a = 9;
if( b > 0)
  float new = 10;
int x , y , z ;
float sum = x + y + z ;
```
## Code
```
#include <iostream>
#include <fstream>
#include <cctype>
#include<string>
#include<bits/stdc++.h>

using namespace std;

bool isIdentifierChar(char c) {
    return isalnum(c) || c == '_';
}
bool isKeyword( string& word) {
    vector<string> keywords = {"int", "float", "if", "else", "while", "for", "return"}; // Add more keywords as needed

    return find(keywords.begin(), keywords.end(), word) != keywords.end();
}

void printIdentifiers() {
    ifstream file("p5.txt");
    if (!file.is_open()) {
        cout << "Unable to open file" << endl;
        return;
    }

    string word;
    while (file >> word) {
        if (isalpha(word[0]) || word[0] == '_') {
            bool isIdentifier = true;
            for (char c : word) {
                if (!isIdentifierChar(c)) {
                    isIdentifier = false;
                    break;
                }
            }
            if (isIdentifier && !isKeyword(word)) {
                cout << "Identifier: " << word << endl;
            }
        }
    }

    file.close();
}

int main() {

    //use printFile to print the file contents
    printIdentifiers();

    return 0;
}

```
