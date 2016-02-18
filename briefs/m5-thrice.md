# More than Thrice

Assume that

```python
def compose(f, g):
  return lambda x: g(f(x))

def double(f):
  return compose(f, f)

def thrice(f):
  return compose(compose(f, f), f)

add1 = lambda x: x + 1
```

Notice that the brackets are different for these two expressions

```python
thrice(double(add1))(0)  # Expression 1
```

and

```python
thrice(double)(add1)(0)  # Expression 2
```

**Do the two expressions return the same thing? What is the difference between them?**

## Order of processing

In mathematics, the BODMAS rule specifies operator precedence. For a given expression, there may be more than one order of computation that conforms to the rule, but no matter which order you choose, you should arrive at the same answer as long as you adhere to the rule. For example, `2*3+10/5` yields `8` whether you do the multiplication `*` or division `/` first.

Python also [specifies an operator precedence](https://docs.python.org/3/reference/expressions.html#operator-precedence). In this section, we will focus on the order functions are called. The ordering described here will help you to deduce the correct answer, but it might not necessarily be the order executed by the Python interpreter.

To a beginner, the order of computation for expressions like those above can be ambiguous. The rule of thumb is that before a function call is made, the function itself and each argument supplied to it needs to be "prepared" first.

Let's see how this works with the two expressions.

### Expression 1

In `thrice(double(add1))(0)`, we are trying to call the function returned by `thrice(double(add1))` with the argument `0`. The argument `0` is already a Python primitive, but `thrice(double(add1))` needs to be evaluated so that it yields a function.

In `thrice(double(add1))`, we are calling `thrice` with the argument `double(add1)`. This time, the function `thrice` does not need to be evaluated because we already know its definition. The argument `double(add1)`, on the other hand, needs to be evaluated.


For the function call `double(add1)`, both the function and the argument need not be evaluated, so the call can be made immediately. Once the result of `double(add1)` has been computed, `thrice` can be called with the result of `double(add1)` as its argument. Finally, we can apply the function yielded by `thrice(double(add1))` to `0`.

The order of evaluation can be summarized as

```python
double(add1)
thrice(double(add1))
thrice(double(add1))(0)
```

### Expression 2

Like in the first expression, we interpret `thrice(double)(add1)(0)` as the function returned by `thrice(double)(add1)` being called with the argument `0`. `thrice(double)(add1)` is interpreted as a call to the function returned by `thrice(double)` with the argument `add1`.

The order of evaluation can be summarized as

```python
thrice(double)
thrice(double)(add1)
thrice(double)(add1)(0)
```

*"Huh? Why can't we do `(add1)(0)` first for `thrice(double)(add1)(0)`? Doesn't it just return `1`?"*

This seems plausible because in mathematics, the redundant parentheses in `((2*3)+((10/5)))` do not affect the result. They can be removed or ignored. Indeed, this is sometimes true in Python also:

```python
>>> ((2*3)+((10/5)))
8.0
>>> (((max)))(1,9,3)
9
>>> (add1)(0)
1
```

*"In that case, how do I tell when the parentheses indicate a function call and when I can ignore them? :confused:"*

One heuristic is to look at what precedes the open parenthesis `(`:

- If the `(` is the first non-whitespace character on a new line and the previous line does not end with a `\`, the parentheses do not indicate a function call.
- If the `(` is immediately preceded by another `(` or by an infix operator (`+ - / * // %` etc), the parentheses do not indicate a function call.
- For all other cases, the `(` most likely represents a function call and you should check if whatever precedes the `(` returns a function.

Once you have identified which parentheses represent function calls, you can use the rule of thumb described above to deduce a possible order of computation.


## Tracing Thrice

Now that we know the order to evaluate the expressions, let's *trace* the evaluation.


### Expression 1

For simplicity, we present the evaluation in the same style as a mathematical derivation. Since each of the functions we defined at the start do not do any processing, but return immediately, we can substitute each function call with the function's definition:

```python
thrice(double(add1))(0)  # Expression 1
= thrice( compose(add1, add1)      )(0)
= thrice( lambda x: add1(add1(x))  )(0)
```

Let's pause for a moment. What does `lambda x: add1(add1(x))` do? Since it adds 2 to `x`, that is, it produces the same result as `lambda x: x + 2`, let us call it `add2`, i.e. `add2 = lambda x: add1(add1(x))`.

Now we have

```python
...
= thrice( lambda x: add1(add1(x)) )       (0)
= thrice( add2                    )       (0)
= compose( compose(add2, add2)     , add2)(0)
= compose( lambda y: add2(add2(y)) , add2)(0)
= compose( add4                    , add2)(0)  # simplify again
= (lambda x: add2(add4(x)))(0)
```

Next, we apply the function `(lambda x: add4(add2(x)))` to `0` to get

```python
...
= (lambda x: add2(add4(x)))(0)
=            add2(add4(0))
=            add2(4      )
= 6
```


### Expression 2

```python
thrice(double)(add1)(0)  # Expression 2
= compose( compose(double,double)      , double)(add1)(0)
= compose( lambda f: double(double(f)) , double)(add1)(0)
```

Again, for ease of understanding, let's inspect what `lambda f: double(double(f))` does:

```python
lambda f: double(double(f))
= lambda f: double( compose(f,f)      )
= lambda f: double( lambda y: f(f(y)) )
= lambda f: compose( (lambda y: f(f(y))) , (lambda y: f(f(y))) )
= lambda f: (lambda z: ((lambda y: f(f(y))) ( (lambda y: f(f(y)))(z) ) ))
= lambda f: (lambda z: ((lambda y: f(f(y)))( f(f(z)) )) )
= lambda f: (lambda z: f(f(f(f(z)))) )
```

That was nuts. But you get the drift - do it carefully step by step to understand exactly what is going on.

The function takes a function `f` and returns a function that takes an argument `z` and puts it through `f` four consecutive times. In colloquial terms, it takes a function and returns a do-er that does it four times.

Following the convention, let's name the function `quadruple`, i.e. `quadruple = lambda f: double(double(f))`.

Now we have:

```python
...
= compose( lambda f: double(double(f)) , double)(add1)(0)
= compose( quadruple                   , double)(add1)(0)
= (lambda x: double(quadruple(x)))(add1) (0)
=            double(quadruple(add1))     (0)
=            double(add4)                (0)
=            add8                        (0)
= 8
```

## Wrap Up

```python
>>> thrice(double(add1))(0)  # Expression 1
6
>>> thrice(double)(add1)(0)  # Expression 2
8
```

How cool is that? Same same but different hor.

This article is just to aid your understanding. For your own sanity (and ours), please do not write out all the steps in your mission solution. Just show enough working so that we know that you understand.
