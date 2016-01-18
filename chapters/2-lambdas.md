# Lambdas

## What are lambdas?

A lambda is a special kind of function. You can think of them as a low-powered, no-frills version of "normal" functions.

**"Normal" function:**

```python
def square(x):
    return x * x
```

**Lambda equivalent:**

```python
square = lambda x: x * x
```

**Key differences**
- Lambdas are one-liners
- Lambdas are anonymous

We expand on these points below. Read on!


## What good are lambdas, anyway?

Let's say we have this function:

```python
def apply_to_11(f):
    "takes a function f and applies it to 11"
    return f(11)
```

To print the square of 11, we can do:

```python
def square(x):
    return x * x

print(apply_to_11(square))
```

That's three lines of code. With lambdas, we can do it with one line:

```python
print(apply_to_11(lambda x: x * x))
```

Here is a more compelling example. You may skip this if you don't know about lists, objects and map. Given a list of objects, we extract their names:

```python
def get_name(x):
    return x.name

print(list(map(object_list, get_name)))
```

can be written as

```python
print(list(map(object_list, lambda x: x.name)))
```


Neater right? Assigning the name `get_name` does not add value to the code. When used well, lambdas can improve the readability of your code.

"Aiyo. The `def` version works what... why complicate things?"

Yes, technically a `def` function can do whatever a `lambda` function can do, but not vice-versa. 

"And sure, if we use say `n=20` lambdas, we can save `2*n = 40` lines of code, which is nice, but why else would anyone use them? What were the programmers thinking when they made this feature?"

Well, there are a number of reasons, some pretty deep (GIYF! A starting point is "[functional programming](https://en.wikipedia.org/wiki/Functional_programming)"). Let's discuss one: *anonymity*.

### Anonymity

Names can be a precious resources to a programmer and naming conflicts can be a source of bugs. We don't want to give out names when we don't have to and end up "polluting" the [*namespace*](https://en.wikipedia.org/wiki/Namespace).

Notice that by using lambdas, we freed the names `square` and `get_name` to be used elsewhere. This might not seem much in a small program, but it is helpful when you have more complex ones.

## When *not* to use lambdas?

Lambdas have some limitations. 

### When we want to reuse a function

On the flip-side, if we want to be able to use a function more than once, we need to give it a name so that we have a way to refer to it.

Lambdas are one-use disposables.

### When the function is too complex

First, notice that the `return` statement is implicit in lambdas, e.g. in `lambda x: x*x`, `x*x` is returned even though the `return` keyword is not used. 

Lambdas can only be used for functions that take in one or more arguments and "immediately" return a value. If the there is some processing to do and you need a few lines, for example,

```python
def get_third_ranked(list_of_runners, n):
    list_of_runners.sort()
    return list_of_runners[n]
```

then use `def` to define the function.


Lambdas are meant for simple functions. If your function is complex, consider using `def` even though you might be able to write it as a long lambda. Readability is important for code maintainability (:
