---
title: S3 Classes
parent: Shared Files
grand_parent: Stage 2 Apps
has_children: false
nav_order: 1
---

## S3 classes

Files in **global/classes** define the object oriented programming (OOP)
components of Stage 2 apps, as R S3 classes.

By convention, a class is defined by scripts named:
    
- **myClass_constructor.R** - for object instantiation
- **myClass_methods.R** - where generic S3 methods are found
- **myClass_utilities.R** - functions called by the above scripts

Constructor functions follow suggested R best practices in being
called 'new_myClass' by convention. Note the case pattern.

Because R objects are never accessed by users 
(only by developers writing code), there is
generally no need to export validation or helper functions. 

Objects defined by classes are never used to access or create
the UI, only to streamline code development by encapsulating 
methods and other common logic. 

### genericMethods.R

If your tool suite has classes that implement non-standard generic 
S3 methods, you must define those generics in genericMethods.R.
See the comments within for details.

As an example, your S3 class can implement the standard generic 
<code>print</code> without worries, but to implement a custom
generic <code>myMethod</code>. myMethod must be defined in genericMethods.R.
