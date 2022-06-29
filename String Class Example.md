
```C++

``
#include <iostream>
#include <string>
using namespace std;

class Book {
   public:
      void SetTitle(string bookTitle) { title = bookTitle; }
      void SetPublisher(string bookPublisher) { publisher = bookPublisher; }
      void Print() const {
         cout << title << " by " << publisher << endl;
      }

   private:
      string title;
      string publisher;
};

int main() {
   Book myBook;

   myBook.SetTitle("Blackcollar");
   myBook.SetPublisher("Open Road Media");

   myBook.Print();

   return 0;