
=========
C is easy
=========

Pointers
========
The location pointed by ``ptr`` cannot be changed or the value pointed at is cannot be changed **by** this pointer. It can be viewed as a read-only pointer.

   const char *ptr
   
This should be read as ``[const char] pointer``, **BUT** the value pointed at is **NOT** itself a constant; it can be changed by another pointer for example. One use case could be to provide access to a file, for example, in read-only mode for a certain type of users and in read-write mode for the owner of the file.

Example program::

  char var1='A';
  printf("%c\n",var1);
  const char *ptr1 = &var1;
  char *ptr2 = &var1;
  //*ptr1='C'; //generates compile time error because ptr1 is a read-only pointer
  *ptr2='C'; //ptr2 can change the value of var1 from 'A' to 'C'
  printf("%c\n",var1);
   
The ``ptr`` itself is constant and cannot be changed.

   char *const ptr

This should be read as a constant pointer of type char.

Example program::

  char var1='A';
  char var2='B';
  char *const ptr=&var1;
  ptr=&var2; // Generates compile time error because ptr1 is declared constant and cannot be reassigned

We can combine both and write ``const char * const ptr`` and in this case, both the char and the pointer are constants.

Arrays
======
Why arrays can be dangerous...

How to declare an array in C99::

   #define MAX_SIZE n
   
   int array[MAX_SIZE];

Strings
======

Command line parameters
=======================
Let's explain ``int argc`` and ``char const *argv[]``...

Make
----
All actions, rules etc... are identified by tabs. To make sure that tabs are correctly inserted in the makefile, enter

``cat -e -t -v makefile_name`` 

on the command line.

``^I`` represents a tab
``$`` represents end of line.

Creating a static library
-------------------------


On linux::

   gcc -c xxxx.c -o xxxx.o
   
   ar rcs libxxxx.a xxxx.o
   
   gcc -static main.c -L. lxxxx -o statically_linked
   
Apple MacOs does not support static linking.

Creating a dynamic library
--------------------------
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
   

