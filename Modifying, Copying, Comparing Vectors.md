
```C++
7.8 Loop-modifying or copying/comparing vectors

   // Convert negatives to 0
   for (i = 0; i < userVals.size(); ++i) {
      if (userVals.at(i) < 0) {
         userVals.at(i) = 0;
      }
   }
```


### Element by element vector copy

In C++, the = operator conveniently performs an element-by-element copy of a vector, called a vector copy operation. The operation vectorB = vectorA ***resizes vectorB to vectorA's size***, appending or deleting elements as needed. vectorB commonly has a size of 0 before the operation.

```C++

Figure 7.8.2: Using = to copy a vector: Original and sale prices.

#include <iostream>
#include <vector>
using namespace std;

int main() {
   const int   NUM_ELEMENTS = 4;         // Number of elements
   vector<int> origPrices(NUM_ELEMENTS); // Original prices
   vector<int> salePrices(NUM_ELEMENTS); // Sale prices
   unsigned int i;                       // Loop index
   
   // Assign original prices
   origPrices.at(0) = 10;
   origPrices.at(1) = 20;
   origPrices.at(2) = 30;
   origPrices.at(3) = 40;
   
   // Copy original prices to sales prices
   salePrices = origPrices;   
   // Update salePrices. Note: does not affect origPrices
   salePrices.at(2) = 27;
   salePrices.at(3) = 35;
   
   // Output original and sale prices
   cout << "Original prices: ";
   for (i = 0; i < origPrices.size(); ++i) {
      cout << " " << origPrices.at(i);
   }
   cout << endl;
   
   cout << "Sale prices:     ";
   for (i = 0; i < salePrices.size(); ++i) {
      cout << " " << salePrices.at(i);
   }
   cout << endl;
   
   return 0;
}

----------------
Original prices:  10 20 30 40
Sale prices:      10 20 27 35
```


### Element by element vector comparison

In C++, the == operator conveniently compares vectors element-by-element, called a vector equality operation, with vectorA == vectorB evaluating to true if the ***vectors are the same size AND each element pair is equal.***