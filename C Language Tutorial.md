#Programming 
**Tutorial for the [[C]]/[[C++]] [[Programming Languages]]**

The [[C]] is used for almost every application on every device, thus it it is probably a smart idea to learn it.

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
typedef struct foo{
	void(*bar)(void);
} foo;

int main(){
	foo foobar;
	foobar.bar();

	/* This is an example that is more common in C */
	foo *foobar = malloc(sizeof(foo));
	

	return 0;
}
```
_This is exactly the same as the pseudo code example before. Note how we use '->' instead of '.' because_
