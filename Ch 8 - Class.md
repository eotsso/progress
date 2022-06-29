 In programming, an object is a grouping of data (variables) and operations that can be performed on that data (functions).

Objects strongly support abstraction, hiding entire groups of functions and variables, exposing only certain functions to a user.

 An abstract data type (ADT) is a data type whose creation and update are constrained to specific well-defined operations. A class 
 can be used to implement an ADT.


# Class Introduction

The class construct defines a new type that can group data and functions to form an object. 

A class' public member functions indicate all operations a class user can perform on the object.
```C++
class Restaurant {                          // Info about a restaurant   
   public:                                  // Indicates all operations a class user can perform on object.
      void SetName(string restaurantName);  // Sets the restaurant's name              
      void SetRating(int userRating);       // Sets the rating (1-5, with 5 best)      
      void Print();                         // Prints name and rating on one line   
}

int main() {
// Declaring a variable of class-type "restaurant" creates an object of that type (restaurant)
   Restaurant favLunchPlace;                // Creates a Restaurant-object named favLunchPlace
// Object holds 2 memory spaces; one for SetName() and one for SetRating() as defined in class-restaurant.
   Restaurant favDinnerPlace;               // Creates a Resturant-object named favDinnerPlace

   favLunchPlace.SetName("Central Deli");   // . is a member class operator that calls function on object. 
   favLunchPlace.SetRating(4);              // calls SetRating() f-n on object-favLunchPlace

   favDinnerPlace.SetName("Friends Cafe");
   favDinnerPlace.SetRating(5);

   cout << "My favorite restaurants: " << endl;
   favLunchPlace.Print();
   favDinnerPlace.Print();

   return 0;
}
```

# Class Example: string

An example of a class is C++'s string. The string-class stores a string's character in memory, along with variables indicating length, and other things. But such details are abstracted away. Instead, the user only needs to know what public member functions can be used (shown below).

```C++
char& at(size_t pos); // Returns a reference to the character at position pos in the string.

size_t length() const; // Returns the number of characters in the string

void push_back(char c); // Appends character c to the string's end (increasing length by 1).

// Been using class and member class operators all along. 
// The push_back() function's comment explains that the character parameter will be appended to the string. (How that appending occurs is unknown to the class user).
```

What enables a user to utilize the string class?
`#include <string>`
This directive includes the class definition into a program, allowing a programmer to use the string class. The class uses a lower-level mechanism for storing strings, namely arrays of characters. The class adds numerous functions to ease working with strings, hiding details from the programmer.


# 8.3 Defining a Class

- Private data members can neither be written nor read by a class user; only accessed via member functions. 
```C++
class Restaurant {                          // Keeps a user's review of a restaurant
   public:                                    
      void SetName(string restaurantName);  // Sets the restaurant's name        
      void SetRating(int userRating);       // Sets the rating (1-5, with 5 best)    
      void Print();                         // Prints name and rating on one line 
   private:
      string name;
      int rating;
};

int main () {
	Restaurant favLunchPlace;

	favLuncPlace.rating = 5; // INVALID; can't access private data members directly, only function. 
}

```
## Defining a class' public member function: **scope resolution operator**. 
- Functions must be declared after `public:`
- A **function declaration** must have a `return type`, `function name`, and `parameter type`
- A **function definition** must have `return type`, `function name`, `parameter name + parameter type`, `and function statements`. 
- A **member function definition** has `class name` and `::` known as **scope resolution operator**. 
	- A member function's definition normally appears separate from the class definition, associated with the class using the `::` operator
```C++
class MyClass {
	public: 
		void Fct(); //function declaration 

	private:
		int NumA;
};

void MyClass::Fct1 () { //(::) is known as scope resolution operator, preceding function name. 
	numA = 0; 
}
```

#  8.4 Inline member functions

A member function's definition may appear within the class definition, known as an inline member function. Programmers may inline short function definitions to yield more compact code, keeping longer function definitions outside the class definition to avoid clutter.
- Example of Inline member function (void Fct1())
```C++
class MyClass {
	public: 
		void Fct1() {
		numA = 0
	}
	private: 
		int numA;
};
```
- Example of scope resolution operator: for longer function definitions 
```C++
class MyClass {
   public:
      void Fct1();
   private:
      int numA;
};

void MyClass::Fct1() {
   numA = 0;
}
```

## Exception to variables being declared before used
- Normally, items like variables must be declared before being used, but this rule does not apply within a class definition.
- This rule exception allows a class to have the desired form of a public region at the top and a private region at the bottom: A public inline member function can thus access a private data member even though that private data member is declared after the function.

## Inline member functions on one line
- Normally, good style dictates putting a function's statements below the function's name and indenting. But, many programmers make an exception by putting very-short inline member function statements on the same line, for improved readability.
```C++
 void SetName(string restaurantName) { name = restaurantName; }
 void SetRating(int userRating) { rating = userRating; }
```

# 8.5 Mutators, accessors, and private helpers
- **Mutators** modify a class' data members
- **Accessors** accesses data but does not modify a class' data members. 
	- Good practice is accessor functions have keyword `const` after a member function's name and parameters because the compiler will catch if the function tries to modify a data member. 
		- Const member function calls can only call other const functions. 
```C++
#include <iostream>
#include <string>
using namespace std;

class Restaurant {
   public:
      void   SetName(string restaurantName); // Mutator
      void   SetRating(int userRating);      // Mutator
      string GetName() const;                // Accessor
      int    GetRating() const;              // Accessor
      void   Print() const;                  // Accessor

   private:
      string name;
      int rating;
};

void Restaurant::SetName(string restaurantName) {
   name = restaurantName;
}

void Restaurant::SetRating(int userRating) {
   rating = userRating;
}

string Restaurant::GetName() const {
   return name;
}

int Restaurant::GetRating() const {
   return rating;
}

void Restaurant::Print() const {
   cout << name << " -- " << rating << endl;
}

int main() {
   Restaurant myPlace;

   myPlace.SetName("Maria's Diner");
   myPlace.SetRating(5);

   cout << myPlace.GetName() << " is rated ";
   cout << myPlace.GetRating() << endl;

   return 0;
}
```
- **Private helper functions** are literally just functions that can't be accessed by the user, which are used to help public functions carry out tasks. 
```C++
class MyClass {
   public:
      void Fct1(); 
   private:
      int numA;
      int FctX(); //private function
};

int MyClass::FctX() { //private function 
	...
}
```
# 8.6 Initalization (preferred) and Constructors
- Good practice is to initalize variables when declared. Any variable delcared of that class type will initially have those values.
```C++
#include <iostream>
#include <string>
using namespace std;

class Restaurant {
   public:
      void SetName(string restaurantName);
      void SetRating(int userRating);
      void Print();
   
   private:
      string name = "NoName";  // NoName indicates name was not set      int rating = -1;         // -1 indicates rating was not set
};

void Restaurant::SetName(string restaurantName) {
   name = restaurantName;
}

void Restaurant::SetRating(int userRating) {
   rating = userRating;
}

void Restaurant::Print() {
   cout << name << " -- " << rating << endl;
}

int main() {
   Restaurant favLunchPlace;  // Initializes members with values in class definition
   
   favLunchPlace.Print();

   favLunchPlace.SetName("Central Deli");
   favLunchPlace.SetRating(4);

   favLunchPlace.Print();
   
   return 0;
}
-----OUTPUT-----
NoName -- -1
Central Deli -- 4
```

## Constructors
- *Note: Since C++11, data members can be initialized in the class definition as in `int price = -1;`, which is usually preferred over using a constructor. However, sometimes initializations are more complicated, in which case a constructor is needed.*
- **Constructors** initalize (not allocates) space for an object. The main feature is that an instance is always in a valid state...
	- C++ has a special class member function, a constructor, called _automatically_ when a variable of that class type is declared, and which can initialize data members. A constructor callable without arguments is a default constructor, like the Restaurant constructor below.
	- A constructor has the same name as the class. A constructor function has no return type, not even void. Ex: `Restaurant::Restaurant() {...}` defines a constructor for the Restaurant class.
	- If a class has no explictedly defined constructor, the complier implictedly defines a defautl constructor with no statements. 
```C++
#include <iostream>
#include <string>
using namespace std;

class Restaurant {
   public:
      Restaurant();      void SetName(string restaurantName);
      void SetRating(int userRating);
      void Print();
   private:
      string name;
      int rating;
};

Restaurant::Restaurant() {  // Default constructor
   name = "NoName";         // Default name: NoName indicates name was not set   rating = -1;             // Default rating: -1 indicates rating was not set
}
void Restaurant::SetName(string restaurantName) {
   name = restaurantName;
}

void Restaurant::SetRating(int userRating) {
   rating = userRating;
}

// Prints name and rating on one line
void Restaurant::Print() {
   cout << name << " -- " << rating << endl;
}

int main() {
   Restaurant favLunchPlace;  // Automatically calls the default constructor

   favLunchPlace.Print();

   favLunchPlace.SetName("Central Deli");
   favLunchPlace.SetRating(4);
   favLunchPlace.Print();

   return 0;
----OUTPUT----
NoName -- -1
Central Deli -- 4

```

- T/F: The following calls the default constructor 5 times.
`vector<Seat> seats(5); // true`

### Initalization vs Constructor Example
- Initalization Example
```C++
#include <iostream>
#include <string>
using namespace std;

class Bicycle {
   public:
      void SetType(string bicycleType);
      void SetYear(int bicycleYear);
      void Print();
   private:
      string type = "NoType";  // NoType indicates brand was not set
      int year = -1;           // -1 indicates year was not set
};

void Bicycle::SetType(string bicycleType) {
   type = bicycleType;
}

void Bicycle::SetYear(int bicycleYear) {
   year = bicycleYear;
}

void Bicycle::Print() {
   cout << type << " " << year << endl;
}

int main() {
   Bicycle commuterBike;
   
   commuterBike.Print();
   
   commuterBike.SetType("road");
   commuterBike.SetYear(1922);

   commuterBike.Print();
   
   return 0;
```
- Constructor Example
```C++ 
#include <iostream>
#include <string>
using namespace std;

class Bicycle {
   public:
      Bicycle();
      void SetType(string bicycleType);
      void SetYear(int bicycleYear);
      void Print();
   private:
      string type;
      int year;
};

Bicycle::Bicycle() {
   type = "NoType";    // NoType indicates brand was not set
   year = -1;          // -1 indicates year was not set
}

void Bicycle::SetType(string bicycleType) {
   type = bicycleType;
}

void Bicycle::SetYear(int bicycleYear) {
   year = bicycleYear;
}

void Bicycle::Print() {
   cout << type << " " << year << endl;
}

int main() {
   Bicycle commuterBike;
   
   commuterBike.Print();
   
   commuterBike.SetType("freight");

   commuterBike.Print();
   
   return 0;
}


```


# # 8.7 Classes and vectors/classes 
```C++
#include <iostream>
#include <string>
#include <vector>
using namespace std;

class Review {
   public:
      void SetRatingAndComment(int revRating, string revComment) {
         rating = revRating;
         comment = revComment;
      }
      int GetRating() const { return rating; }
      string GetComment() const { return comment; }

   private:
      int rating = -1;
      string comment = "NoComment";
};

int main() {
   vector<Review> reviewList;
   Review currReview;
   int currRating;
   string currComment;
   unsigned int i;

   cout << "Type rating + comments. To end: -1" << endl;
   cin >> currRating;
   while (currRating >= 0) {
      getline(cin, currComment); // Gets rest of line
      currReview.SetRatingAndComment(currRating, currComment); //uses single currReview
      reviewList.push_back(currReview); //stores the entire class into a vector, effectively creating seperate instances
      cin >> currRating;
   }

   // Output all comments for given rating
   cout << endl << "Type rating. To end: -1" << endl;
   cin >> currRating;
   while (currRating != -1) {
      for (i = 0; i < reviewList.size(); ++i) {
         currReview = reviewList.at(i); //retrives that specific instance class and stores it back into currReview (which is also a Review class)
         if (currRating == currReview.GetRating()) {
            cout << currReview.GetComment() << endl;
         }
      }
      cin >> currRating;
   }

   return 0;
}
----OUTPUT----
Type rating + comments. To end: -1
5 Great place!
5 Loved the food.
2 Pretty bad service.
4 New owners are nice.
2 Yuk!!!
4 What a gem.     
-1

Type rating. To end: -1
5
 Great place!
 Loved the food.
1
4
 New owners are nice.
 What a gem.     
-1
```
- The above, but with a 'reviews' class to manage the vector of Review objects. The Reviews class has a "getter" function returning the average rating. The function computes the average rather than reading a private data member. The class user need not know how the function is implemented.
	- main() declares a variable of type Reviews. Reviews itself has a vector, but main() doesn't declare a vector. In general, main() is simpler, since much of the functionality is now in the Reviews class.
```C++
#include <iostream>
#include <string>
#include <vector>
using namespace std;

class Review {
   public:
      void SetRatingAndComment(int revRating, string revComment) {
         rating = revRating;
         comment = revComment;
      }
      int GetRating() const { return rating; }
      string GetComment() const { return comment; }

   private:
      int rating = -1;
      string comment = "NoComment";
};
// END Review class

class Reviews {
   public:
      void InputReviews();
      void PrintCommentsForRating(int currRating) const;
      int GetAverageRating() const;

   private:
      vector<Review> reviewList; //privated the vector of Review objects
};

// Get rating comment pairs, add each to list. -1 rating ends.
void Reviews::InputReviews() {
   Review currReview;
   int currRating;
   string currComment;

   cin >> currRating;
   while (currRating >= 0) {
      getline(cin, currComment); // Gets rest of line
      currReview.SetRatingAndComment(currRating, currComment);
      reviewList.push_back(currReview);
      cin >> currRating;
   }
}

// Print all comments for reviews having the given rating
void Reviews::PrintCommentsForRating(int currRating) const {
   Review currReview;
   unsigned int i;

   for (i = 0; i < reviewList.size(); ++i) {
      currReview = reviewList.at(i);
      if (currRating == currReview.GetRating()) {
         cout << currReview.GetComment() << endl;
      }
   }
}

int Reviews::GetAverageRating() const {
   int ratingsSum;
   unsigned int i;

   ratingsSum = 0;
   for (i = 0; i < reviewList.size(); ++i) {
      ratingsSum += reviewList.at(i).GetRating();
   }
   return (ratingsSum / reviewList.size());
}
// END Reviews class

int main() {
   Reviews allReviews;
   string currName;
   int currRating;

   cout << "Type ratings + comments. To end: -1" << endl;
   allReviews.InputReviews();

   cout << endl << "Average rating: ";
   cout << allReviews.GetAverageRating() << endl;

   // Output all comments for given rating
   cout << endl << "Type rating. To end: -1" << endl;
   cin >> currRating;
   while (currRating != -1) {
      allReviews.PrintCommentsForRating(currRating);
      cin >> currRating;
   }

   return 0;
}
----OUTPUT----
Type ratings + comments. To end: -1
5 Great place!
5 Loved the food.
2 Pretty bad service.
4 New owners are nice.
2 Yuk!!!
4 What a gem.     
-1

Average rating: 3

Type rating. To end: -1
5
 Great place!
 Loved the food.
1
4
 New owners are nice.
 What a gem.     
-1
```

## Classes within Classes

```C++
#include <iostream>
#include <string>
#include <vector>
using namespace std;

// Review and Reviews classes omitted from figure 
// ...

class Restaurant {
   public:
      void SetName(string restaurantName) {
         name = restaurantName;
      }
      void ReadAllReviews();
      void PrintCommentsByRating() const;

   private:
      string name;
      Reviews reviews;
};

void Restaurant::ReadAllReviews() {
   cout << "Type ratings + comments. To end: -1" << endl;
   reviews.InputReviews();
}

void Restaurant::PrintCommentsByRating() const {
   int i;

   cout << "Comments for each rating level: " << endl;
   for (i = 1; i <= 5; ++i) {
     cout << i << ":" << endl;
     reviews.PrintCommentsForRating(i);
   }
}

int main() {
   Restaurant ourPlace;
   string currName;

   cout << "Type restaurant name: " << endl;
   getline(cin, currName);
   ourPlace.SetName(currName);
   cout << endl;

   ourPlace.ReadAllReviews();
   cout << endl;

   ourPlace.PrintCommentsByRating();

   return 0;
}

```

# 8.8 Seperate files for classes

- **ClassName.h** contains the class definition, including data members and member function declarations.
- **ClassName.cpp** contains member function definitions.
StoreItem.h  (header file)
- You can essentially nest each class into another class; think of it like putting everything into a bigger and bigger box. 
```C++
#ifndef STOREITEM_H
#define STOREITEM_H

class StoreItem {
   public:
      void SetWeightOunces(int ounces);
      void Print() const;
   private:
      int weightOunces;
};

#endif
```

StoreItem.cpp  
```C++
#include <iostream>
using namespace std;

#include "StoreItem.h"
void StoreItem::SetWeightOunces(int ounces) {
   weightOunces = ounces;
}

void StoreItem::Print() const {
   cout << "Weight (ounces): " << weightOunces << endl;
}
```

main.cpp
```C++
#include <iostream>
using namespace std;

#include "StoreItem.h"
int main() {
   StoreItem item1;

   item1.SetWeightOunces(16);
   item1.Print();

   return 0;
}
```

Compliation commands/example (*note that the .h file is not included in the compliation command because it is included by the approcaite .cpp files*)
`% g++ -Wall StoreItem.cpp main.cpp
`% a.out`
`Weight (ounces): 16``

## # [Why are #ifndef and #define used in C++ header files?](https://stackoverflow.com/questions/1653958/why-are-ifndef-and-define-used-in-c-header-files) And at the end of the file is And at the end of the file is `#endif`

Those are called [#include guards](http://en.wikipedia.org/wiki/Include_guard).

Once the header is included, it checks if a unique value (in this case `HEADERFILE_H`) is defined. Then if it's not defined, it defines it and continues to the rest of the page.

When the code is included again, the first `ifndef` fails, resulting in a blank file.

That prevents double declaration of any identifiers such as types, enums and static variables.


# Included Header Files

main.cpp declares objects of both types so also includes both .h files. 

# 8.10 Unit testing (classes)
- Testbench is a program whose job is to thoroughly test another program (or portion) via a series of input/output checks known as test cases. 
- Unit testing means to create and run a testbench for a specific item (or "unit") like a function or a class.

- Features of a good testbench include:
	-   Automatic checks. Ex: Values are compared, as in `testData.GetNum1() != 100`. For conciseness, only fails are printed.
	-   Independent test cases. Ex: The test case for GetAverage() assigns new values, vs. relying on earlier values.
	-   100% code coverage: Every line of code is executed. A good testbench would have more test cases than below.
	-   Includes not just typical values but also border cases: Unusual or extreme test case values like 0, negative numbers, or large numbers.

- Regression testing means to retest an item like a class anytime that item is changed; if previously-passed test cases fail, the item has "regressed".
## Example of Unit Testing

```C++
#include <iostream>
using namespace std;

// Note: This class intentionally has errors

class StatsInfo {
public:
   void SetNum1(int numVal) { num1 = numVal; }
   void SetNum2(int numVal) { num2 = numVal; }
   int GetNum1() const { return num1; }
   int GetNum2() const { return num1; }
   int GetAverage() const;

private:
   int num1;
   int num2;
};

int StatsInfo::GetAverage() const {
   return num1 + num2 / 2;
}
// END StatsInfo class

// TESTBENCH main() for StatsInfo class
int main() {
   StatsInfo testData;

   // Typical testbench tests more thoroughly

   cout << "Beginning tests." << endl;

   // Check set/get num1
   testData.SetNum1(100);
   if (testData.GetNum1() != 100) {
      cout << "   FAILED set/get num1" << endl;
   }

   // Check set/get num2
   testData.SetNum2(50);
   if (testData.GetNum2() != 50) {
      cout << "   FAILED set/get num2" << endl;
   }

   // Check GetAverage()
   testData.SetNum1(10);
   testData.SetNum2(20);
   if (testData.GetAverage() != 15) {
      cout << "   FAILED GetAverage for 10, 20" << endl;
   }

   testData.SetNum1(-10);
   testData.SetNum2(0);
   if (testData.GetAverage() != -5) {
      cout << "   FAILED GetAverage for -10, 0" << endl;
   }

   cout << "Tests complete." << endl;

   return 0;
}

----OUTPUT----
Beginning tests.
   FAILED set/get num2
   FAILED GetAverage for 10, 20
   FAILED GetAverage for -10, 0
Tests complete.
```