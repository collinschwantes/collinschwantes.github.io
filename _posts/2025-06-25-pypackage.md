---
layout: post
title: Writing a python package with Hatch and pyOpenSci 
date: 2025-03-13 17:39:00
tags: reproducibility python
description: Notes on writing a python package
featured: true
mermaid:
  enabled: true
  zoomable: true
---

I recently published a new R package called [`virionData`](https://github.com/viralemergence/virionData). 
It is essentially a wrapper for the Zenodo api and is designed to 1) provide access to the virion data stored on zenodo and 2) make it easier to track the version of the virion data one is using. 
After announcing the publication of the R package, a colleague almost immediately asked for a python version.
Fair, why should they have to install R a dependency in their pipeline just to get the data?

So now I am setting out to write a python package using Hatch and guidance from [pyOpenSci](https://www.pyopensci.org/python-package-guide/tutorials/get-to-know-hatch.html#).

First impressions: 

In R, we can use `devtools`, `testthat`, and `usethis` to develop a fairly robust package. Granted those three packages load a host of others, the python package development ecosystem seems much less consolidated. 

I almost immediately ran into an issue with hatch.
I wanted to call my package pyVirionData and that meant that my top level directory and the package directory in source had the same name. 
This caused some regex functions in hatch to fail when attempting to build the package. 
I may have also run an unnecessary `hatch init` call. 
So I started over and changed the name of the package to py-virion-data, the sub directory became py_virion_data and everything works as expected. 

As someone who primarialy programs in R, I'm a little nervous about publishing python code. I have developed a strong muscle memory for functional programming and will likley write code in that flavor (as opposed to more object oriented paradigms).

After the initial hiccup with the package name, the tutorials seems to be running smoothly. 

### Writing python code - you're about enter a stream of conciousness section

Using vscode the docString extension is really helpful. 

Having to think in terms of classes makes me more economical. 

Oh yeah, you have to import functions between files, its not all just global like in R. 

python does a good job with json out of the box. this is nice.

File paths are a mess. thank the gods for r's FS package. 

The pythonFileSystem docs are confusing.
There are functions for fs.path.BLAH and there are functions for different types of file systems. 

All file systems have api calls listed here: https://pyfilesystem2.readthedocs.io/en/latest/interface.html

these are called with something like
```
from fs.osfs import OSFS
 
fs_home = OSFS.home(".")
fs_home.makedir("hello") # makes a directory relative to working directory

```

fs itself has classes and methods.

```
import fs
helloworld_path = fs.paths.join("hello","world")
```

we can use them together with something like

```
import fs
from fs.osfs import OSFS
fs_home = OSFS.home(".")
fs_home.makedir("hello")

helloworld_path = fs.paths.join("hello","world")
# note that makedir doesnt make directories recursively.
# there are functions in fs to build up components of a path
# and I am sure they would be useful for creating recursive
# directories
fs_home.makedir(helloworld_path)
```
For loops on items are awesome.

### merge pull requests

I have gotten into the habit of splitting R functions into their own files. 
When adjudicating a PR, I check that each file/function meets my criteria for documentation and clarity. 
Each correction I make is reflected in only that file so I can use the "viewed" feature in github to great effect.
With a monolith file that defines a class and its methods, I have to carefully check each section. 
While polishing up documentation and refining methods, the monolith file is changed, so I have to be extra vigilent about where I made changes. 
This is probably a function of not using subclasses/inheritance properly - though as of this writing the class definition is only ~350 lines.

### publishing workflow

pypi using hatch

1) `hatch version`
2) `hatch build`
3) `hatch publish -r # main or test ` 

grayskull for conda forge - to do

read the docs - to do - this is a little less straightfoward than using `pkgdown` in R to build nice docs for your package. 

## Conclusion

In general the system for publishing a python package is really straight foward. 
The PyOpenSci tutorial made the process very smooth.
I think that since I had already written the R package and knew what functionality I wanted, it was easier to focus on building the python library. 
I would definitely recommend this order of operations for anyone coming from R to python because it allows you to focus on the python syntax and structure. 
Writing out the classes in python made me realize there is a lot of bloat in my R package and gave me ideas about how I could refactor to be more efficient.
