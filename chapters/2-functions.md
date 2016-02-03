# Functions

## Huh? Why are there two parentheses in `add_5(x)()`?

```python
def shell_with_pearl():
    return 'pearl'
```

This function `shell_with_pearl` takes in no arguments and returns the string `'pearl'`.

```python
>>> a = shell_with_pearl
>>> a
<function shell_with_pearl at 0x1078ff268>
```

Here, the function `shell_with_pearl` is assigned to `a`.
Note that we have not yet called the function, so there is no returning of values.

```python
>>> b = shell_with_pearl()
>>> b
'pearl'
```

Here, `shell_with_pearl` is being called and it returns the string `'pearl'`.
So `b` takes the value `'pearl'`.

```python
def wrapper():
    return shell_with_pearl
```

This function takes in no arguments and returns the function `shell_with_pearl`.

```python
>>> c = wrapper
>>> c
<function wrapper at 0x109543ea0>
```

Here, `c` is assigned the function `wrapper`.

```python
>>> d = wrapper()
>>> d
<function shell_with_pearl at 0x1078ff268>
```

Here, `wrapper` is being called with no arguments. It returns the function `shell_with_pearl`;
the value of `d` is not a string, but a function that returns a string when called.
Now, let's call that inner function to obtain the string `'pearl'`:

```python
>>> e = wrapper()()
>>> e
'pearl'
```

In this line, we can think of the first function call (denoted by the first parentheses pair) as serving to 'unwrap' and reveal the function `shell_with_pearl`. The second function call is made to the 'unwrapped' function `shell_with_pearl` and `'pearl'` is returned. Thus, the value of `e` is `'pearl'`.
