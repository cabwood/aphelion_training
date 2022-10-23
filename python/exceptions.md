# Exceptions

Most modern languages have some form of exception system, an exception being any error (or deliberate event) that interrupts the usual program flow. The trouble with exceptions is that if they are not dealt with, they will cause execution to halt. Obviously this is not desirable if the program is supposed to keep running no matter what, such as a web server.

Every language implements the exception mechanism differently. Python uses a base class `Exception` to represent an exceptional condition, and sub-classes of that class to represent different kinds of exceptions, which hold additional information (such as an error message) about what happened. Not all exceptions are errors, sometimes you deliberately "raise" an exception to indicate some condition that requires special handling, but that is not considered an error, per se.

## try: except:

Here we divide by zero:

```
>>> 5 / 0
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ZeroDivisionError: division by zero
```

Normally this would cause your program to halt, but we can "wrap" the division operation (or any code that could potentially raise an exception) inside a `try: except:` structure. The code block following `try:` is executed as usual, but if an exception is raised within that block of code, the block is immediately terminated and execution continues with code block following `except:`:

```
>>> try:
...     print(5 / 0)
... except:
...     print("Something went wrong")
... 
Something went wrong
```

## else:

Sometimes you will want to execute code *only* if *no* exception was raised in the `try:` block. This is achieved with an `else:` clause. Here are two examples using `except:` and `else:`, the first raising an exception in the `try:` block, the second having no problems:

```
>>> try:
...     print(5 / 0)
... except:
...     print("Something went wrong")
... else:
...     print("Everything went swimmingly")
... 
Something went wrong
```

```
>>> try:
...     print(5 / 2)
... except:
...     print("Something went wrong")
... else:
...     print("Everything went swimmingly")
... 
2.5
Everything went swimmingly
```

## finally:

Often you will want something to be exceuted regardless of whether an exception occured. For this purpose there exists the `finally:` clause. Here, if you look closely, the print statement inside the `finally:` block is successfuly executed, even though the "division-by-zero" error occurs, and the exception is raised only after the `finally:` block finishes:

```
>>> try:
...     print(5 / 0)
... finally:
...     print("This always gets executed")
... 
This always gets executed
Traceback (most recent call last):
  File "<stdin>", line 2, in <module>
ZeroDivisionError: division by zero
```

In that last example, the program will still be halted, because the exception is not handled by an `except:` block; in other words, the exception is still raised, but not dealt with. You can combine `try:`, `except:` and `finally` into a single structure, to handle all possible outcomes, and prevent execution from halting:

```
>>> try:
...     print(5 / 0)
... except:
...     print("Something went wrong")
... finally:
...     print("This always gets executed")
... 
Something went wrong
This always gets executed
```

Any code following this last example would continue to execute as if nothing went wrong.

A great use-case for `finally:` is when you open a file; if you fail to close the file when you've finished with it, it gets left open, using up system resources. This kind of thing leads to memory leaks and resource exhaustion, which are clearly bad. Here we open a file, but the code that actually uses it could raise an exception. We want that file to be closed under *any* circumstances, exception or no exception, and for this we employ `finally:`

```
f = open("numbers.txt", "r")  # Acquire some resource
try:
    # Do things with the resource that might raise an exception
    line = f.readline()
    print(int(line))
finally:
    # Always, always, always release the resource
    f.close()
```

It's important to note that the resource being protected here (f = open...) should not be acquired inside the `try:` structure, since if the open() function fails (maybe the file doesn't exists, or is locked), we definitely *should not* try to close it!

## Mixing it all together

All these clauses can appear in a `try:` structure:

```
try:
    # Do something that may or may not raise an exception
except:
    # Code to run if an exception is raised
else:
    # Code to run if an exception is NOT raised
finally:
    # Code to run in all cases, exception or no exception
```

## Responding to Exception Type

We've only seen the `ZeroDivisionError` so far, but there are many types. `ValueError` is raised when the argument to a function does not have an appropriate value. Here we try to convert a string to an integer, but the string does not have an appropriate value:

```
>>> int("abc")
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: invalid literal for int() with base 10: 'abc'
```

Here we pass a list to the `int()` function, which raises a `TypeError`:

```
>>> int([1, 2, 3])
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: int() argument must be a string, a bytes-like object or a real number, not 'list'
```

We can respond differently to different exception types by using multiple `except:` clauses:

```
>>> age_str = "52"
>>> try:
...     age_int = int(age_str)
... except ValueError:
...     print("The value of age_str is not valid")
... except TypeError:
...     print("The type of age_str is not valid")
... else:
...     print("The value and type of age_str were valid")
... finally:
...     print("Thanks for playing")
... 
The value and type of age_str were valid
Thanks for playing
```

```
>>> age_str = "NO"
>>> try:
...     age_int = int(age_str)
... except ValueError:
...     print("The value of age_str is not valid")
... except TypeError:
...     print("The type of age_str is not valid")
... else:
...     print("The value and type of age_str were valid")
... finally:
...     print("Thanks for playing")
... 
The value of age_str is not valid
Thanks for playing
```

```
>>> age_str = [51, 52, 53]
>>> try:
...     age_int = int(age_str)
... except ValueError:
...     print("The value of age_str is not valid")
... except TypeError:
...     print("The type of age_str is not valid")
... else:
...     print("The value and type of age_str were valid")
... finally:
...     print("Thanks for playing")
... 
The type of age_str is not valid
Thanks for playing
```

It's possible that the code inside the `try:` block raises an exception that you weren't expecting, but that needs to be handled anyway. You do this by including a last `except:` clause with no exception type. Note the deliberate missing `_` in `agestr`, that will raise an AttribteError, since it doesn't exist:

```
>>> age_str = "52"
>>> try:
...     age_int = int(agestr)
... except ValueError:
...     print("The value of age_str is not valid")
... except TypeError:
...     print("The type of age_str is not valid")
... except:
...     print("Something else went wrong, that wasn't a ValueError or TypeError")
... else:
...     print("The value and type of age_str were valid")
... finally:
...     print("Thanks for playing")
... 
Something else went wrong, that wasn't a ValueError or TypeError
Thanks for playing
```

You may write a single block of code that handles different types of exception by specifying a tuple of exception classes after `except`:

```
>>> age_str = "oops"
>>> try:
...     age_int = int(age_str)
... except (ValueError, TypeError):
...     print("Please enter a valid number")
... except:
...     print("Something else went wrong, that wasn't a ValueError or TypeError")
... else:
...     print("The value and type of age_str were valid")
... finally:
...     print("Thanks for playing")
... 
Please enter a valid number
Thanks for playing
```

## Raising Exceptions

You may raise your own exceptions with the `raise` keyword:

```
>>> age_str = "15"
>>> age_int = int(age_str)
>>> if age_int < 18:
...     raise ValueError("You are too young to vote!")
... 
Traceback (most recent call last):
  File "<stdin>", line 2, in <module>
ValueError: You are too young to vote!
```

## Accessing the Exception Object

Of course you can trap your own exceptions in a `try:` structure, as you can any system-generated exceptions. Here I will use the `as` keyword to capture the exception object and convert it to a string to be displayed:

```
>>> age_str = "15"
>>> try:
...     age_int = int(age_str)
...     if age_int < 18:
...         raise ValueError("You are too young to vote!")
... except (ValueError, TypeError) as exc:
...     print(str(exc))
... except:
...     print("Something else went wrong, that wasn't a ValueError or TypeError")
... else:
...     print("You are old enough to vote")
... finally:
...     print("Thanks for being a good citizen")
... 
You are too young to vote!
Thanks for being a good citizen
```
