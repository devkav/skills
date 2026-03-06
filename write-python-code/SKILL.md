---
name: write-python-code
description: Write python code that follows my personal style guidelines and formatting.
---

When writing python code, always ensure:

1. **Add spacing between code blocks**: Add spaces between code blocks. I like to use 1 newline when inside a function to space things out, and 2 newlines to space out
things like functions, imports, and more. Example:
```python
import pathlib
import vbuPyUtils
from datetime import datetime


MY_CONST_VALUE = "HELLO"


def my_function(my_value):
    my_value_str = str(my_value)
    my_value_str_upper = my_value_str.upper()

    if my_value_str == "":
        return
    else if my_value_str == "abc":
        return my_value_str_upper

    return f"My string: {my_value_str}"


def my_function(a, b):
    return a + b
```

2. **Use constants for hardcoded strings or "magic numbers"**: Hardcoded strings or magic numbers should be avoided. However, if they are necessary, you should use constant
values. These should be defined at the top of the file in all uppercase letters. If there are several constant variables, they should all be added to a config file. To write
a config file, use your `write-python-config-file` skill.

3. **Use clear and descriptive variable names**: Variable names should be clear, and descriptive. Variable names should not be overly verbose, but you should error on the side
of verbosity. Variables should be written in snakecase.

3. **Limit comments**: Comments in code should be avoided unless the code is not self explanatory. Comments should only be used unless it is unclear to a new developer why a 
line is written.

4. **Use pathlib instead of os**: The `pathlib` library should be almost always used when dealing with paths. When dealing with paths, `pathlib` should always be used over the python
`os` library. 

5. **Use typer and rich console for CLIs**: Use `typer` to build CLI tools. Use `rich.console.Console` for output in user-facing applications like CLIs. The built-in `print()` is
fine for debug messages, basic development scripts, and non-interactive output.
