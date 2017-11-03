
# C is easy

## Contents
* [Introduction](#introduction)
* [Programming in C](#programing-in-c)
* [Datatypes](#datatypes)
* [Operators](#operators)
* [Pointers](#pointers)
* [Arrays](#arrays)
* [Strings](#strings)
* [Structures](#structures)
* [Unions](#unions)
* [Bitmasks](#bitmasks)
* [Resources](#resources)

## Introduction

*No website is as good as a good book. And no good book is as good as a disassembly output*.

This tutorial is intended for people who have a background in programming and more particularly who are familiar with programming in a high-level language. Rather than developing a simple Hello world program and add complexity, we prefer to present how to create real complex program from the start. Therefore, you need to have some basic knowledge of how a language works and how you run it.

Disclaimer: we don't explain or try to explain what is good C code but will focus only on how it works.

## Programming in C

### The basics of a C program
Programming in C necessitates to create one or more *source files* with the extension `*.c` and, optionally, `*.h` header files. Header files are mainly used to group common declarations and to define functions prototype.

Once these files are created, we need to create an executable, like `exe` file on Windows.

For this, a program in C we have to follow 3 mandatory steps:
* preprocessing
* compiling
* linking

### Preprocessing
Each time you type `#` (or `##` in one case) in your code, the preprocessor is activated. In this phase, the all the `#include`, `#define`,... statements are replaced by their implementation.

What is the difference between a `#define MY_VARIABLE 5` and a global variable?

Predefined macros.

Macros are very important to understand e.g. for ellipsis which is based on the `__VA_ARGS__` macro.

### Compiling
This is where the compiler like `gcc` or `clang` comes into play. A file with extension `*.obj` is/are created.

### Linking
This phase is done by another program, the linker. It links your program with external libraries.

## Data types

### Numeric datatypes

#### Types
* `int`: positive or negative whole number. Occupies 2 bytes in memory
* `double`: occupies 8 bytes in memory
* `float` positive or negative fractional numbers

#### Modifiers
Size modifiers allow to specify how much space is allocated to a number
* `long`: increases the size by 2 bytes. A `long int` will the occupy 4 bytes and a `long double` will occupy 10 bytes.
* `short`: reduces the size
* `signed`: positive and negative values
* `unsigned`: positive values only

Example:

```C
unsigned short int total=5;
```

Useful predefined types provided by the standard library `stdint.h` (Typedef are described later but basically a typedef is an alias for an existing datatype). For example the type 'int32_t' defined is `_int32_t.h`is simply an `int`but the advantage of using it is that you know immedialtely that it occupies 32 bits or 4 bytes of memory.

Their usages becomes more obvious if you want to use a 64 bits unsigned integer. Instead of declaring `typedef unsigned long long uint64_t` you can simply use the type defined by `uint64_t`

### Char datatype
ASCII characters occupy 1 byte aka 8 bits (not universal but is usually the case) in memory. All capital letters will begin with `010` in binary. Lower case letter will begin with `011`, hence the 3rd bit is a flag that indicates if the letter is capital or not.

Given a letter, we can make it uppercase or lowercase by just turning on/off the third bit.

Or we can determine if a character is uppercase or lowercase just by looking at the third bit.

Here is the code to represent the binary representation of a character:

```C
char letter = 'A';
int i;
for(i=0; i<8; i++) {
  printf("%d", !!((letter << i) & 0x80));
}
printf("\n");
```
Run this code [here](http://tpcg.io/0gi1wJ).

And here is the code to switch the flag:

```C
//TODO
```

### Typedef
Besides native datatypes, a `typedef`allows to define aliases to existing ones. The syntax is `typedef <datatype> <alias_name>`. Typedefs can be chained, that is to say we can define a typedef on another typedef, as can be seen in the `stdint` library.

## Operators

* Arithmetic Operators
* Relational Operators
* Logical Operators
* Bitwise Operators
* Assignment Operators
* Ternary or Conditional Operators

## Pointers

Pointer to an integer
```C
int *
```

Pointer to a const integer.

```C
int const *
```


A constant pointer to an integer.

```C
int * const
```

A very useful technique to read (understand) that kind of declaration is the so-called [Clockwise/Spiral Rule](http://c-faq.com/decl/spiral.anderson.html) by David Anderson.

Example program:

```C
  int var=10;
  int * const ptr = &var; // being constant, ptr is initialized here
  printf("Value of var is %d\n",var);
  printf("Value of ptr is %d\n",*ptr);
  //*ptr=20; would generates compile time error because it is a read-only pointer
  var=20;
  printf("New value of var is %d\n",var);
  printf("New value of ptr is %d\n",*ptr);
```

The `ptr` itself is constant and cannot be changed.

```C
   int *const ptr
```

This should be read as a constant pointer of type char.

Example program:

```C
  char var1='A';
  char var2='B';
  char *const ptr=&var1;
  ptr=&var2; // Generates compile time error because ptr1 is declared constant and cannot be reassigned
```

Constant pointer to a constant integer

```C
int const * const
```

Real functions using a pointer to a constant character (``const char *``). Examples taken from `<stdio.h>`:

```C
int	 puts(const char  *);
```

## Arrays
To create an array, choose the type of the elements stored in the array, choose the size (optional), and stor the data in the array:

```C
   char str_a[20];
```

or:

```C
  char str_a[]="abc123"; //The size of the array is optional
```

or:

```C
  char str_a[7]="abc123"; //Don't forget the \0 last character
```

Why arrays can be dangerous...

How to declare an array in C99::

```C
#define MAX_SIZE n
int array[MAX_SIZE];
```

## Strings

In C, strings are arrays of characters. A pointer stores the memory address of the first element of the array: ``char *ptr = "Hello, World!"``. As seen in the previous section, the elements of an array occupy contiguous blocks of memory.

The difference between:

```C  
   char str_a[7]="abc123"; //Read Write memory
```
and:

```C
char *p_str = "abc123"; //Read memory
```

is that in the later case, we work with a string constant that cannot be changed. In the first case, we have an array of character variables; therefore we can change the content.   

## Command-line parameters

Let's explain ``int argc`` and ``char const *argv[]``...


## Structures

## Unions

## Bitmasks

## The preprocessor

## Toolbox
A list of mandatory and useful tools to use in C programming.
### gcc

### gdb

### gcov

### gprof

### Make
All actions, rules etc... are identified by tabs. To make sure that tabs are correctly inserted in the makefile, enter

`cat -e -t -v makefile_name`

on the command line.

``^I`` represents a tab
``$`` represents end of line.

## Creating libraries
#### Static library
On linux::
```C
gcc -c xxxx.c -o xxxx.o
ar rcs libxxxx.a xxxx.o   
gcc -static main.c -L. lxxxx -o statically_linked
```
Apple MacOs does not support static linking.

#### Dynamic library

On linux `gcc`
  
On MacOs::
```C  
   gcc -dynamiclib -o libxxxx.dylib xxxx.c
```

Verify the library `file libxxxx.dylib`. You should get something like `libxxxx.dylib: Mach-O 64-bit dynamically linked shared library x86_64
`.

Finally, compile your application, link it to your library or libraries execute it `gcc -L. -lxxxx -lyyyy -o mainsl main.c`
and execute it `./mainsl`.
  
## Resources

### C online
Compile and execute C code online at [Codingground](https://www.tutorialspoint.com/compile_c_online.php).

### Some great C code

### The Clockwise/Spiral rule
The technique called "Clockwise/spiral rule" helps to parse any C declaration and can be found [here](http://c-faq.com/decl/spiral.anderson.html).
