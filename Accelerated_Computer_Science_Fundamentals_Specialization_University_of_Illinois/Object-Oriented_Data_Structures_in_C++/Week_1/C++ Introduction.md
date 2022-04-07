
![[Primitive types in C++.png]]

![[User defined types.png]]

![[Starting a C++ program.png]]

* Setting up C++ on your local repo and environment

Keeping the Local Repository Updated
If you have cloned the git repo (repository) locally using the "git" command, then you can also receive updates that the course staff might make. For example, we may add small bug fixes or improvements, as well as further examples. Here's how you can make sure you have the latest version.

First, if you have made changes to the example files that you want to keep, you should manually make a backup copy of these to another directory. (There are advanced git commands that can do something like this for you, but for now, it's easiest to make a backup copy of your work manually.)

Then, in the bash terminal, make sure you are in the coursera-cs400 directory where you have cloned the repo locally. The terminal commands below should be entered in the bash terminal one at a time. These commands will ensure you are on the main "master" branch, reset any changes you have made, and then pull the latest versions from the server:

```
git checkout master
git stash
git pull
```

After you do this, you should be sure to do "make clean" before running "make" again in any of the example directories. That way, you will force the example to be rebuilt completely using the latest version of the code.

If you experience any confusing git error messages while trying to update your local repo, the simplest solution to clone a fresh copy of the entire repo as described in the earlier steps above, being sure to clone to a new directory locally. The newly cloned copy will have the latest version.

![[C++ Header file.png]]

![[C++ Header file example.png]]

![[C++ Implementation class.png]]

![[C++ Main file.png]]

![[Standard library organization 1.png]]


![[Using namespace in C++ main file.png]]

![[Using namespace in C++.png]]

![[Using namespace in C++ Cube.cpp.png]]