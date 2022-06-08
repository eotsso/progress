### Reversing a List 
- If you have studied arrays or vectors (or other kinds of lists), know that most swaps are actually performed between two list elements. For example, reversing a list with N elements can be achieved by swapping element 1 and N, element 2 and N-1, element 3 and N-2, etc. (stopping at the middle of the list).


### Figure 7.10.4: Vector reversal program with correct output.  
Be aware of the following:
	1. Store the element in a temporary variable
		 ```tmpValue = revVctr.at(i);```
	2. Be mindful of 'out of range'
		```revVctr.at(i) = revVctr.at(revVctr.size() - 1 - i);```
	3. Remember to swap *odd* numbered lists with: 
		```for (i = 0; i < (revVctr.size() / 2); ++i) ```
			(Not sure what to do with even-numbered lists
```C++
Figure 7.10.4: Vector reversal program with correct output.

#include <iostream>
#include <vector>
using namespace std;

int main() {
   const int NUM_ELEMENTS = 8;        // Number of elements
   vector<int> revVctr(NUM_ELEMENTS); // User values
   unsigned int i;                    // Loop index
   int tmpValue;                      // Placeholder
   
   cout << "Enter " << NUM_ELEMENTS << " integer values..." << endl;
   for (i = 0; i < revVctr.size(); ++i) {
      cout << "Value: ";
      cin >> revVctr.at(i);
   }
   
   // Reverse
   for (i = 0; i < (revVctr.size() / 2); ++i) {      
	  tmpValue = revVctr.at(i);  // These 3 statements swap
      revVctr.at(i) = revVctr.at(revVctr.size() - 1 - i);
      revVctr.at(revVctr.size() - 1 - i) = tmpValue;
   }
   
   // Print values
   cout << endl << "New values: ";
   for (i = 0; i < revVctr.size(); ++i) {
      cout << " " << revVctr.at(i);
   }
   cout << endl;
   
   return 0;
}

```

### Why are vectors preferred over arrays?
- Vectors are safer because the access v.at(i) is checked during execution to ensure the index is within the vector's valid range. An array access a[i] involves no such check. Such checking is important; trying to access an array with an out-of-range index is a very common error, and one of the hardest errors to debug.
	- Assigning with an out-of-range index can mysteriously change some other variable's value. Debugging such an error can be a nightmare.
- Advantages of vectors also include: 
	- resizing during runtime 
	- easy insertion of items front or rear 
	- vector size determination (arrays do not have a .size() function feature)

### Brackets [] vs. Paratheses ()
- You're able to use brackets with both vectors and arrays.
	- However, brackets will not range check in the compiler, which may cause another important memory location to be overwritten when accessed out of range. 