
# C is easy

## Contents
* [Datatypes](#datatypes)
* [Pointers](#pointers)
* [Arrays](#arrays)
* [Strings](#strings)

## Data types

### Numeric datatypes

Data type itself
* `int`: positive or negative whole number
* `signed int`: the same as int
* `unsigned int`: no sign bit so only for positive whole numbers
* `float` positive or negative fractional numbers

Size modifiers allows to specify how much space is allocated to a number
* `long`: increases the size
* `short`: reduces the size

Example: 

```C 
unsigned short int total=5;
```

### Char datatype

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

This should be read as a pointer to a `const int` (see the [Clockwise rule](http://c-faq.com/decl/spiral.anderson.html)).

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

Real functions using ``const char *``. The ``printf`` or ``puts`` functions in the standard library. Examples taken from `<stdio.h>`.

```C
  int	 printf(const char * __restrict, ...) __printflike(1, 2);
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

## The preprocessor

## Toolbox

### gdb

### Make
All actions, rules etc... are identified by tabs. To make sure that tabs are correctly inserted in the makefile, enter

`cat -e -t -v makefile_name`

on the command line.

``^I`` represents a tab
``$`` represents end of line.

#### Creating a static library


On linux::

   gcc -c xxxx.c -o xxxx.o
   
   ar rcs libxxxx.a xxxx.o
   
   gcc -static main.c -L. lxxxx -o statically_linked
   
Apple MacOs does not support static linking.

#### Creating a dynamic library

On linux `gcc`
   
On MacOs::
```C   
   gcc -dynamiclib -o libxxxx.dylib xxxx.c
```

Verify the library `file libxxxx.dylib`. You should get `libxxxx.dylib: Mach-O 64-bit dynamically linked shared library x86_64
`.
   
Finally, compile your application, link it to your library or libraries execute it `gcc -L. -lxxxx -lyyyy -o mainsl main.c`
and execute it `./mainsl`.
   
## Resources

The technique called "Clockwise/spiral rule" helps to parse any C declaration and can be found [here](http://c-faq.com/decl/spiral.anderson.html).
