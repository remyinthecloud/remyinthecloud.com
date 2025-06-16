---
title: [What is a Module in Python]
date: 2025-06-16 12:47:00 -500
categories: [python, data engineering]
tags: [python, modules, attributes, syntax, data, data analyst, data engineer]
---

Modules are Python scripts, they are files ending with the .py extension.

Modules can contain functions and attributes, as well as, other modules. Similar to functions, modules allow us to reuse code blocks.

### Import Module

To import a module we use the below syntax:
```python
import <module_name>
```

Example:
```python
import os
```

Type will be <class 'module'>

To know what functions are available within a module we can use help.
```python
help(os)
```

> [!WARNING]
> This will return a **very large** output.

#### Helpful Functions in the OS Module

##### Get the current working directory:

```python
os.getcwd()
```

- This will return the current working directory name, including any directories above it.

Example Output:
```python
'/home/user_name/python_learning'
```

##### Changing directory:

```python
os.chdir("/home/new_user")
```


We can check the current directory now:

```python
os.getcwd()
```

Output:
```python
'/home/new_user'
```

#### Module Attributes

Modules also are attributes. In contrast to functions, these are values that perform a task.

For example, we can use the os.environ attribute to get information about out local environment.

```python
os.environ
```

> [!NOTE]
> This is an attribute not a function, as we don't include any parenthesis afterward. As we aren't calling it like we would a function.

- Output will return a dictionary with values such as the location where Python is installed, and the timezone we are based in.

### Important to Know

Importing a whole memory can require a lot of memory.
Knowing this, we can import a single function from a module if that's all we need from that module.

The syntax is below:
```python
from os import chdir
```

We can import more than one function doing the following:
```python
from os import chdir, getcwd
```

Now we can call the function without referring to the module first, because we haven't imported the entire module so Python won't know what os means.

```python
getcwd()
```

Will return the same as our previous output:
```python
'/home/new_user'
```
