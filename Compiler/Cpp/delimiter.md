## Summary
This C++ program reads a file named `p1.txt` and identifies specified delimiters (`,`, `;`, `'`, `{`, `}`, `|`, `\`) in each line. 

### Key Features:
- **Delimiter Detection**: It searches for and prints the positions of delimiters in each line.
- **File Handling**: The program opens the file, reads it line by line, and checks for delimiters, providing output for each line.
- **Error Handling**: It checks if the file opens successfully and handles errors appropriately.

Overall, it effectively parses a text file to find specific characters.
## file(p1.txt)
```
a=b+c;
int a,b,c;
a = 0/
```
## Code

```
#include<iostream>
#include<fstream>
#include<set>
using namespace std;

void findDel(const string& s) {
    set<char> delimiters ={',', ';', '\'', '{', '}', '|', '\\'};

    int l = s.length();

    bool flag=false;

    cout << "Line: " << s << endl;

    for (char delimiter : delimiters) {
        size_t pos = s.find(delimiter);
        while (pos != -1) {
            flag=true;
            cout << "Delimiter '" << delimiter << "' found at position " << pos << endl;
            pos = s.find(delimiter, pos + 1);
        }
    }
    if(!flag){
        cout<<"No delimiters is found!"<<endl;
    }

    cout << "---------------------" << endl;
}

int main() {
    ifstream myfile;
    string s;

    myfile.open("p1.txt");

    if (!myfile.is_open()) {
        cout << "Error opening file." << endl;
        return 1;
    }

    while (getline(myfile, s)) {
        findDel(s);
    }
    myfile.close();

    return 0;
}
```
