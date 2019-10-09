# A quick intro to Python

## Background
  * Interpreted, cross platform, 
  * Pros: Data manipulation, easy(ish) to learn the basics, popular, open source, loads of libraries, compact syntax, good as a beginners language and a serious one.
  * Cons: performance, weakly typed, suddenly gets more complicated after you learn the basics, compact syntax leads to horrible one liners, poor handling of concurrency

## Identation
  * Python forces identation
  * Uses indentation instead of braces or begin/end for if statements, for loops, functions etc
  * Underneath everything is an object

## Types

  * Weakly typed, implicit type assignment

  print(1 + int('2'))
  3

  print(str(1) + '2')
  12

  * Force conversion with float(), int() and str()

### Lists, Tuples and Dictionaries

#### Lists
  * Lists like arrays in other languages (mostly)
  * a = [1,2,3]
  * b = a[1] (2)
  * b = a[1:2]  (2)
  * b = a[0:2] (1,2)

#### Tuples
  * Like lists but immmutable, can't be changed once created.
  * Same operators, but use ( ) instead of [ ] 

#### Dictionaries
  * Associative arrays, key/value pairs
  * Use keys instead of indicies
  * Fast(er) lookups, O(1)
  * c = { "robot": "Boat", "flying": "Drone"}
  * c.get("robot")

## Functions
  * Called by doing function_name(parameter1,parameter2)
  * Named parameters function_name(paramater1=value)
  * Defined with def keyword
  * def function_name(paramter1, parameter2):

## Loops
  * for loops:
  * for i in 1,2,3:
  * or
  * for i in range(1,3):
  * or
  * for i in list_name:

## If statements
  * if a == 1:
  * if a == "a":
  * if a < 1:
  * if a > 1:

## Modules
  * import <library name>
  * import <library name> as <shortname>
  * import matplotlib as m
  * from <library> import <function>
 
### Pip
  * Python's package manager, installs extra libraries
  * pip install <library name>
  * Published via [pypi](https://pypi.org/) website

### Virtual env

## Python 2 vs 3
  * Python version 2 and 3 have some differences
  * python 2 allows print "hello world"
  * python 3 forces brackets, print("hello world"). Still valid in python 2.
  * Different integer division rules. Python3 auto converts integers to floats, python2 rounds down.
  * Rounding rules for floats different too. 
  * Version 3 slowly becoming standard but 2 lives on in many places
  * Often have both installed
  * explicitly run python2/python3 commands
  * pip = python2, pip3 = python3, different library sets
  * from __future__ import division 
  * see https://sebastianraschka.com/Articles/2014_python_2_3_key_diff.html
  
