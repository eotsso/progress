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

