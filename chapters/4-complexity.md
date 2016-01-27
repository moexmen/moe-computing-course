# Orders of Growth

Cute introduction by [Algosaur.us](http://algosaur.us/algorithmic-complexity/).

## [Arithmetic Progressions](https://en.wikipedia.org/wiki/Arithmetic_progression) (AP)

APs occur frequently when computing orders of growth. The formula to sum consecutive integers is

$$
1 + 2 + 3 + \cdots + (n-1) + n = \frac{n(n+1)}{2} \in O(n^2)
$$

Example 1:

$$
1 + 2 + 3 + \cdots + 99 + 100 = \frac{100 \times 101}{2} = 5050
$$

Example 2:

```python
def factorial(k):
    return 1 if k == 0 else k * factorial(k-1)

def sum_factorials(n):
    "returns  n! + (n-1)! + (n-2)! + ... + 2! + 1!"
    total = 0
    for i in range(n):
        total += factorial(i+1)
    return total
```

What is the time complexity of `sum_factorials`?

First, we need to calculate the time complexity of `factorial`.
When `factorial(k)` is called, exactly `k` number of steps of computation are done.
To be specific, `k` multiplications are executed.
Thus, the order of growth for the number of steps of execution of `factorial` is $$O(k)$$, i.e. linear.

Now, let's count the number of operations (`+` or `*`) done when `sum_factorials(4)` is called:

```
number of steps
=   1    # i+1
  + 1    # when factorial(1) is executed
  + 1    # addition to total
  + 1    # i+1
  + 2    # when factorial(2) is executed
  + 1    # addition to total
  + 1    # i+1
  + 3    # when factorial(3) is executed
  + 1    # addition to total
  + 1    # i+1
  + 4    # when factorial(4) is executed
  + 1    # addition to total
```

if we rearrange the terms, we get

```
number of steps
=   4                # (i+1) done 4 times
  + 4                # addition to total done 4 times
  + (1 + 2 + 3 + 4)  # calls to factorial
```

Now, if we generalize this for `sum_factorials(n)`,

```
number of steps = n + n + (1 + 2 + 3 + ... + n)
```

Since we only want the *order* of growth of the number of steps and not the exact number of steps itself, we can use our formula.

```
order of growth of number of steps = O(n) + O(n) + O(n^2)
```

We can simplify by taking the term with the fastest growing order.

```
order of growth of number of steps = O(n^2)
```

Thus, the time complexity of `sum_factorials` is $$O(n^2)$$.

## Visualizing Space Complexity

A good way to visualize orders of growth for an algorithm is to use Python Tutor.

Step through your code. At which step of your code is the right side "fullest"?
