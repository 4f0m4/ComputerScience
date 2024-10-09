## Summary
This C++ program reads a file named `p4.txt` and identifies arithmetic operators within its content.

### Key Features:
- **File Reading**: It reads and displays the content of `p4.txt` line by line.
- **Arithmetic Operator Detection**: The program checks for arithmetic operators (`+`, `-`, `*`, `/`, `%`) that are not part of consecutive operator sequences (e.g., `++` or `--`).
- **Output**: For each detected arithmetic operator, it prints the line number and the operator itself.

### Overall Functionality:
The program serves as a simple tool to analyze source code, helping users identify and understand the usage of arithmetic operators across different lines in a given file.

## File(p4.txt
a= 8+9
b= 8*9
c= 8/9
d++;
d+=4;

## Code

```
#include<bits/stdc++.h>
using namespace std;

bool isArithmeticOperator(char prev_c, char c, char next_c) {
   return (c == '+' || c == '-' || c == '*' || c == '/' || c == '%') && !((prev_c == '+' || prev_c == '-') && c == prev_c) && !((next_c == '+' || next_c == '-') && c == next_c);

}

void printFile() {
    ifstream file("p4.txt");
    string line;
    cout << "Input file content:\n";
    if(file.is_open()) {
        while(getline(file, line))
            cout << line << endl;
        file.close();
    } else {
        cout << "Unable to open file" << endl;
    }
}

int main() {
    printFile();
    ifstream file("p4.txt");
    string line;
    int lineNumber = 1;

    if(file.is_open()) {
        while(getline(file, line)) {
            for(int i = 0; i < line.length(); i++) {
                char prev_c = (i > 0) ? line[i - 1] : ' ';
                char next_c = (i < line.length() - 1) ? line[i + 1] : ' ';
                if (isArithmeticOperator(prev_c, line[i], next_c)) {
                    cout << "Line " << lineNumber << ": " << line[i] << endl;
                }
            }
            lineNumber++;
        }
        file.close();
    } else {
        cout << "Unable to open file" << endl;
    }

    return 0;
}
```
