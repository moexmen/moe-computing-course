# Curve Missions

This mission is meant to help you learn data abstraction.

Understand:
1. Why learn data abstraction?
  - In general, abstractions help us to think about things.
  - Before we can manipulate data, we need to represent them.
  - By hiding some details and sometimes making simplifications, we Manage Complexity.
  - It helps us understand the benefits of Object-Orientated Programming better.
1. We can see data abstraction as *wrapping* data together and attaching some meaning to the package.
1. Methods can be specified for each Abstract Data Type (ADT).
1. What does it mean to "break the abstraction barrier"? Why should we avoid it?

Examples of Abstraction:
- Colour names
- Representing a marker point on whiteboard.
- What can we represent with three points?
  - ADT can have constraints.

Viewport:
- `x: [0, 1], y: [0, 1]`
- Origin at bottom-left

Data types and their methods:
- **Number**
  - Any integer or float has the type **Number**.
- **Unit-Interval**  
  - Any **Number** `n` where `0 <= n <= 1` has the type **Unit-Interval**.
- **Point**
  - `make_point(number_1, number_2)`: (**Number**, **Number**) → **Point**
  - `x_of(point)`: (**Point**) → **Number**
  - `y_of(point)`: (**Point**) → **Number**
- **Curve** is any function in the form (**Unit-Interval**) → **Point**
  - Notes
    - Convention: use the variable name `t` (for 'time') for the **Unit-Interval**.
    - The curve is defined parametrically.
  - `draw_points(num_points, curve)`: (**Number**, **Curve**) → Nothing
  - `draw_points_scaled(num_points, curve)`: (**Number**, **Curve**) → Nothing
  - `draw_connected(num_points, curve)`: (**Number**, **Curve**) → Nothing
  - `draw_connected_scaled(num_points, curve)`: (**Number**, **Curve**) → Nothing

Quiz: If these *"abstract"* data types, then what is treated as *"concrete"* data types?

Quiz: Categorize the methods.
  - Constructors
  - Selectors
  - Predicates
  - Printers

Quiz: Define a **Curve** that represents a straight line drawn between `(1,1)` and `(2,3)`.

**Task 1**

```python
def unit_line_at_y(y):
    return lambda t: make_point(t, y)

a_line = unit_line_at_y(0)
```
Task 1a:
- `unit_line_at_y` input and output type?
- What is the type of `unit_line_at_y` itself?

Task 1b:
- `a_line` input and output type?
- What is the type of `a_line` itself?

Task 1c,d:

> Define a function vertical_line with two arguments, a point and a length, that returns a vertical line of that length beginning at the point. Note that the line should be drawn upwards (i.e., towards the positive-y direction) from the point.

- `vertical_line` input and output type?
- Define `vertical_line`.


Task 1e:

> Using draw_connected and your function vertical_line with suitable arguments, draw a vertical line which is centred both horizontally and vertically and has half the length of the sides of the window.

- See Picture in Mission PDF.


**Task 2 (Curve Transformation)**

> rotate_90 : (**Curve**) → **Curve**

Quiz: Other examples?

Quiz: Write a method that shifts right by 1 unit.

Quiz: Write a method that reflect in x-axis.

Quiz: How to check?


## Pedagogical Notes

- Can a number be a **Unit-Interval** and **Number** at the same time?
  - Look ahead to OOP.
- OOP enforces data and method "wrapping", constraints etc.
- Why does **Curve** not have a constructor? Can we write one?
- What notation should we use a function does not return anything?
- How would you design an assignment to teach Data Abstraction?
