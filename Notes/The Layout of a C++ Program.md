	int main() {}
	
The basic start of a C++ program is defining the main function that is always called, the rest of the program goes in the curly braces.

### A Simple Hello to the World

	#include <iostream>
	
	int main()
	{
			std::cout << "Hello, World!\n"
	}

- The ""#include < iostream>" is basically importing the iostream library for use
- "std::cout" declares that what follows is sent to the standard output stream
- "<<" is the equivalent of 'put to'

Note: When initializing a variable in C++, you MUST declare it always, as otherwise the memory is not automatically allocated like other coding languages, ie if you initialise var i and print it without declaring as i = 0, the prev. memory val from i will be printed.

Note: Normally a "using namespace std;" line is included in the declarations so that standard ops can be used without "std::". However, it is recommended you don't import the entire namespace as it pollutes the file, only import the elements you absolutely need and use.

Note: It is common practice to declare functions first at the top of your file before defining further in.

