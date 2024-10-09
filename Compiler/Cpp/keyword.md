## Summary
This C++ program reads a file named `p3.txt` and identifies C programming keywords within its content.

### Key Features:
- **File Reading**: It reads and displays the entire content of `p3.txt`.
- **Keyword Detection**: It checks for specific C keywords (like `int`, `if`, `for`, etc.) in the file.
- **Keyword Output**: If a keyword is found, it prints the keyword to the console.

### Overall Functionality:
The program effectively reads a source code file and extracts and displays C keywords, helping users understand which keywords are present in the code.

## File(p3.txt)
```
int a=9,b;
float c = 6.7;
while(a>c)
break;
```

## Code
```
#include<bits/stdc++.h>
using namespace std;
void printFile()
{
    ifstream file("p3.txt");
    string line;
    cout << "Input file content:\n";
    if(file.is_open())
    {
        while(getline(file,line))
            cout<<line<<endl;
        file.close();
    }
    else
    {
        cout << "Unable to open file" << endl;
    }


}

int main()
{

    printFile();
    set<string> keywords = {"auto", "break", "case", "char", "const", "continue", "default",
                            "do", "double", "else", "float", "for",
                            "goto", "if", "int", "long",  "return", "short",
                            "signed", "sizeof", "struct", "switch", "typedef",
                            "unsigned", "void", "while"
                           };

    ifstream file("p3.txt");
    string word;

    if(file.is_open())
    {
        cout<<"Kewords are: ";
        while(file>>word)
        {

                size_t pos = word.find('(');
                string substring = word.substr(0, pos);
                // Check if the word is a C keyword
                if (keywords.find(substring) != keywords.end())
                {
                    // Print the keyword
                    cout << " " << substring ;
                }
        }
        cout<<endl<<"--------------------"<<endl;
        file.close();
    }
    else
    {
        cout << "Unable to open file" << endl;
    }


    return 0;
}
```
