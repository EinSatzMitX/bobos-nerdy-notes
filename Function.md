#Programming 
A function in terms of [[Programming Languages]] is reusable [[Source Code]], e.g. code that can be run with multiple parameters and will achieve mostly the same results, as long a variable is not an edge case.
In [[Mathematics]] for example, one can create a function $f$, so that $f(x) = x²$ . In [[C]] for example this could be represented as:
```C
float f(float x){
	return x*x;
}
```
where x can be a [[Float]] (any approximation of any real number).
Functions can have return types, like in the example above, or they can only consist of code that has to be run multiple times in a [[Program]]. This is usually marked with the keyword "void"
```C
#include <stdio.h>
void foo(void){
	printf("Hi!\n");
}
```

Functions are often confused with [[Method]]s, which are a similar concept from the field of [[OOP]].
In some [[Programming Languages]], like [[C]], the programmer can also create [[Pointer]]s to functions. This feature has very limited use cases, but it can can be very useful sometimes, especially due to the fact that [[C]] is not [[OOP]] Language.