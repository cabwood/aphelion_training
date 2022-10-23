# Variables, Objects and Expressions

In the following examples, I use the `#` character to indicate the beginning of a comment. The Python interpreter ignores everything on a line that follows the `#` character.

## Assignment

Values are assigned using `=`. Variables don't have to be declared before they are assigned to, and do not have any explicit type:

```
w = True        # Create variable w, and assign a literal boolean value
x = 7           # Assign a literal integer value
y = 2.0         # Assign a literal floating point value
z = "elephant"  # Assign a literal string value
a = x           # Assign the value of variable x to variable a
```

## Methods

Everything in Python is an object, which means everything has methods. Any string object, for example, has methods to manipulate the string in some way, or return some "transformed" version of the string. A method is invoked in an expression by using the variable object's name and method name joined with a `.`, and followed with parentheses enclosing a comman-separated list of arguments (if any are required), like this:

```
>>> animal = "Elephant"
>>> animal.lower()
'elephant'
>>> animal.upper()
'ELEPHANT'
>>> animal.count('e')  # Count the occurrences of the lowercase 'e'
1
```

Since the return value of a method is also an object, with its own methods, you may chain `.` multiple method invokations one after the other. The `lower()` method of string objects returns another string object, so this will work:

```
>>> animal.lower().count('e')
2
```

## Expressions

Expressions work as you would expect in any language, using parentheses to group and prioritise operations:

```
>>> a = (1 + 2) * 3
>>> print(a)
9
```

The arithmetic operators are the usual ones:

 - `+` addition
 - `-` subtraction
 - `*` multiplication
 - `/` division
 - `**` exponentiation
 - `//` integer division
 - `%` modulus

Some examples of the obscure ones:

```
>>> 2 ** 10             # 2 raised to the 10th power
1024
>>> 8 / 3
2.6666666666666665      # Note the rounding error
>>> 8 // 3              # Integer part of 2.666666666
2
>>> 15 // 2             # Integer part of 15 / 2
7
>>> 15 % 2              # Remainder part of 15 / 2
1
```

### None

The special value `None` is a singleton, meaning there is only ever one instance of the `None` object, and every time you use `None`, or create a variable with value `None`, you are referring to the same object. `None` represents the absence of a value. Functions can return None to indicate that no result is available.

`None` is the equivalent of C's NULL keyword, and the null keyword in Java and Javascript. It is an object, just like any other value in Python, but it has no useful methods.

### Boolean Expressions

There are two boolean values, `True` and `False`, both singletons, for use with the if keyword and other conditional execution statements. Expressions return a boolean result if they employ one of the comparison operators (this is not a complete list):

 - `==` is equal to
 - `!=` is not equal to
 - `<` is less than
 - `>` is greater than
 - `<=` is less than or equal to
 - `>=` is greater than or equal to
 - `not` logical inverse
 - `is` is the same instance as
 - `in` contains

```
>>> a = 3
>>> b = 5
>>> a == b
False
>>> "3" == 3
False
>>> a != b
True
>>> a < 10
True
>>> b > a
True
>>> b > a + 10
False
>>> 5 <= b
True
>>> b is None
False
>>> b is not None   # A use of 'not' unique to Python
True
>>> not (b is None)
True
>>> 4 in [1, 2, 3, 5]
False
>>> 3 in [1, 2, 3, 5]
True
>>> "3" in [1, 2, 3, 5]  # 'in' operator is type-sensitive
False
>>> "z" in "abcdef"
False
>>> "c" in "abcdef"
True
```

Boolean expressions can be combined with `and` and `or` clauses to define complex conditions:

age = 5
(age > 5) and (age < 18)

```
>>> age = 3
>>> (age > 5) and (age < 18)
False
>>> (age <= 5) or (age >= 18)
True
```

## String Literals

There are several ways to enclose a string literal. All the following expressions are valid:

```
"Hello World!"
'Hello World!'
"""Hello World!"""
'''Hello World!'''
```

This flexibility is useful when you wish to include quotation marks as part of the string. The following is invalid because the second single quote mark is interpreted as the end of the string, and what follows is not valid Python code:

    'This won't work'

To solve this, enclose the literal inside double-quote marks:

    "This won't fail"

If you wish to use both type of quotation marks in a single string literal, use triple-qoutes:

    '''This isn't a problem for "good" programming languages'''

Alternatively, use C-like escaping, with the backslash `\` character:

    'This isn\'t a problem for "good" programming languages'
    "This isn't a problem for \"good\" programming languages"

You can use the escape character `\` to include non-printable characters in a string literal, such as newline. Here the sequence `\n` is interpreted to mean a single new-line character, as the `print` function will reveal:

```
>>> my_text = 'This text contains\ntwo lines'
>>> print(my_text)
This text contains
two lines
```

Strings can be concatenated with the `+` operator:

```
>>> s = "Don't forget" + "the space"
>>> print(s)
Don't forgetthe space
```

```
>>> s1 = "Don't forget"
>>> s2 = 'the space'
>>> print(s1 + ' ' + s2)
Don't forget the space
```

Strings are sequences, and behave like lists (See "Lists" below). They can be subscripted and sliced just like lists:

```
>>> s = 'Red cars and blue cars'
>>> s[0]
'R'
>>> s[1]
'e'
>>> s[0:3]
'Red'
>>> s[18:22]
'cars'
>>> s[13:]
'blue cars'
>>> s[:8]
'Red cars'
```

## String Interpolation

Dynamic strings can be created on the fly using "f-string" syntax, which requires a lower case `f` preceding the opening quote. When this `f` is present, anything inside curly braces `{` and `}` within the literal body is evaluated as a normal Python expression, the result of which is inserted into the string:

```
>>> count = 12
>>> f'There were {count} incidents this year.'
'There were 12 incidents this year.'
>>> num = 2
>>> f"The square root of {num} is {num ** 0.5}"
'The square root of 2 is 1.4142135623730951'
```

An older (but still occasionally useful) syntax for string interpolation:

```
>>> "The square root of %f is %f" % (num, num ** 0.5)
'The square root of 2.000000 is 1.414214'
```

## Tuples

A tuple is a variable with multiple values (similar to a list, below, but faster and less flexible). The name "tuple" is a generalisation of words like "triple", "quadruple", "quintuple" etc, all indictating many of something. A tuple in Python is written as a comma-separated list of values enclosed in parentheses `()`:

```
>>> t = (15, "Robert", "Palmer", True)
>>> t
(15, 'Robert', 'Palmer', True)
```

Like lists below, tuples can be subscripted:

```
>>> t
(15, 'Robert', 'Palmer', True)
>>> t[0]
15
>>> t[3]
True
```

Unlike lists, after their creation tuples cannot be modified, they are "immutable". Trying to modify a tuple after its creation will raise an exception:

```
>>> t[1] = "Peter"
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment
```

Tuples and lists can be "unpacked" during assignment operations. In the next example, four variables are assigned simultaneously, each with the corresponding value extracted from the tuple being assigned to them:

```
>>> code, first_name, last_name, is_rock_star = t
>>> code
15
>>> first_name
'Robert'
>>> last_name
'Palmer'
>>> is_rock_star
True
>>> 
```

Value swapping is a common problem to solve in programming. Usually it requires creation of a temporary variable to hold one of the values during the process of exchanging the values:

```
>>> x = 5
>>> y = 10
>>> print(f"x={x}, y={y}")
x=5, y=10
>>> # Now swap them:
>>> temp = x
>>> x = y
>>> y = temp
>>> print(f"x={x}, y={y}")
x=10, y=5
```

Tuple unpacking simplifies this procedure, and removes the need for a temporary variable:

```
>>> x = 5
>>> y = 10
>>> print(f"x={x}, y={y}")
>>> x, y = (y, x)
>>> print(f"x={x}, y={y}")
x=10, y=5
```

In the above example, the parentheses in `(y, x)` are optional, when the tuple context is unambiguous. The following would also work:

    x, y = y, x

However, when passing a tuple to a function, the parentheses must be included to avoid confusion. The following function call passes **two** arguments, a tuple and an integer, but the tuple itself also contains two elements:

    print((x, y), 5)

When we cover functions, later, it will become clear that tuples enable a function to return multiple values, in the form of a tuple, without having to create special objects (like C STRUCTs, or a Java class) to encapsulate multiple values:

    name, address, balance = get_customer_info(15)

## Lists and Dictionaries

One of reasons Python is so popular is that lists (arrays) and dictionaries (hash-maps) are built in, with no special coding or object instantiation necessary. On top of that, Python lists and dictionaries can contain a mix of any type of object.

### List

A list in Python is an object representing a collection of objects. It's what most languages call an "array", except its members can be any type of object, integers, strings, floats etc, or a mix of types. To create a list, use square brackets:

```
animals = []    # Creates an empty list
animals = ['Cat', 'Dog', 'Elephant']
mixed = [1, 2, 3.5, "hello"]
```

The members of a list can be anything, even more lists:

```
mixed = [1, 2, 3.5, "hello", ['red', 'blue', 'green'], ['mercury', 'venus', 'earth', 'mars']]
```

To retrieve any individual element of a list, subscript the list with an integer (zero-based) index enclosed in square brackets:

```
>>> mixed[0]
1
>>> mixed[1]
2
>>> mixed[3]
'hello'
>>> mixed[4]
['red', 'blue', 'green']
```

That last line returned a list, which can also be subscripted. To retrieve the 2nd member of that 5th member, you could chain subscripts:

```
>>> mixed[4][1]
'blue'
```

Lists can be sliced. A slice is a section of the list specified with a subscript of the form `[start:end:step]`. To return the 2nd, 3rd and 4th elements:

```
>>> mixed[1:4]
[2, 3.5, 'hello']
```

Note that the `end` index member is not included in the returned list. A subscript [5:10] returns five members at indices 5, 6, 7, 8 and 9, *but not 10*.

List objects have methods to manipluate its members:

```
>>> nums = [5, 3, 11, 2]
>>> nums.append(8)
>>> nums
[5, 3, 11, 2, 8]
```

To remove an element from the list, use the `del` keyword:

```
>>> del nums[2]  # Discard the 3rd member
>>> nums
[5, 3, 2, 8]
```

The `insert` method of list objects is user to insert a new member at a specific position:

```
>>> nums.insert(1, 1000)  # Insert 1000 as the 2nd member
>>> nums
[5, 1000, 3, 2, 8]
```

### Dictionaries

By far the most useful of all Python objects is the dictionary, which other languages call a "hash-map". A dictionary is a collection of key-value pairs, designed to be able to locate any key instantly (along with its associated value), regardless of how many items it contains. It does not have to iterate through all its items until it finds the requested key, as you would have to do with a list.

Dictionaries are enclosed in curly braces `{}`, with a comma separated list for items inside, where each item has the format `key: value`:

```
my_dict = {}    # The empty dictionary
greetings = {1: "hello", 2: 'welcome', 3: 'goodbye'}
```

Values associated with keys can be any object. Keys can have almost any value or type, but they must be "hashable" (lists are not hashable, and cannot be keys) and unique within the dictionary:

```
my_dict = {-5: 'Moon', 'abc': 14.5, True: 'Yes'}
```

Like lists, dictionaries can be subscripted (but not sliced):

```
>>> my_dict = {-5: 'Moon', 'abc': 14.5, True: 'Yes', False: 'No'}
>>> my_dict[-5]
'Moon'
>>> my_dict["abc"]
14.5
>>> my_dict[3 == 4]
'No'
>>> my_dict[3 <= 4]
'Yes'
```

To insert a key-value pair (an "item") into a dictionary:

```
>>> my_dict["new"] = "This was inserted"
>>> my_dict
{-5: 'Moon', 'abc': 14.5, True: 'Yes', False: 'No', 'new': 'This was inserted'}
```

To remove an item:

```
>>> del my_dict[-5]
>>> my_dict
{'abc': 14.5, True: 'Yes', False: 'No', 'new': 'This was inserted'}
```

List lists, dictionaries have methods to manipulate their member elements.

To remove an item from the dictionary, and return the associated value, use the `pop` method:

```
>>> v = my_dict.pop("abc")
>>> v
14.5
>>> my_dict
{True: 'Yes', False: 'No', 'new': 'This was inserted'}
```

To empty a dictionary:

```
>>> my_dict.clear()
>>> my_dict
{}
```
