
C Programming
=============

Arrays
======
Why arrays are dangerous...

How to declare an array in C99::

   #define MAX_SIZE n
   
   int array[MAX_SIZE];
  

Make
----
All actions, rules etc... are identified by tabs. To make sure that tabs are correctly inserted in the makefile, enter

``cat -e -t -v makefile_name`` 

on the command line.

``^I`` represents a tab
``$`` represents end of line.

Creating a static library
-------------------------

   gcc -c xxxx.c -o xxxx.o
   ar rcs libxxxx.a xxxx.o
   gcc -static main.c -L. lxxxx -o statically_linked
   
Creating a dynamic library
--------------------------

