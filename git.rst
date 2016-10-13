
Working locally
===============

Checking the status of files
----------------------------
  
  git status
  
To have a shorter output

  git status -s

Tracking new files
------------------

  git add README.rst
  

Committing files
----------------

  git commit -m "Commit message"
  
or to skip the staging

  git commit -a -m "Commit message"
  
Undoing things
--------------

   git commit --amend
   
Unstaging a staged file
-----------------------

  git reset HEAD CONTRIBUTING.md
  
Unmodifying a modified file
---------------------------
If you want to cancel a commit on a file:

  git checkout -- CONTRIBUTING.md
  
Working with remotes
====================




  

