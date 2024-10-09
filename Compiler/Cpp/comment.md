## Summary
This C++ program reads a file named `p2.txt` and identifies single-line and multi-line comments within the file. 

### Key Features:
- **Comment Detection**: 
  - It detects single-line comments starting with `//`.
  - It detects multi-line comments starting with `/*` and ending with `*/`, printing all lines in between.
  
- **File Handling**: 
  - It opens the specified file, reads its contents, and outputs the lines containing comments.

- **Error Handling**: 
  - The program checks if the file opens successfully and handles errors appropriately.

### Overall Functionality:
The program effectively parses a text file to extract and display comments, allowing users to understand which parts of the code are comments.
## File (p2.txt)

```
// This is a single-line comment
x = 10;// Another comment at the end
x++;/* This is a
   multi-line comment */
y = 20;
while(true){//last comment
break;
}
```
## Code

```
#include <iostream>
#include <fstream>
#include <string>

using namespace std;

bool isSingleLineComment(const string& line)
{
    size_t pos = line.find("//");
    return pos != string::npos && (pos >=0);
}

bool isMultiLineCommentStart(const string& line)
{
    size_t pos = line.find("/*");
    return pos != string::npos &&(pos >=0);
}

bool isMultiLineCommentEnd(const string& line)
{
    return line.find("*/") != string::npos;
}
void readfile_contents()
{
    ifstream file("p2.txt");
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
    readfile_contents();
    ifstream inputFile("p2.txt");
    string line;

    if (inputFile.is_open())
    {

        cout<<"----------------------------------"<<endl;
        while (getline(inputFile, line))
        {

            if (isSingleLineComment(line))
            {
                cout << "Single line comment: " << line.substr(line.find("//")) << endl;
            }
            else if (isMultiLineCommentStart(line))
            {
                cout << "This is a multi-line comment: " << line.substr(line.find("/*")) << endl;

                // read and output lines until the end of multi-line comment
                while (getline(inputFile, line) && !isMultiLineCommentEnd(line))
                {
                    cout << line << endl;
                }

                if (isMultiLineCommentEnd(line))
                {
                    cout << line << endl;
                    cout << "--End of multi-line comment--" << endl;
                }
            }
        }

        inputFile.close();
    }
    else
    {
        cout << "Unable to open file" << endl;
    }

    return 0;
}
```
