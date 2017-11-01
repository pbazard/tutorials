
# C is easy

## Pointers

The location pointed by `ptr` cannot be changed or the value pointed at is cannot be changed **by** this pointer. It can be viewed as a read-only pointer.

```
   const char *ptr
```   

This should be read as `const char *pointer` (see Clock, **BUT** the value pointed at is **NOT** itself a constant; it can be changed by another pointer for example. One use case could be to provide access to a file, for example, in read-only mode for a certain type of users and in read-write mode for the owner of the file.

Example program::

```
  char var1='A';
  printf("%c\n",var1);
  const char *ptr1 = &var1;
  char *ptr2 = &var1;
  //*ptr1='C'; //generates compile time error because ptr1 is a read-only pointer
  *ptr2='C'; //ptr2 can change the value of var1 from 'A' to 'C'
  printf("%c\n",var1);
```

The `ptr` itself is constant and cannot be changed.

   char *const ptr

This should be read as a constant pointer of type char.

Example program::

  char var1='A';
  char var2='B';
  char *const ptr=&var1;
  ptr=&var2; // Generates compile time error because ptr1 is declared constant and cannot be reassigned

We can combine both and write ``const char * const ptr`` and in this case, both the char and the pointer are constants.

Real functions using ``const char *``. The ``printf`` or ``puts`` functions in the standard library::

   int	 printf(const char * __restrict, ...) __printflike(1, 2);
   int	 puts(const char *);

## Arrays
To create an array, choose the type of the elements stored in the array, choose the size (optional), and stor the data in the array::

   char str_a[20];
   
or::

   char str_a[]="abc123"; //The size of the array is optional

or::

   char str_a[7]="abc123"; //Don't forget the \0 last character
   


Why arrays can be dangerous...

How to declare an array in C99::

   #define MAX_SIZE n
   
   int array[MAX_SIZE];

## Strings

In C, strings are arrays of characters. A pointer stores the memory address of the first element of the array: ``char *ptr = "Hello, World!"``. As seen in the previous section, the elements of an array occupy contiguous blocks of memory.

The difference between::
   
   char str_a[7]="abc123"; //Read Write memory
   
and::
   
   char *p_str = "abc123"; //Read memory
   
is that in the later case, we work with a string constant that cannot be changed. In the first case, we have an array of character variables; therefore we can change the content.   

## Command-line parameters

Let's explain ``int argc`` and ``char const *argv[]``...

## Toolbox

### gdb

### Make
All actions, rules etc... are identified by tabs. To make sure that tabs are correctly inserted in the makefile, enter

``cat -e -t -v makefile_name`` 

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

On linux::
   
   gcc
   
On MacOs::
   
   gcc -dynamiclib -o libxxxx.dylib xxxx.c
   
Verify the library::

   file libxxxx.dylib
   
You should get::

   libxxxx.dylib: Mach-O 64-bit dynamically linked shared library x86_64
   
Finally, compile your application, link it to your library or libraries execute it::

   gcc -L. -lxxxx -lyyyy -o mainsl main.c
   
   ./mainsl
   
## Resources

The technique called "Clockwise/spiral rule" helps to parse any C declaration and can be found [here](http://c-faq.com/decl/spiral.anderson.html).
