# Abstraction

Functional abstraction allows us to treat functions as black boxes,
meaning that we just care about what a function does and how to use it.
We don't care how it does its task.

This is helpful when implementing more complex programs.
We use **Wishful Thinking** to imagine that we have functions
which do what we want.
We start by thinking of what they should do and how to use them.
This helps you to think about what functions and data you need
before you implement the function.

## Writing Stubs

When writing a program, we can practise wishful thinking by writing
**function stubs**.

A [function stub](https://en.wikipedia.org/wiki/Method_stub)
is a piece of code that stands in for the actual functionality.

The stub allows us to get the main outline of the program up
before figuring out the details.
While incrementally working towards the final product,
the program can be run without syntax errors, allowing us to write
small manageable chunks at a time.

## Defeating the Balrog

We had quite a few questions about the Balrog lecture training question.
The main difficulties were not knowing what the question wanted,
and unfamiliarity with Python's syntax for defining functions.

### Similar Examples

We have already written three stubs.
`spawn_balrog`, `balrog_attack` and `take_defensive_action`.

We'll cover their main parts below.

#### Function Definition

Let's look at `def balrog_attack(balrog, person)`

The function starts with the Python keyword `def`, for "define",
followed by the function's name (`balrog_attack`). Finally, variable names
(`balrog`, `person`)
for the function's parameters are surrounded by parentheses.


#### Docstrings

Notice that both functions have an English sentence right below the `def`
line. This is a **docstring**. It's meant to document your code,
explaining what the function is supposed to do.

[PEP 257](https://www.python.org/dev/peps/pep-0257/) explains Python's
docstring conventions.

*Why don't we just use a comment?*

Docstrings are useful for documentation generators such as
[Sphinx](http://www.sphinx-doc.org/en/stable/). These programs
go through your code, find the docstrings and generate various output
formats of your documentation.

You can also view your helpful description with `help(your_function_name)`.


By following the conventions, you can get readable documentation for
little effort!

#### Function Body

If you leave the function body empty, you will get a syntax error. Python requires you to put something.
You can put `pass`. `pass` is just a placeholder that does nothing.

### Completing the Question

Look through the given code. Which functions names have not been defined?
Just follow the examples of `spawn_balrog` and `balrog_attack`, replacing
them with the undefined names!

#### Syntax Error!

*I can't pass the test! There's this red box which says SyntaxError!!!*

A common error we've seen is code which looks like this:

```python
def yell(protagonist, 'You cannot pass!'):
    """The protagonist yells a message"""
    pass
```

We did tell you to follow existing examples, but copy and paste can be taken
too far.

Here, the function invocation was simply copied, and `def` was added in front.
When defining a function, the list of things you pass to it is represented by variables.
These variables can be used later when you write the function body.

Look closely. `'You cannot pass!'` is **not** a variable.
It's surrounded by quote marks, making it a string!

Now go forth and defeat the evil balrog!!
