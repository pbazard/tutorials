

Display line number: ``:se nu``

Number of lines in a file: ``:echo line('$')``

File explorer: ``Sex``

Create a new file: ``:e filename``

Forward one word: ``w``

Backward one word: ``b``

Undo last action: ``:u``

Redo the last action: ``.``

Delete an entire line and stay in edit mode: ``dd``

Delete an entire line and switch to insert mode: ``cc``

Select current paragraph: ``vip``

Search: ``/pattern``

Search a specific word: ``*``

Back full screen: ``CTRL + b``

Forward full screen: ``CTRL + f``

Forward half screen: ``CTRL + d``

Back half screen: ``CTRL + u``

Working with buffers
--------------------

List of buffers: ``:ls``

Next buffer: ``:bn``

Previous buffer: ``:bp``

Specific buffer: ``:b2`` for example

Delete buffer: ``:bd`` or ``:bd!``

Create a vertical split and show buffer number 3 in the window to the left: ``:vertical sb 3``

Other useful stuff
------------------

How to remove all lines containing a "certain pattern": ``:g/certain\ pattern/d``

How to remove all blank lines: ``:g/^$/d``



