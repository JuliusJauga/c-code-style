# C code style
This document describes C code style implemented by Julius Jauga in his projects.
## Table of contents
- [General rules](#general-rules)
- [Variables](#variables)
- [Functions](#functions)
- [Comments](#comments)
### General rules
Here are the general syntax rules for this code style
- Do not use tabs, use spaces instead
- Use 4 spaces per indent level
- Use 1 space between keyword and opening bracket
- Use English names/text for functions, variables, comments
```c
// Correct
if (condition)
while (condition)
for (init; condition; step)
do {} while (condition)

// Wrong
if(condition)
while(condition)
for(init;condition;step)
do {} while(condition)
```
- Do not use space between function name and opening bracket
```c
int a = sum(4, 3);              // Correct
int a = sum (4, 3);             // Wrong
```
- Opening curly bracket is always at the same line as keyword.
```c
char a,b; // Correct
int my_variable; // Correct

char MYVARIABLE; // Wrong, uppercase letters and two words

for (int i = 0; i < 10; ++i) {           // Correct
}
for (int i = 0; i < 10; ++i){            // Wrong
}
for (int i = 0; i < 10; ++i)             // Wrong
{
}
```
- Use single space before and after comparison and assignment operators
```c
int sum;
sum = 2 + 2;              // Correct
for (int i = 0; i < 5; ++i) // Correct
sum=2+2;                  // Wrong
sum = 2+2;                // Wrong
for (sum=0;sum<5;++sum)       // Wrong
```
- Use single space after every comma
```c
my_function(1, 3);        // Correct
my_function(2,2);         // Wrong
```
### Variables
- Use only lowercase characters for variables with optional underscore '_' char
- Declare all local variables of the same type in the same line
```c
    //1. // Correct
    int a,b;
    
    //2. //Wrong
    int a;
    int b;
```
- Declare variables in order
    I. Custom structures, pointers.
    II. Integer types (int, long, short, char...)
    III. Single, double floating point numbers.
```c
// 1.
my_struct x,y,z;
char* x;
int *
// 2.
int a;
long b;
short c;
char k;
...
// 3.
double num;
float num;
```
- Always declare local variables at the beginning of the block, before first executable statement
```c
// Correct
int a,b = 5;
for (a = 0; a < 10; ++a) {
	if (...) {
		break;
	}
}
if (a < b) {
	...
}

// Wrong
int a;
for (a = 0; a < 10; ++a) {
	if (...) {
		break;
	}
}
int b = 5;
if (a < b) {
	...
}
```
- You may declare new variables inside next indent level
```c
int a, b;
a = func();
if (a) {
    int c, d;   // Correct, c and d are in if-statement scope
    c = func();
    int e;      // Wrong, there was already variable declaration of same type in the block
}
```
- Declare counter variables in for loop
```c
// Correct
for (int i = 0; i < 10; ++i)

// Correct, if you need the counter variable
int i;
for (i = 0; i < 10; ++i) {
    if (...) {
        break;
    }
}
if (i == 10) {

}

// Wrong
int i;
for (i = 0; i < 10; ++i) ...
```
- Declare pointer variables with asterisk aligned to type
```c
// Correct
int* a;

// Wrong
int *a;
```
- When declaring multiple pointer variables, you may declare them with asterisk aligned to variable name
```c
// Correct
int *p, *n;
```
- Always use pre-increment (and decrement respectively) instead of post-increment (and decrement respectively)
```c
a++;            // Wrong
++a;            // Correct
```
- Always use size_t for length or size variables
- Always use const for function parameter or variable, if it should not be modified
```c
// Correct
void my_function(const size_t length) {

}

// Wrong
void void my_function(int length) {

}
```
- Always use brackets with sizeof operator
- Never use Variable Length Array (VLA). Use dynamic memory allocation instead with standard C malloc and free functions
```c
// Correct
#include <stdlib.h>
void my_function(size_t size) {
    int* arr;
    arr = (int*)malloc(sizeof(*arr) * n); // Correct, allocate memory
    arr = (int*)malloc(sizeof *arr * n);  // Wrong, brackets for sizeof operator are missing

    free(arr); // Free memory after use
}

// Wrong
void my_function(size_t size) {
    int arr[size];  // Wrong
}
```
### Functions
- Use only lowercase characters for functions with optional underscore '_' char
- Every function must include its declaration, prototype
- When function returns pointer, align asterisk to return type
```c
// Correct;
int* myfunction(void);

int main(void) {
}

int* myfunction(void) {
	// Something
}

// Wrong 
int *myfunction(void) {
	// Something
}
int main(void) {
}
```
### Comments
- Comments can start with // if it's one line, use /* */ for multiple lines
```c
// Correct

// My comment.

/* This
   is
   a multiple
   line
   comment
*/

// Wrong

// This
// is
// a multiple
// line
// comment
```
- Comments have to be aligned
```c
if (a) {			// Starting condition
	for (int i = 0; i < 10; ++i) {
		if (...) {
			break;	// This breaks the loop.
		}
		else {
			...		// This does something.
		}
	}
}
```
