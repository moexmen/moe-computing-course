# Writing Stubs

When writing a program, we can practise [wishful thinking](chapters/2-abstraction.md) by writing **function stubs**.

A [function stub](https://en.wikipedia.org/wiki/Method_stub)
is a piece of code that stands in for the actual functionality.

Let's have an example. Little Miss Nought wants to write a Tic-Tac-Toe game. Wishfully, she writes the following:

```python
def tictactoe():
    """
    Human plays a single Tic-Tac-Toe game against an AI.
    """
    game = new_game()
    humans_turn = True
    game_result = None
    while game_result is None:
        if humans_turn:
            game = humans_move(game)
            humans_turn = False
        else:
            game = computers_move(game)
            humans_turn = True
        game_result = check_winner(game)
    print(game_result)
```

If she runs `tictactoe()` now, she will get a `NameError` because
some of the functions have not yet been defined. Next, she proceeds to *stub* the missing functions:

```python
def new_game():
    """Returns a representation of an empty game grid"""
    pass

def humans_move(game_board):
    """
    Displays the game board to the user, then
    gets the human player's move and executes it.
    """
    pass

def computers_move(game_board):
    """Executes the computers player's move if empty cell exists"""
    pass

def check_winner(game_board):
    """
    Checks if there is a winner or if it is a draw.
    Returns one of the following strings as appropriate:
    - "Human Wins!"
    - "Computer Wins!"
    - "Draw"
    """
    pass
```

This informally serves as her to-do list. It lists the functions she must implement for the program to be complete.



### Docstring

The text within the triple quotes `"""` in each function is called a **docstring**. They are strings which document what each function is about. Little Miss Nought likes docstrings because they allow her to use English to express what she intends each function to do before she translates those intentions into code. She likes to solve one thing at a time.

Little Miss Nought recommends that you read [PEP 257](https://www.python.org/dev/peps/pep-0257/) to find out the conventions on how docstrings should be written.


#### *Why don't we just use comments?*

If others are going to use your code, then your code needs to be documented. Such documentation usually come in the form of a webpage or pdf file and give details on how to use each function. They are like a users' manual for code.

Docstrings are useful because documentation generators such as
[Sphinx](http://www.sphinx-doc.org/en/stable/) can go through your code, find the docstrings and automatically generate the documentation. How cool is that?

If you follow Little Miss Nought's recommendation,
you can get readable documentation for little effort!

You can also view your helpful description with `help(your_function_name)`. For example,

```
>>> help(new_game)
new_game()
    Returns a representation of an empty game grid
```



### Function Body

`pass` is just a placeholder that does nothing.
Little Miss Nought uses `pass` in the function bodies because
if she leaves the function body empty,
she will get a syntax error. Python requires her to put something.

If Little Miss Nought wants her program to be able to run, she can also go further and hard code the stubs to return some appropriate values.



In conclusion, stubs allows us to get the main outline of the program up
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

Notice that they follow the format described earlier.

### Completing the Question

Look through the given code. Which functions names have not been defined?
Just follow the examples of the existing stubs,
replacing them with the undefined names!

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
