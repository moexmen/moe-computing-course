# Functions

## Huh? Why are there two parentheses in `add_5(x)()`?

```python
def zero():
    return 0
```

This function takes in no arguments and returns `0`.

```python
>>> x = zero
```

Here, the function zero is assigned to `x`. Note that we have not yet called the function, so there is no returning of values.

```python
>>> x = zero()
```

Here, zero is being called and it returns `0`. So `x` takes the value `0`.

```python
def wrapper():
    return zero
```

This function takes in no arguments and returns the function zero
.

```python
>>> y = wrapper
```

Here, `y` is assigned the function wrapper.

```python
>>> y = wrapper()
```

Here, wrapper is being called with no arguments. It returns the function zero; the value of `y` is not a number, but a function that returns a number when called. Now, let's call that inner function to obtain the number `0`:

```python
>>> y = wrapper()()
```

In this line, we can think of the first function call (denoted by the first parentheses pair) as serving to 'unwrap' and reveal the function `zero`. The second function call is made to the 'unwrapped' function `zero` and the number `0` is returned. Thus, the value of `y` in this line is `0`.