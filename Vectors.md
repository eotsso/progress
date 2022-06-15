1. [BUG]: all negative values returned maxMiles = 0; 

```C++

#include <iostream>
using namespace std;

int main() {
   const int NUM_ROWS = 2;
   const int NUM_COLS = 2;
   int milesTracker[NUM_ROWS][NUM_COLS];
   int i;
   int j;
   int maxMiles = 0;
   int minMiles = 0;
   int value;

   for (i = 0; i < NUM_ROWS; i++){
      for (j = 0; j < NUM_COLS; j++){
         cin >> value;
         milesTracker[i][j] = value;
      }
   }

   /* Your solution goes here  */
   

   for (i = 0; i < NUM_ROWS; i++) {
      for (j = 0; j < NUM_COLS; j++) {
         if (minMiles > milesTracker[i][j])
            minMiles = milesTracker[i][j]; 
         
         if (maxMiles < milesTracker[i][j])
            maxMiles = milesTracker[i][j];
      }
   }
   
   cout << "Min miles: " << minMiles << endl;
   cout << "Max miles: " << maxMiles << endl;

   return 0;
}

----SOLUTION----
//assign maxMiles and minMiles with first element in array. 
   maxMiles = milesTracker[0][0];
   minMiles = milesTracker[0][0];
# 7.6 [[Vector resize]]

Commonly, the size of a list of items is not known during a program's compile time. Thus, a vector's size need not be specified in the vector's declaration. Instead, a vector's size can be set or changed while a program executes using resize(N). Ex: `highScore.resize(10)` resizes the highScores vector to have 10 elements.

`resize()` can be called multiple times. If the new size is larger, resize() adds elements at the end. If smaller, resize() deletes elements from the end. If userScores has size 3 (elements 0, 1, 2), `userScores.resize(2);` would delete element 2, leaving elements 0 and 1. A subsequent access to userScores.at(2) would result in an error.

# 7.7 [[Vector push_back()]] , [[back()]], [[pop_back()]]

- push_back()
```C++
void push_back(const int newVal);  
//Append new element having value newVal.

// playersList initially 55, 99, 44 (size is 3)
playersList.push_back(77); // Appends new element 77 
// playersList is now 55, 99, 44, 77 (size is 4)

```

- back()
```C++
int back();  
//Returns vector's last element. Vector is unchanged.

// playersList initially 55, 99, 44
cout << playersList.back(); // Prints 44 
// playersList is still 55, 99, 44
```

- pop_back()
```C++
void pop_back();  
//Removes the last element.

// playersList is 55, 99, 44 (size 3)
playersList.pop_back(); // Removes last element
// playersList now 55, 99 (size 2)

cout << playersList.back(); // Common combination of back() 
playersList.pop_back();     // followed by pop_back()
// Prints 99. playersList becomes just 55

cout << playersList.pop_back(); // Common error: 
	                                // pop_back() returns void
```

- Using push_back(), back(), and pop_back(): A grocery list example.
```C++
/*
The program below declares a vector groceryList, which is initially empty. As the user enters grocery items one at a time, the program uses push_back() to append the items to the list. When done, the user can go shopping, and is presented one list item at a time (which the user presumably finds and places in a shopping cart). The program uses back() to get each item from the list and pop_back() to remove the item from the list. When the list is empty, shopping is finished.
*/

#include <iostream>
#include <vector>
#include <string>
using namespace std;

int main() {
   vector<string> groceryList; // Vector storing shopping list
   string groceryItem;         // Individual grocery items
   string userCmd;             // User input
   
   // Prompt user to populate shopping list
   cout << "Enter grocery items or type done." << endl;
   cin >> groceryItem;
   while (groceryItem != "done") {
      groceryList.push_back(groceryItem);
      cin >> groceryItem;
   }
   
   // Display shopping list
   cout << endl << "Enter any key for next item." << endl;
   while (groceryList.size() > 0) {
      groceryItem = groceryList.back();
      groceryList.pop_back();
      cout << groceryItem << "   ";
      cin >> userCmd;
   }
   cout << endl << "Done shopping." << endl;
   
   return 0;
}

------------
Enter grocery items or type done.
Oranges
Apples
Bread
Juice
done

Enter any key for next item.
Juice   a
Bread   a
Apples   a
Oranges   a

Done shopping.


```

# 7.12 Two-dimensional arrays
- 2-D arrays are conceptually a table, but it's implemented in memory by **row-major order. ** 

## 2-D Array Initalization and Format
```C++
// Initializing a 2D array
int numVals[2][3] = { {22, 44, 66}, {97, 98, 99} };

// Use multiple lines to make rows more visible
int numVals[2][3] = {
   {22, 44, 66}, // Row 0
   {97, 98, 99}  // Row 1
};
```

- Write a statement that assigns 99 into the fifth row, third column of array numVals. Note: the first row/column is at index 0, not 1.
	- `numVals[4][2] = 99;`


# 7.13 Char arrays / C string || `#include <cstring>` (These are NOT strings from C++)
C strings (which are not C++ strings) is basically a character array appended by a null chracter '\0' to indicate an end of an array. Therefore, a char moviesTitle[20] can hold a maximum of 0 to 19 characters becuase one character must be reserved for the null character, which is known as a **null-terminating string**. 

A string can be shorter than the character array it occupies. 
`char movieTitle[20] = "Star Wars";` is valid because the compiler automatically appends on 10th memory location, despite the array having 20 memory locations.

# You cannot assign a new "value" to a "C string". C strings must be initialized and declared at the same time. Otherwise, functions exist to copy one string to another. 
After a string is declared, a programmer may not later assign the string as in `movieTitle = "Indiana Jones";`. That statement tries to assign a value to the char array variable itself, rather than copying each character from the string on the right into the array on the left. Functions exist to _copy_ strings, such as strcpy(), discussed elsewhere.

A programmer can traverse a string using a loop that stops when reaching the null character.

## 1. Transversing a String, and other bug errors such as not stopping at null char, and accessing beyond memory index
- `for (i = 0; arrayVal[i] != '\0'; i++) {}`

```C++
Figure 7.13.2: Traversing a C string.

#include <iostream>
using namespace std;

int main() {
   char userStr[20] = "1234567890123456789"; // Input string
   int i; 
   
   // Prompt user for string input
   cout << "Enter string (<20 chars): ";
   cin >> userStr;
   
   // Print string
   cout << endl << userStr << endl;
   
   // Look for '@'
   for (i = 0; userStr[i] != '\0'; ++i) {
      if (userStr[i] == '@') {
         cout << "Found '@'." << endl;
      }
   }
   cout << endl;
   
   
   // The following is an ERROR.
   // May print chars it shouldn't.
   // Problem: doesn't stop at null char.
   cout << "\""; // Print opening "
   for (i = 0; i < 20; ++i) { // Print each char
      cout << userStr[i];
   }
   cout << "\"" << endl;      // Print closing "
   
   
   // The following is an even WORSE ERROR.
   // Accesses beyond valid index range.
   // Program may crash.
   cout << "\""; // Print opening "
   for (i = 0; i < 30; ++i) {
      cout << userStr[i];
   }
   cout << "\"" << endl; // Print closing "
   
   return 0;
}
```
# Another bug error with C strings are users entering a string value larger than the character array. 
- A solution is ensuring user output is zero to (arraySize - 1) (because of the null character) through if statement. 

# # 7.14 C-String library functions ; targetText = orgName does NOT work. 
`#include <string>`

```C++
char orgName[100] = "United Nations"; 
char userText[20] = "UNICEF"; 
char targetText[10];
```

1. strcpy()
`strcpy(destStr, sourceStr)`  
	Copies sourceStr (up to and including null character) to destStr.
	(The strcpy() function copies str2 to str1, up to and including str2's null character.)
```C++
strcpy(targetText, userText); // Copies "UNICEF" + null char to targetText 

strcpy(targetText, orgName);  // Error: "United Nations" has > 10 chars

targetText = orgName;    // Error: Strings can't be     
```

2. strncpy()
`strncpy(destStr, sourceStr, numChars)`    
	Copies up to numChars characters. 
		*Note: common errors include copying source string that is too large, causing out-of-range access*

```C++
strncpy(orgName, userText, 6); // orgName is "UNICEF Nations"
```

3.  strcat()
`strcat(destStr, sourceStr)`  
  The strcat() function starts at str1's null character, then copies str2 to str1, up to and including str2's null character.
```C++
strcat(orgName, userText); // orgName is "United NationsUNICEF"
```

4. strncat()
`strncat(destStr, sourceStr, numChars)`  
	Copies up to numChars characters to destStr's end, then appends null character.
	
```C++
strcpy(targetText, "abc");           // targetText is "abc"

strncat(targetText, "123456789", 3); // targetText is "abc123"
```

## Why is the following code not correct? (string functions)
```C++
char userStr[5];
strncpy(userStr, "Goodbye", 4);
```
- Answer: "Good" is copied into userStr[0] . . . [3], but it does not append a null character, so the resulting string has no null character. 

## Why is the following code not correct?

```C++
strcat(userStr, '!'); 
```
- Answer: strcat()'s 2nd parameter must be a string, not a single char--will result in errors.

# 7.14 String Functions (Retrieving Information)

```C++
Given:  

char orgName[100] = "United Nations"; 
char userText[20] = "UNICEF"; 
char targetText[10];
```

1. strchr()

`strchr(sourceStr, searchChar)`  //for single char
  Returns NULL if searchChar does not exist in sourceStr. (Else, returns address of first occurrence, discussed elsewhere).  
NULL is defined in the cstring library. Else, returns ASCII value of found character. 


```C++
if (strchr(orgName, 'U') != NULL) { // 'U' exists in orgNam; 'U' exists in "United Nations", branch taken
```

2. strlen()

`size_t strlen(sourceStr)`  
  Returns number of characters in sourceStr up to, but not including, first null character. size_t is integer type.
```C++
x = strlen(orgName);    // Assigns 14 to x 
x = strlen(userText);   // Assigns 6 to x
x = strlen(targetText); // Error: targetText may lack null char
```

Iterating through a String using strlen()
```C++
for (i = 0; i < strlen(userName); ++i) {
      if (userName[i] == ' ') {
         userName[i] = '_';
```
3. strcmp()

`int strcmp(str1, str2)`   
  Returns 0 if str1 and str2 are equal, non-zero if they differ. 
  (-) if str1 less than str2. (+) if str1 is greater than str2. Comparasions are for ASCII values at each element. 
	  *Note: A common error is to use == when comparing C strings, which does not work. str1 == str2 compares the strings' addresses, not their contents.*
	  *Note: r. Another common error is to forget to compare the result of strcmp with 0, as in `if (strcmp(str1, str2)) {...}`. The code is not a syntax error, but is a logic error because the if condition will be false (0) when the strings are equal. The correct condition would instead be `if (strcmp(str1, str2) == 0) {...}`. Although strcmp returns 0, a good practice is to avoid using `if (!strcmp(str1,str2)) {...}` because that 0 does not represent "false" but rather is encoding a particular situation.*

```C++
if (strcmp(orgName, "United Nations") == 0) {
   ... // Equal, branch taken
}
if (strcmp(orgName, userText) != 0) {
   ... // Not equal, branch taken

//DO NOT COMPARE STRINGS DIRECTLY. 
```

#  [[Char Functions]]
```C++
char myString[30] = "Hey9! Go";
```

`isalpha(c) -- Returns true if c is alphabetic: a-z or A-Z.`

isalpha('A');            // Returns true
isalpha(myString[0]);    // Returns true because 'H' is alphabetic
isalpha(myString[3]);    // Returns false because '9' is not alphabetic

`isdigit(c) -- Returns true if c is a numeric digit: 0-9.`

isdigit(myString[3]);    // Returns true because '9' is numeric
isdigit(myString[4]);    // Returns false because ! is not numeric

`isalnum(c) -- Returns true if c is alphabetic or a numeric digit. Thus, returns true if either isalpha or isdigit would return true.`

isalnum('A');            // Returns true
isalnum(myString[3]);    // Returns true because '9' is numeric

`isspace(c) -- Returns true if character c is a whitespace.`

isspace(myString[5]);    // Returns true because that character is a space ' '.
isspace(myString[0]);    // Returns false because 'H' is not whitespace.

`islower(c) -- Returns true if character c is a lowercase letter a-z.`

islower(myString[0]);    // Returns false because 'H' is not lowercase. 
islower(myString[1]);    // Returns true because 'e' is lowercase.
islower(myString[3]);    // Returns false because '9' is not a lowercase letter.

`isupper(c) -- Returns true if character c is an uppercase letter A-Z.`

isupper(myString[0]);    // Returns true because 'H' is uppercase. 
isupper(myString[1]);    // Returns false because 'e' is not uppercase.
isupper(myString[3]);    // Returns false because '9' is not an uppercase letter.

`isblank(c) -- Returns true if character c is a blank character. Blank characters include spaces and tabs.`

isblank(myString[5]);    // Returns true because that character is a space ' '. 
isblank(myString[0]);    // Returns false because 'H' is not blank.

`isxdigit(c) -- Returns true if c is a hexadecimal digit: 0-9, a-f, A-F.`

isxdigit(myString[3]);  // Returns true because '9' is a hexadecimal digit.
isxdigit(myString[1]);  // Returns true because 'e' is a hexadecimal digit.
isxdigit(myString[6]);  // Returns false because 'G' is not a hexadecimal digit.

`ispunct(c) -- Returns true if c is a punctuation character. Punctuation characters include: !"#$%&'()*+,-./:;<=>?@[\]^_`{|}~`

ispunct(myString[4]);  // Returns true because '!' is a punctuation character. 
ispunct(myString[6]); // Returns false because 'G' is not a punctuation character.

`isprint(c) -- Returns true if c is a printable character. Printable characters include alphanumeric, punctuation, and space characters.`

isprint(myString[0]);    // Returns true because 'H' is a alphabetic. 
isprint(myString[4]);    // Returns true because '!' is punctuation.
isprint(myString[5]);    // Returns true because that character is a space ' '.
isprint('\0');           // Returns false because the null character is not printable

`iscntrl(c) -- Returns true if c is a control character. Control characters are all characters that are not printable.`

iscntrl(myString[0]);    // Returns false because 'H' is a not a control character 
iscntrl(myString[5]);    // Returns false because space is a not a control character
iscntrl('\0');           // Returns true because the null character is a control character

# Character conversion functions

`toupper(c) -- If c is a lowercase alphabetic character (a-z), returns the uppercase version (A-Z). If c is not a lowercase alphabetic character, just returns c.`

letter = toupper(myString[0]);  // Returns 'H' (no change) 
letter = toupper(myString[1]);  // Returns 'E' ('e' converted to 'E') 
letter = toupper(myString[3]);  // Returns '9' (no change) 
letter = toupper(myString[5]);  // Returns ' ' (no change)

`tolower(c) -- If c is an uppercase alphabetic character (A-Z), returns the lowercase version (a-z). If c is not an uppercase alphabetic character, just returns c.`

letter = tolower(myString[0]);  // Returns 'h' ('H' converted to 'h')
letter = tolower(myString[1]);  // Returns 'e' (no change)
letter = tolower(myString[3]);  // Returns '9' (no change) 
letter = tolower(myString[5]);  // Returns ' ' (no change)


###Example Code of Functions in cctype

```C++
#include <iostream>
#include <cctype>
using namespace std;

int main() {
   const int MAX_LEN = 30;      // Max string length
   char userStr[MAX_LEN];       // User defined string
   int i;
   
   // Prompt user to enter string
   cout << "Enter string (<"
   << MAX_LEN << " chars): ";
   cin >> userStr;
   
   cout << "Original: " << userStr << endl;
   
   cout << "isalpha:  ";
   for (i = 0; userStr[i] != '\0'; ++i) {
      if (isalpha(userStr[i])) {
         cout << "Y";
      }
      else {
         cout << "N";
      }
   }
   cout << endl;
   
   cout << "isdigit:  ";
   for (i = 0; userStr[i] != '\0'; ++i) {
      if (isdigit(userStr[i])) {
         cout << "Y";
      }
      else {
         cout << "N";
      }
   }
   cout << endl;
   
   cout << "isupper:  ";
   for (i = 0; userStr[i] != '\0'; ++i) {
      if (isupper(userStr[i])) {
         cout << "Y";
      }
      else {
         cout << "N";
      }
   }
   cout << endl;
   
   for (i = 0; userStr[i] != '\0'; ++i) {
      userStr[i] = toupper(userStr[i]);
   }
   cout << "After toupper: " << userStr << endl;
   
   return 0;
}
----Output----

Enter string (<30 chars): ABC123$!def
Original: ABC123$!def
isalpha:  YYYNNNNNYYY
isdigit:  NNNYYYNNNNN
isupper:  YYYNNNNNNNN
After toupper: ABC123$!DEF

```