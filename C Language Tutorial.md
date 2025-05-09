#Programming 
**Tutorial for the [[C]]/[[C++]] [[Programming Languages]]**

The [[C]] is used for almost every application on every device, thus it it is probably a smart idea to learn it. The language is pretty old though and thus has a lot of different compilers, which requires it to have standards, which define specific rules and behaviors of the [[Compiler]]s.
Here is a list of all official C standards

| Year                                         | Informal name           | Official standard                   |
| -------------------------------------------- | ----------------------- | ----------------------------------- |
| 1972                                         | first release           | -                                   |
| 1978                                         | K&R C                   | -                                   |
| 1989, 1990                                   | ANSI C, C89, ISO C, C90 | ANSI X3.159-1989  ISO/IEC 9899:1990 |
| 1999                                         | C99, C9X, "modern C"    | ISO/IEC 9899:1999                   |
| 2011                                         | C11, C1X                | ISO/IEC 9899:2011                   |
| 2018                                         | C17, C18                | ISO/IEC 9899:2018                   |
| 2024                                         | C23, C2X, "latest C"    | ISO/IEC 9899:2024                   |
| <abbr title="To be announced">TBA</abbr><br> | C2Y                     | ...                                 |

# **Basics**
## Primitive types (a.k.a. Variables)
In [[Programming Languages]], there are [[Variable]]s. You can think of these variables as drawers, which can hold some combination of bits. These [[Variable]]s are stored in [[Memory]] and have an address and size.
Just like most [[Programming Languages]], [[C]] has different kinds of [[Variable]] types, or to what this chapter is talking about: [[Primitive Data Structures]], such as
```C
/* Added in C23 */
bool b; /* 1 Byte of storage, can hold values from 0 to 255 */

char c; /* 1 Byte of storage */
signed char sc; /* 1 Byte of storage, holds values from -128 to 127 */
unsigned char uc; /* 1 Byte of storage, holds values from 0 to 255; usually used when dealing with characters or inputs from devices */

/* short signed integers, varying in size but usually 16 bits or [-32768; 32767] */
short sh;
short int shi;
signed short ssh;
signed short int sshi;

/* short, unsigned integers, varying in size but usually 16 bits or [0; 65535] */
unsigned short ush;
unsigned short int ushi;

/* Basic signed integer types, usually 32 bits [-2^31; 2^31 -1] */
int i;
signed s;
signed int si;

/* Basic unsigned integer types, usually 32 bits [0; 2^32 -1] */
unsigned u;
unsigned int ui;

/* Long signed integer types, usually 64 bits [-2^63; 2^63 - 1] */
long l;
long int li;
signed long sl;
signed long int sli;

/* Long unsigned integer types, usually 64 bits [0; 2^64 - 1] */
unsigned long ul;
unsigned long int uli;

/* Long long signed integer types, usually 64 bits or more */
long long ll;
long long int lli;
signed long long sll;
signed long long int slli;

/* Long long unsigned integer types, usually 64 bits or more */
unsigned long long ull;
unsigned long long int ulli;

/* Real floating-point type, usually referred to as a single-precision floating-point type. Actual properties unspecified (except minimum limits); however, on most systems, this is the IEEE 754 single-precision binary floating-point format(32 bits). This format is required by the optional Annex F "IEC 60559 floating-point arithmetic". */
/* So in simple words, it can represent (an approximation of) any real number*/
float f;

/* double precision floating point type, usually 64 bits */
double d;

/* extended precision floating point type, usually 64 or 128 bits */
long double ld;

```

As some may have noticed, there are no [[String]]s in [[C]] by default, however this does not mean you can't handle blocks of text. String are represented with something called [[Pointer]]s, but more about that later.


Basic examples of using those types:
```C
char c1 = 'a';
char c2 = c1 + 1;
// c2 == 'b'

short s1 = 13;
short s2 = s1 / 4;
// s2 will be floored to the next integer, in this case 3

float f1 = 13.0f // floats are usually indicated with an f at the end, to make the work for the compiler easier
float f2 = f1 / 4.0f;
// f2 = 3.250000

```

As a sum-up to the [[Primitive Data Structures]], we will run this block of code:
```C
#include <stdio.h>

int main(int argc, char** argv){
	int i1 = 1-5; // -4
	printf("%i\n", i1);

	float f1 = 13.0f / 4.0f; // 3.25
	printf("%f\n", f1);

	// return 0 to indicate or program exited successfully
	return 0;
}
```

To be able to run this code, we need to invoke or [[Compiler]], for simplicity sake, let's just run [[GCC]] with these arguments and then execute our [[Program]]:
`gcc -c main.c -o program`
_Supposing your C file was called main.c_
`./program`

We should get an output like this: 
```
[~]$ ./test
-4
3.250000
```



## [[Struct]]s
We can use our already gained knowledge to combine these various data types in so called [[Struct]]s. A structure is simply a collection of various data types, which are the "fields" of a structure. 

```C
struct person {
	char name[20];
	int age;
	int height;
};
```
_Example of a struct called "person"_

To create a variable of this new type, we can use multiple methods, but the first one is the most common

```C
struct person Person = {
	.name = "Albert Einstein     ",
	.age = 76,
	.height = 172,
};
```
_This only works for C99 and higher_

In the older days, it was the Programmers job to make sure all fields of a struct were in order at initialization, but since most things can be compiled with "modern C", this will not be a problem.

```C
struct person Person = {
	"Albert Einstein     ",
	76,
	172,
};
```
_Example for older standards of C_

## Type Casting 
This isn't really worth creating a new chapter, but you should still know about it: Type casting.
You have now learned about some basic types of the C Programming Language, but especially when dealing with pointers,  you're going to do a lot of type conversions.
```C
#include <stdio.h>

int main(int argc, char** argv){
	int a = 5;
	long b = 6;
	float = c = 5.5f;

	printf("%f", a+b+c);

	return 0;
}
```
_Example on how NOT to do it_
```terminal
[~]$ gcc test.c -o test                                                        
test.c: In function ‘main’:
test.c:6:16: error: expected identifier or ‘(’ before ‘=’ token
    6 |         double = c = 5.5f;
      |                ^
test.c:8:26: error: ‘c’ undeclared (first use in this function)
    8 |         printf("%i", a+b+c);
      |                          ^
test.c:8:26: note: each undeclared identifier is reported only once for each function it appears in
```
_Compiler complains because the types are incorrect_

This code makes absolute sense, we're adding numbers with numbers and printing them to the console, but not all number variable types are the same. Floats and integers can't directly by added together, we have to cast them to another type first.
We can do this by writing the new variable type in front of the variable we want to convert.
```C
#include <stdio.h>

int main(int argc, char** argv){
	int a = 5;
	long b = 6;
	float c = 5.5f;

	printf("%f", (float)a+(double)b+c);

	return 0;
}
```
_Corrected version using type casts_
```terminal
[~]$ gcc test.c -o test                                                        
[~]$ ./test                                                                    
16.500000
```
_The program now successfully compiles and runs!_

## Pointers
One of the most challenging concepts for most beginners are pointers. But they're actually not even so hard to understand, if you know the syntax

A [[Pointer]] is marked with an ' * ' character and it can point to a specific [[Variable]], that is stored at an address in [[Memory]].
The ' * ' character in front of a pointer variable means that, the variable is "dereferenced", which means  the values at the address stored in that pointer is being used.
The '&' ("Ampersand") character in front of a variable takes the address of that variable, so this can be used to create a pointer (as shown in the example below).

```C
#include <stdio.h>

int main(int argc, char** argv /* char** is actually a pointer as well, in this case it points to the beginning of an array of char* (strings) */)
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


## Arrays and Pointers
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
_In this example a char* called "string" is created, which points to the string "abcdefghij". When increasing that variable called "string" we're effectively increasing the address it points to, so when we now print the char it points to by using %c as our specifier we get 'f' as an output_

The Programmer can also create a [[Pointer]] to an [[Array]].
```C
/* Pointer of a 10 elements large integer array */
int (*ptr)[10];
/* Array of 10 pointers to integers */
int *ptr[10];
```
_Example of how easily to confuse different pointer arrays with array pointers_

## Function Pointers
If you know some [[OOP]], this will probably be a bit easier for you, but if not that's still okay.
We have already discussed Pointers by now, but all of them were pointers to specific [[Data Structure]]s.
We now want to step it up by creating pointers to actual code!

```Pseudo-code
class foo{
	void bar();
}

int main(){
	foo foobar;
	foobar.bar();
	
	return 0;
}
```
_This is an example in pseudo code, of how you can creates classes and "methods" in [[OOP]] languages_

In this example we create a class "foo" with a [[Method]] "bar" and then run that method for a variable called "foobar" of this type "foo".

There are no classes in C, so how do we do things there?
Well, it's actually kind of similar, but instead of [[Method]]s, we use [[Function Pointer]]s.

```C
#include <stdlib.h>

typedef struct foo{
	void(*bar)(void);
} foo;

int main(){
	foo foobar;
	foobar.bar();

	/* This is an example that is more common in C */
	foo *foobar2 = malloc(sizeof(foo));
	foobar2->bar();

	return 0;
}
```
_This is exactly the same as the pseudo code example before. Note how we use '->' instead of '.' because foobar2 is a pointer and to run the function we have to run whatever code stands at the address of foobar2 + the offset for the funtion bar_

Now this actually gives us a Segfault, because both foobar and foobar2 haven't initialized their functions yet. So in this code example we try to run the code that stands at the address of foobar2->bar. This is mostly just NULL, but it can be virtually anything, theoretically it could be actual code that hasn't been cleaned up by the OS and that leads to what we call "[[Undefined Behaviour]]". That is why the OS gives us a segmentation fault, not because it hates us and doesn't want to let us run the code, but because it wants to protect us from what might happen when the code would continue.

```C
#include <stdio.h>
#include <stdlib.h>

void bar1(){
  printf("This is the bar function from foobar!\n");
}

void bar2(){
  printf("This is the bar function from foobar2!\n");
}

typedef struct foo{
	void(*bar)(void);
} foo;

int main(){
	foo foobar;
  foobar.bar = bar1;
	foobar.bar();

	/* This is an example that is more common in C */
	foo *foobar2 = malloc(sizeof(foo));
  foobar2->bar = bar2;
	foobar2->bar();

	return 0;
}
```
_Corrected from the example above_

```terminal
[~]$ gcc test.c -o test                                                                                                                                               
[~]$ ./test                                                                                                                                                           
This is the bar function from foobar!
This is the bar function from foobar2!
```
_In the output you can see that it works now! :D_

## TODO:
	- Unions
	- Enums

## Memory management
I haven't really talked about the most important topic of the C Programming Language: Managing [[Memory]]. 
This is easier said than done, especially in C, a language without a [[Garbage Collector]]. Here, the memory management relies completely on you, the programmer.

To know more about Memory management, you have to know what a [[Stack]] and a [[Heap]] are.
The core concept of a [[Stack]] is, that you can put stuff at the "top" of the stack and you can only take (or "pop") the item on the top. You can imagine it like a stack of paper sheets.
The stack is extremely fast, compared to the [[Heap]], but the heap is still necessary for dynamically allocating memory. 
Take a video game as an example, where there are a number of entities. You can create an array of entities, but allocating the space for all of them right at the start of the program would be stupid, especially if the entity struct holds something like an array for the name as a field, because you often don't even need to use all of them. So instead you allocate the entities all individually on the [[Heap]]. The heap is just a fixed region of [[Memory]], which stores all kinds of (writable) data. In contrast to the stack, the heap doesn't require the data to be in a specific order and in can even be scattered across multiple pages (read: [[Paging]]).

```C
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct entity{
	char name[64];
	
	void (*update)(float);

	int health;
} entity;

void update1(float dt){
	printf("[Update1]: Delta time: %f\n", dt);
}

void update2(float dt){
	printf("[Update2]: Delta time: %f\n", dt);
}

int main(int argc, char** argv){
  /* ---- Stack example ---- */
	/* ALOT of unnecessary allocations and wasted memory space */
	entity stack_array[100];
	entity stack_entity = {
    .name = "",
		.update = update1,
		.health = 100,
	};
  /* Copy the string into to the character array of the entity */
  strcpy(stack_entity.name, "Stack Entity");
  /* Make an entry for stack_entity */
	stack_array[0] = stack_entity;

	// 99 entities allocated for no reason...
	printf("Wasted space on the stack: %zu\n", 99*sizeof(entity));


  /* ---- Heap example ---- */
	entity** heap_array = (entity**)malloc(sizeof(entity*)); /* Cast the output of malloc() from a void* to an entity** (this is not necessary, but I'm still doing it for demonstration purposes) */
	entity* heap_entity = (entity*)malloc(sizeof(entity));

  /* Set the fields of the heap entity */
  heap_entity->update = update2;
  heap_entity->health = 50;
  snprintf(heap_entity->name, 64, "Heap entity");

	heap_array[0] = heap_entity;
	/* Way less space wasted */
	printf("Wasted space on the stack (yes stack, not heap): %zu\n", 99*sizeof(entity*));



  stack_array[0].update(0.016f);
  heap_array[0]->update(0.016f);

  /* ---- DON'T FORGET TO FREE EVERYTHING THAT WAS ALLOCATED ON THE HEAP, AS THIS CAN LEAD TO MEMORY CORRUPTION BUGS ---- */
  free(heap_entity);
  free(heap_array);
  /* It is also smart to set the pointers to NULL, so that you can't try to use the addresses anymore (This has caused 9.x exploit in browsers not too long ago) */
  heap_entity = NULL;
  heap_array = NULL;

	return 0;
}
```
_Don't worry about all the string functions starting with "str", you'll learn how to use them after some time, and if not, you can always just look them up_
Now I know, there is a lot going on here, but when breaking it down, it's actually quite simple.
At first we define the entity struct and the two update functions.
In main, we create an array of entities on the stack and then create one entity that we will enter into the array, the rest is left empty.
Note that filling in the fields of the entity variable wasn't necessary for this example.

When finished with the stack version of the array, we start allocating the space for 100 entity pointers in the heap and then we allocate space for one entity on the heap as well.
Note that entity** is an array of entity*. After all, it is just a pointer, which points to the first entity in an array of entity pointers (Let that sink in for a second).

After using all the heap data, make sure to free it, as not doing so will lead to [[Memory Corruption]] and, who guessed it, [[Undefined Behaviour]].
It is also recommended to set all pointers to heap data to NULL after freeing them, because using them will lead to "Use-after-free" [[Bug]]s, which can ALSO lead to serious security issues and [[Undefined Behaviour]].

```terminal
[~]$ gcc test.c -o test                                                                                                                                               
[~]$ ./test                                                                                                                                                           
Wasted space on the stack: 7920
Wasted space on the stack (yes stack, not heap): 792
[Update1]: Delta time: 0.016000
[Update2]: Delta time: 0.016000
```
_Using the heap used 90% less space than using the stack, note that sizes may vary on different machines_

# Intermediate Topics
## TODO:
	- Building tools (Make, clang/gcc, linkers, ...)
	- Preprocessor and compiler control (partly) (e.g. #define, #pragma, ...)
	- storage classes (auto, static, ..) and type qualifiers (const, volatile, restrict)
	- "Variadic" Functions (stdarg.h, va_lsit, va_start, ...)
	- Inline functions vs. macros 
		- Inline assembly
	- setjmp/longjmp for error handling
	- stdlib I/O
	- Low Level I/O
	- Error Handling (errno, perror, assert.h)
	- Debugging with gdb

## Building tools and Project organization
Writing  C code is nice, but it won't do much without compiling, linking and executing your code. This section talks about how to do these things and briefly explains what is going on behind the hood.

When you write a 50 line program, you won't have much trouble putting it all in the main.c file and compiling it using `gcc main.c -o main`. But this doesn't really scale well with programs, that are thousands of lines in size. So, to give your project some organization, you can split your program into multiple files.
Take this program as an example:
```C
// main.c
#include <stdio.h>

void print_hello(){
	printf("Hello!\n");
}

int main(int argc, char** argv){
	print_hello();

	return 0;
}
```
_This is a pretty simplified program, but you can still see, that it is not necessary to have the print_hello function in the main file_

We can split this code into multiple files like this:
```C
// print_hello.h

/* ALWAYS put this on top of your header files, otherwise the compile will complain a lot */
#pragma once

/* Declare the function */
void print_hello();
```
_This is a header file, it is used to declare functions, extern variables and structs_

```C
// print_hello.c
#include <stdio.h>

void print_hello(){
	printf("Hello!\n");
}
```
_Define the functions code in the corresponding C file_

```C
//main.c

/* It is common to distinguish your own header files from extern libraries by using "" for your files and <> for libraries */
#include "print_hello.h"

int main(int argc, char** argv){
	print_hello();

	return 0;
}
```
_Finally put everything together in your main file_

Now to compile this, you'll have to do a bit more:
```terminal
[~/test]$ gcc main.c print_hello.c -I. -o main 
[~/test]$ ./main                                                                                                                                                  
Hello!
```
_Example on how to compile the new project_

As before, we are compiling the C files first, but then we use the -I flag to include directories, containing [[Header File]]s we want to use (in this case all files are in the same directory, in which we're invoking the compiler, so -I. tells the compiler to include the current directory) and finally, we use -o to specify the name of the linked output file. 

But again, that doesn't really scale well, so what better ways are here to build a C project?
Well, luckily there's [[GNU Make]]. A really powerful with a syntax that you might have to wrap your head around, but it won't take too long to understand the basics.



# Advanced Topics
	- Concurrency, Threads, Processes, Signals, ...
	- Optimization (gprof, perf)
	- Portability stuff