# Recursion

### Cute Explanation about Recursion

[Explanation by Algosaur.us](http://algosaur.us/recursion/)

### Factorial Function with Tracing

The function below is simply factorial, but with print statements
to illustrate what's happening.

```python
def fact(n, indent):
    if n == 0:
        print(indent + "BASE CASE: 1\n")
        return 1
    else:
        print(indent + str(n) + "! = " + str(n) + " * " + str(n-1) + "!")
        prev_result = fact(n-1, indent + "  ")
        result =  n * prev_result
        print(indent + str(result) + " = " + str(n) + " * " + str(prev_result))
        return result

print("\n" + str(fact(6, "")))
```

Run it and trace through the print statements to see how the function
approaches the base case, then propagates the result up to obtain the
final answer.

### Cool Stuff

Now that you've learnt about recursion, you should be able to understand
Google's little easter egg when you do a search for 'recursion'.

![Google search for recursion](images/recursion-search.png)
