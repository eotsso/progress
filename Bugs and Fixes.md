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
