---
title: What is a Function in Python
date: 2025-06-16 12:36:00 -500
categories: [python, data engineering]
tags: [python, functions, syntax, data, data analyst, data engineer]
---

A **function** is a block of reusable code, that performs a specific task.
This is helpful when you have code, complex or not that you will be using often within your program.

We will cover built-in functions in Python specifically. We can also create custom functions in Python.

## Numeric Functions

### Min()

Returns the smallest numeric value in a list.

- Example:

```python
sales = [120.64, 120.5, 99.65, 72.35]

# Find the lowest sale
print(min(sales))
```

- Output:

```python
72.35
```

### Max()

Max returns the largest numeric value in a string.

- Using the previous example:

```python
print(max(sales))
```

- Output:

```python
120.64
```

### Sum()

Sum adds all the values in a list.

- Using sales list in previous example:

```python
print(sum(sales))
```

- Output:
```python
413.14
```

### Round()

Round will round the value to the nearest decimal specified.

```python
print(round(sum(sales), 1))
```

- Output:
```python
413.1
```

If no number is specified then python will round to the nearest whole number.

## General Purpose

### Len()

The Len() function returns the number of items in an object. It can be applied to various data structures.

- Using our previous sales list:
```python
print(len(sales))
```

- Output:
```python
4
```

### Sorted()

The sorted() function returns a new sorted list from the elements of any iterable without modifying the original iterable.

```python
print(sorted(sales))
```

- Output:
```python
[72.35, 99.65, 120.5, 120.64]
```

### Help()

The help() function provides information on how to use a function.

```python
print(help(sorted))
```

- Output:
```python
Help on built-in function sorted in module builtins:

sorted(iterable, /, *, key=None, reverse=False)
    Return a new list containing all items from the iterable in ascending order.

    A custom key function can be supplied to customize the sort order, and the
    reverse flag can be set to request the result in descending order.
```