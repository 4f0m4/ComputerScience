## Summary
This C++ program scans a file named `p7.txt` to identify and print relational operators used in the text.

### Key Features:
- **Relational Operator Detection**: The program looks for common relational operators: `<`, `>`, `<=`, `>=`, `==`, and `!=`.
- **Line Number Tracking**: It keeps track of the line number where each operator is found.
- **Comment Handling**: Lines starting with `#` are treated as comments and skipped.

### Overall Functionality:
The program reads through the specified file, checking each line for relational operators and printing their occurrences along with the respective line numbers. This functionality can be useful for code analysis, helping to identify comparison operations in source code.

## File (p5.txt)
```
if x == 5 and y < 10: print('Hello')
```

## Code
```
#include <iostream>
#include <fstream>
#include <string>
#include <vector>

using namespace std;

bool isRelationalOperator(const string& line, size_t pos) {
    // List of relational operators
    const vector<string> operators = {"<", ">", "<=", ">=", "==", "!="};

    for (const auto& op : operators) {
        if (line.substr(pos, op.length()) == op) {
            return true;
        }
    }

    return false;
}

void findRelationalOperators(const string& filename) {
    ifstream file(filename);
    if (!file.is_open()) {
        cerr << "Error: Unable to open the file '" << filename << "'" << endl;
        return;
    }

    string line;
    int lineNumber = 0;

    while (getline(file, line)) {
        lineNumber++;
        if(line[0]=='#'){
            continue;
        }
        for (size_t i = 0; i < line.length(); i++) {
            if (isRelationalOperator(line, i)) {
                cout << "Line " << lineNumber << ": " << line.substr(i, 2) << endl;
            }
        }
    }

    file.close();
}

int main() {
    string filename = "p7.txt";
    findRelationalOperators(filename);
    return 0;
}
```
