NOTES

```C++
#include <iostream>
#include <iomanip> // cout >> fixed >> setprecision() 
#include <cmath> //math functions such as pow(x, y) 
#include <cstdlib> // used for rand(); function 
#include <string>      // Supports use of "string" data type
#include ios //WHAT IS THIS?
#include <conio.h> // getch(); for windows only.
#include <cctype> //functions for characters/string interations http://www.cplusplus.com/reference/cctype/
using namespace std;
#include <cassert> //if expression is false, prints line--unit testing. 
https://www.javatpoint.com/cpp-string-find-function

1. How to limit the amount of digits in a double? 
cout << fixed << setprecision(2) 

2. How do I write z = sqrt(x^2 + y^2) in C++? 
	1. x = pow(x, 2.0);
	2. y = pow (y, 2.0);
	3. z = sqrt(x + y);

3. How do we get an entire line as a string?
getline(cin, firstString);
getline(cin, secondString);

Mixing cin >> and getline() can be tricky, because cin >> leaves the newline in the input, while getline() does not skip leading whitespace. When following cin >> with getline(), an extra getline() is needed to get past the newline left in the input by cin >>.


4. rand(time(0));  // Unique seed
      rand() alone will produce a random number, but if you run the program again and again
      it is going to return the same value. 
   thus, 
   srand(time(NULL)) // this is required, so it grabs hours minutes and seconds. 
      //must #include <ctime> 
      //NULL is a C++ constant that evalutes to 0. 

CHAR AND STRING MODIFICATIONS
- isalpha(c) // true if alphabetic a-z or A-Z
- isdigit(c) // true if digit 0-9
- isspace(c) // true if whitespace ' ' or  '\n'
- toupper(c) //uppercase; does not modify argument; returns value.
- tolower(c) //lowercase; does not modify argument; returns value.
- .at(0) //indicates specific string placements given that string name is userStr. 
    - isspace(userStr.at(3))
- searchName.substr() //subtracts the string at a given point. 
if (isdigit(passCode.at(0)) || isdigit(passCode.at(1)) || isdigit(passCode.at(2)))
   hasDigit = true;
-stringName.erase() //erases string after a given point
-----------------------
STRING SIZE DECLARATION
string s(N, X), where N = string size, and X = a character that itll be filled with. 
====---------------------------
2. converting data type int to string using to_string() function #include <string>
string intToString = to_string(remaining);
-------------------------------
SWITCH STATEMENTS 
- variables or char comparasions only; 
Good practice is to always have a default case for a switch statement. 

switch (expression) {
   case constantExpr1: 
      // Statements
      break;

   case constantExpr2:
      // Statements
      break;
   
   ...
   
   default: // If no other case matches
      // Statements
      break;
}

	OMITTING THE BREAK STATEMENT 
		-  makes sense for "falling through cases"

#include <iostream>
using namespace std;

int main() {
   int dogAgeYears;
   int dogAgeMonths;

   cout << "Enter dog's age (in years): ";
   cin >> dogAgeYears;

   if (dogAgeYears == 0) {
      cout << "Enter dog's age in months: ";
      cin  >> dogAgeMonths;

      switch (dogAgeMonths) {
         case 0:
         case 1:
         case 2:
            cout << "That's 0..14 human months." << endl;
            break;

         case 3:
         case 4:
         case 5:
         case 6:
            cout << "That's 1..5 human years." << endl;
            break;

         case 7:
         case 8:
            cout << "That's 5..9 human years." << endl;
            break;

         case 9:
         case 10:
         case 11:
         case 12:
            cout << "That's 9..15 human years." << endl;
            break;

         default:
            cout << "Invalid input." << endl;
            break;
      }
   }
   else {
      cout << "FIXME: Do earlier dog year cases." << endl;
      switch (dogAgeYears) {
      }
   }

   return 0;
}
	

--------
QUESTION: What is the value of encoded value for 'E'? 
switch (userChar) {
   case 'A':
      encodedVal = 1;
      break;

   case 'B':
      encodedVal = 2;
      break;

   case 'C':

   case 'D':
      encodedVal = 4;
      break;

   case 'E':
      encodedVal = 5;

   case 'F':
      encodedVal = 6;
      break;

   default:
      encodedVal = -1;
      break;
      
ANSWER: 6. No break statement. 
}---------
SUBTRACTING PART OF A STRING

 while (inputName.size() > 0) {
      searchName = inputName;
      for (j = 0; j < inputName.size(); ++j) {
         searchName.at(j) = tolower(inputName.at(j));
      }
      isCoreGtld = false;

      periodCounter = 0;
      for (i = 0; i < searchName.size(); ++i) {
         if (searchName.at(i) == '.') {
            periodCounter++;
            periodPosition = i;
         }
      }

      if ((periodCounter == 1) && (searchName.at(0) != '.')) {
         // Extract the top-level domain name starting at the period's position.
         // Ex: If searchName = "example.com", the next statement extracts ".com"
         theTld = searchName.substr(periodPosition); 

			
 main.cpp: In function ‘int main()’:
main.cpp:13:22: warning: comparison of integer expressions of different signedness: ‘int’ and ‘std::__cxx11::basic_string<char>::size_type’ {aka ‘long unsigned int’} [-Wsign-compare]
   13 |    for (int i = 0; i < userString.size(); i++)
      |                    ~~^~~~~~~~~~~~~~~~~~~  
			
					-- Happens when you try to compare a string to an integer value. Remember why...? 
					
------------
Dev-Cpp is just IDE (frontend) for coder and behind it sits MinGW with GCC 4.9.2 as compiler*. 
So every time you click "Run" or "Build" it is GCC to do the dirty job. 
GCC by default uses C++03 standard and to use newer one you have to tell it explicitly via compiler flag -std=c++11. 
You can change it in Tools->Compiler Options->Settings->Code generation->Language standard (-std).
-------------
int = userInput; 
string s = to_string(userInput); //stores int value into string 
cout << s << endl; //will print string format of int userInput //refer to 4.22 LAB countdown 
			//only works* in C++ 11, so it will NOT work out the box for DEV-C++ 
			//DEV-C++ out the box runs GCC 4.9.2, so change it via Tools -> Compiler Options _> Settings -> Code generation 
			// --> Language standard -std --> select C++ 11; 

----
STRING COMPARASIONS
https://www.cplusplus.com/reference/cstring/strcmp/
----
while (userInput != "Done" && userInput != "done" && userInput != "d") {
      for (i = userInput.size(); i >= 0; i--) {
         cout << userInput.at(i);
      }
ERROR: out-of-range 
FIX: it's because "i" userInput.at(i) would be 1 greater than the actual string. 
FIX: userinput.size() - 1 
-----
What is "wrong" with the below code?

int IntMax(int numVal1, int numVal2) {
   if (numVal1 > numVal2) {
      numVal2 = numVal1; // numVal2 holds max
   }

   return numVal2;
}


Avoid assigning pass by value parameters.
May be confusing later on and lead people to think numVal2 is being updated in memory--when in fact
numVal2 is deleted as soon as the function is returned. 
While such programming "saves" you from declaring an additional variable, 
one should strive for understanable code and declare another local variable to assign. 
----
Difference between assign by value vs assign by reference?
- Assign by value: even if the variable's name match in both main and function, they are seperate 
unless declared otherwise.

e.g., 

void declareByVariable (int x) {
...
}

main () {
   int x = 6
}
Both x values are stored in different memory locations and hence have different values. 

-Assign by value; basically interconnecting both variables to 1 location. //...fact check this

void declareByVariable (int& x) {
...
}

main () {
   int x = 6
}

    //now both variables will have the same value;
   //note the parameters don't necessarily need to have the same variable name. 

-----
TLDR: linking two variables together.
Figure 5.10.2: Reference variable example.
#include <iostream>
using namespace std;

int main() {
   int usrValInt;
   int& usrValRef = usrValInt;  // Refers to usrValInt

   cout << "Enter an integer: ";
   cin  >> usrValInt;

   cout << "We wrote your integer to usrValInt." << endl;
   cout << "usrValInt is: " << usrValInt << "." << endl;
   cout << "usrValRef refers to usrValInt, and is: " << usrValRef << "." << endl;

   usrValInt = 99;
   cout << endl << "We assigned usrValInt with 99." << endl;
   cout << "usrValInt is now: " << usrValInt << "." << endl;
   cout << "usrValRef is now: " << usrValRef << "." << endl;
   cout << "Note that usrValRef refers to usrValInt, so it changed too." << endl;
   return 0;
}

Enter an integer: 42
We wrote your integer to usrValInt.
usrValInt is: 42.
usrValRef refers to usrValInt, and is: 42.

We assigned usrValInt with 99.
usrValInt is now: 99.
usrValRef is now: 99.
Note that usrValRef refers to usrValInt, so it changed too.
----
What is a global variable? 

Declare it before main, and you can initialize it inside main. 

#include <iostream>

using namespace std;

int x = 2; //global variable

main()
{
   int a = 4;b = 7;

   cout << x << endl; //will print 2
   //however

   int x = 3; //same variable name as global variable, will take precedence in local. 
   cout << x << endl; //will print 3
}

-----
5.11 Functions with string/vector parameters
The string serves as function input and output. T
he string parameter must be pass by reference, achieved using &, 
so that the function modifies the original string argument (userStr) and not a copy.



#include <iostream>
#include <string>
using namespace std;

// Function replaces spaces with hyphens
void StrSpaceToHyphen(string& modStr) { //refer to this line
   unsigned int i;   // Loop index
   
   for (i = 0; i < modStr.size(); ++i) {
      if (modStr.at(i) == ' ') {
         modStr.at(i) = '-';
      }
   }
}

int main() {
   string userStr;  // Input string from user
   
   // Prompt user for input
   cout << "Enter string with spaces: " << endl;
   getline(cin, userStr);
   
   // Call function to modify user defined string
   StrSpaceToHyphen(userStr);
   
   // Output modified string
   cout << "String with hyphens: ";
   cout << userStr << endl;
   
   return 0;
}
----
Sometimes, a programmer might declare a vector or string parameter as "pass by reference"
even though the function does not modify the parameter. Why?

improves performance by preventing memory overhead of copying the argument to local. 

----
Explain why a 'const' might be used in a vector or string parameter? 
Also, why is 'const' and pass by reference used together? seems counter-intutitve.

The keyword const can be prepended to a function's vector or 
string parameter to prevent the function from modifying the parameter.
 Programmers commonly make a large vector or string input parameter pass by reference, 
 to gain efficiency, while also making the parameter const, to prevent assignment.

 tl;dr: 
 'const' is used to prevent the function from modifying the parameter to prevent assignment.
at the SAME TIME, pass by reference '&' is used. Why?
improves efficency of compiler. pass by reference prevents another copy's declaration.

Tl;d
So, to summarize-

- Pass-by-value and pass-by-const-reference imply similar things - you want 
to be able to look at the value without being able to modify it.

- Any time you could use pass-by-value you could instead use 
pass-by-const-reference without affecting the correctness of the program. 
However, there are performance tradeoffs between the indirection of the reference and 
the cost of copying and destructing the parameter.

- Pass-by-non-const-reference should be used to indicate "I want to modify the argument."
- You cannot pass rvalues into functions that take their arguments by non-const reference.

https://stackoverflow.com/a/5060218
---
In summary:
1.Define a functions output or input/output parameters as pass by reference.
But create output parameters sparingly, striving to use return values instead.

2.Define input parameters as pass by value.
Except for large items (perhaps 10 or more elements); use constant pass by reference for those.
     - WHY??
         -- Why make local copies at all? The reason is efficiency. 
         For parameters involving just a few memory locations, making a local copy enables 
         the compiler to generate more efficient code, in part because the compiler can place 
         those copies inside a tiny-but-fast memory inside the processor called a register 
         file—further details are beyond our scope.

---
PASS BY REFERENCE WILL ALWAYS MAKE THE ARGUEMENT MODIFABLE.
-----
void MakeSentenceExcited(string& sentenceText) {

   unsigned int i; //Loop index
   /* Your solution goes here  */
   for (i = 0; i < sentenceText.size(); i++) 
      {
         if (sentenceText.at(i) == '.')
            sentenceText.at(i) = '!'; BUG ERROR, I WROTE == INSTEAD OF =. 
      }

----
For a function with a string parameter, the function must include a second parameter for the string size.

FALSE. 
The strlen() function can be used to determine the string size, so a second parameter is not needed.
----
T/F:
Passing a C string to a function creates a copy of that string within the function.

FALSE.
//All characters in the C string are not passed to the function. Rather, a pointer to the string is passed.
----
T/F:
A C string is automatically passed by pointer.

TRUE.
Any array (including a C string) is automatically passed using a pointer, to prevent inefficient copying of large arrays or strings.

----

What is wrong with the following?
The following is a valid start of a function definition: 

void myFct(int num1 = 0, int num2 = 0, char usrMethod) {
   ...

}

A function call(s) last arguments can be omitted, 
so parameter default values must start from the end of the parameter list. 
The compiler will generate an error like "default argument missing for parameter 3".
-----
7.6 Vector resize
Commonly, the size of a list of items is not known during a program's compile time. 
Thus, a vector's size need not be specified in the vector's declaration. 
Instead, a vector's size can be set or changed while a program executes using resize(N). 
Ex: highScore.resize(10) resizes the highScores vector to have 10 elements.
```