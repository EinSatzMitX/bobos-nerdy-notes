#Programming #osdev #unix 

C is a [[Compiled Programming Language]], developped by [[Dennis Ritchie]], the creator of [[Unix]], and it first appeared in 1972
![[Pasted image 20250306134158.png]] 
_Picture of Ken Thompson (left) and [[Dennis Ritchie]] (right)_

The C Programming Language is often used in [[Low Level]] environments, such as [[Operating System]]s or [[Embedded Systems]] because it can be compiled to [[Bare Metal]] and doesn't require any additional software. 
There are a lot of [[Compiler]]s for C but the most common ones are [[GCC]] ([[GNU]] Cross Compiler) and [[Clang]] ([[LLVM]]-based compiler).

```C 
/* main.c */
#include <stdio.h>

int main(int argc, char** argv){
	printf("Hello World!");

	return 0;
}
```
_Small example for a C [[Program]] that prints out "Hello World!"_

Since C is usually not programmed in some fancy [[IDE]] that has a simple button which compiles and runs the [[Source Code]] for the user, one must run the [[Compiler]] command themself:
`gcc -o my_program main.c`

This might work for one simple file but as soon as a project consists of multiple files this will become very annoying. 
Luckily there are a bunch of build systems for C, like [[GNU Make]] or [[CMake]] (which also used [[GNU Make]]).
The [[Source Code]] of a C [[Program]] can either be compiled directly into a [[Executable]] or be compiled into [[Object Code]] and then optionally linked against specific [[Libraries]] to finally be linked to an [[Executable]].
Those [[Libraries]] (Shared objects on [[Unix]] systems and Dynamic-link libraries on [[Windows]]) are simply a form of [[Object Code]] that can be shared between different [[Process]]es to save up space in [[Memory]]. These [[Libraries]] can be linked against using a [[Linker]].
One can also write code in so called [[Header File]]s to use its code in multiple C files at once. Because the [[Compiler]] simply copies the contents of the included file and pastes it into the C file, [[Function]] and [[Variable]] declarations can appear multiple times. To prevent this from happening one can use "Include Guards"

```C
/* foo.h */
#pragma once

void print_hello();
```

```C
/* foo.c */
#include "foo.h"
#include <stdio.h>

void print_hello(){
	printf("Hello, World!");
} 
```

```C
/* main.c */
#include "foo.h"

int main(int argc, char** argv){
	printhello();
	return 0;
}
```

To compile this code one must include the foo.h file
`gcc -Ifoo.h -o my_program main.c foo.c`

C has [[Primitive Data Structures]] like int, float, char, ... but it also gives the option to the programmer to create [[Complex Data Structures]] using [[Struct]]s, [[Union]]s, creating [[Enum]]s, etc.
One important [[Data Structure]] is missing in C however: The [[String]]. This doesn't mean one can't use them, they clearly can as demonstrated in the example above, just not in the same way.
This can be achieved using [[Pointer]]s, one of the most powerful [[Data Structure]]s in all [[Programming Languages]]. 
A [[Pointer]] is marked with an ' * ' character and it can point to a specific [[Variable]], that is stored at an address in [[Memory]].

```C
#include <stdio.h>

int main(int argc, char** argv /* char** is actually a opinter as well, in this case it points to the beginning of an array of char* (strings) */)
{
	/* Create a variable of type integer called "a" with a value of 5 */
	int a = 5;
	/* Create a pointer to an integer called "pA" which holds the address of a as its value */
	int * pA = &a;

	/* prints the value at the address stored in pA to the console in form of an integer (followed by a newline character) */
	printf("%i\n", *pA);

	return 0;
}
```

``` 
[~/tmp/test]$ gcc main.c -o main      
[~/tmp/test]$ ./main
5
[~/tmp/test]$ 
```

As showcased in this example, ' * ' after a [[Data Structure]] indicates that the [[Variable]] will hold a pointer to that [[Data Structure]], although there can be some confusion:
```C
/* The same*/
int * a, b, c;
int *a;
int b;
int c;
```

The ' * ' before a variable can be read as "the value at the address which the variable holds"
The '&' before a variable can be read as "the address of the variable" 

```C
int a = 5;
int * pA = &a;
int b = *pA + 1;
```
`a = 5`
`b = 6`

Just like most other [[Programming Languages]], C also has [[Array]]s starting at 0 (FUCK YOU LUA!!!). They can hold any [[Data Structure]], even other [[Array]]s to create a multi-dimensional [[Array]]. Even though [[Array]]s are a really good [[Data Structure]] and they can be extremely fast when they're stored on the [[Stack]], they are not perfectly suited for every use case because their size needs to be known when declaring them. [[Pointer]]s can also be used to represent an [[Array]].
```C
int array[8]; /* Fixed-size array that can hold 8 integers */
/* Cast the return value of malloc as int* */
int * cooler_array = (int*)malloc(sizeof(int) * 8); /* Also fixed-size array that holds 8 integers BUT it can be reallocated */
cooler_array = (int*)realloc(cooler_array, sizeof(int) * newsize);
```

Back to our problem with the [[String]] not being a standard variable in C, we can actually solve it by using an array
```C
char my_string[10] = "0123456789";
char* cooler_string = "0123456789"; /* The compiler automatically makes space for our array contents */

printf("%i\n", cooler_string[9]);
```
`stdout: 9`

This means that a string, indicated by "", is actually just a char*, or in other words a memory address we can manipulate. This is called [[Pointer Arithmetic]].

```C
#include <stdio.h>

int main(int argc, char** argv)
{
	char* string = "abcdefghij";
	int f = *(string + sizeof(char)*5);

	printf("%c", a);

	return 0;
}
```
_In this example a char* called "string" is created, which points to the string "abcdefghij". When increasing that variable called "string" we're effectively increasing the address it points to, so when whe now print the char it points to by using %c as our specifier we get 'f' as an output_

The Programer can also create a [[Pointer]]


The is also a book Called "The C Programming Language" (often referred to as "K&R" because it was written by Kernighan and [[Dennis Ritchie]]) which is still a relevant book to this day.


