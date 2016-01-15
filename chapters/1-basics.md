# Python Basics

Basic operators, syntax, conditionals

## `if True:` Huh? If what is true?

When well-written, Python code can usually be made to read like English.

```python
if (2 < 3) and ("me" == "you"):
    # if-body
else:
    # else-body
```

We read this as *"if two is less than three and the string 'me' is the same as 'you', then do whatever is in the if-body. Otherwise, execute the code in the else-body"*.

On the other hand, this piece of code can look confusing:

```python
if False:
    # if-body
else:
    # else-body
```

"If false? Huh? If what is false? Did we miss out something?", you ask. This following snippet would have made more sense:

```python
if is_odd(x) is False:
    print("x is an even number")
```

### How it works

The Python interpreter cannot tell which branch to run from the line `if (2 < 3) and ("me" == "you"):` directly. It will first evaluate the expression between the `if` keyword and the colon `:` and reduce it to either `True` (or equivalent) or `False` (or equivalent like `0`). Only then will it know which block of code to execute.

In this sense, we can say that the interpreter *only* knows how to execute either

```python
if True:
    # if-body
else:
    # else-body
```

or 

```python
if False:
    # if-body
else:
    # else-body
```

The interpreter combines this ability with its ability to simplify expressions like `(2 < 3) and ("me" == "you")` into `True` or `False` in order to process our English-like if-statements. 

### Examples

Let's call the python interpreter Py. Say 'Hi!' to Py!

![](https://upload.wikimedia.org/wikipedia/commons/thumb/0/0a/Python.svg/48px-Python.svg.png)

User: Py, execute this for me

```python
if (2 < 3) and ("me" == "you"):
    # if-body
else:
    # else-body
```

Py: Hmm, I don't know if I should execute the `if` or `else` branch yet. Give me a moment, let me simplify things a bit. `2 < 3` is `True` and `"me" == "you"` is `False`. Easy-peasy-lemon-squeezy. 

```python
if True and False:
    # if-body
else:
    # else-body
```

Py: \*scratches head* Hold on a second. I need to simplify some more:

```python
if False:
    # if-body
else:
    # else-body
```

Py: There. We should execute the `else` block!

**Note:** This is a simplification of what really goes on, but we hope it helps your understanding (: 
