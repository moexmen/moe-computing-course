# Functional Abstraction

Functional abstraction allows us to treat functions as black boxes,
meaning that we just care about what a function does and how to use it.
We don't care how it does its task.

This is helpful when implementing more complex programs in a couple of ways.

## Wishful Thinking

We use *wishful thinking* to imagine that we have functions
which do what we want.
We start by thinking of what they should do and how to use them, then proceed to code the main program using these functions as if we have already defined them (although we have not).

Only after we are done with the main program,
do we implement these functions.
In other words, we use functional abstraction to hide or *abstract* away the details for the time being and fill them in later on.
In this way, we break a large problem down into smaller,
more manageable pieces.

This process is known as *top-down design*. To understand how to do this practically, see the chapter on [writing stubs](chapters/2-stubbing.md).

## Building from the Bottom Upwards

Functional abstraction also helps us to manage the complexity of our programs when build them upwards,
i.e. when we start the process of filling in the details.
This happens when we (re)use existing functions written by ourselves or by others.
We are doing this whenever we `import` a library into our programs.

This is akin to building flats using pre-frabricated parts instead of individual bricks.
The process is more manageable and quicker.

![](images/prefab.jpg)
