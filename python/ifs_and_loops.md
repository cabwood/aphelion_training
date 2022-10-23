# Code Blocks

Python is quite unique in that a block of code is "grouped together" into a block by sharing the same indentation level. Other languages, like C, use some kind of parentheses, like `{ instruction1; instruction2; ... }`

In Python you must use indentation. You may not mix tabs and spaces, but you may use either. Most programmers use 4, 8, 12 etc consecutive spaces to indent lines of Python code.

It's easiest to understand by example...

# Conditional Execution with if

The syntax to execute code conditionally is:

```
if <condition>:
    <line1 of some code to be executed if the condition is true>
    <line2 of to be executed if the condition is true>
    .
    .
    .
    <Last line of code to be executed if the condition is true>
<First line of code that is NOT part of the conditional block>
```

For example:

```
>>> x = 2
>>> y = 1
>>> if x > y:
...     print("x is greater than y")
... 
x is greater than y
```

An `else:` clause can be use to execute code if the condition is false:

```
>>> x = 2
>>> y = 2
>>> if x > y:
...     print("x is greater than y")
... else:
...     print("x is less than or equal to y")
... 
x is less than or equal to y
```

The `elif` keyword, short for "else if", is used to chain `if` statements together. Only one block of code, either the `if:` block, the `elif:` block or the `else` block can be executed:

```
>>> x = 2
>>> y = 2
>>> if x > y:
...     print("x is greater than y")
... elif x < y:
...     print("x is less than y")
... else:
...     # If x is neither greater nor less than y, they must be equal
...     print("x is equal to y")
... 
x is equal to y
```

You can use as many `elif:` tests as you want:

```
>>> age = 15
>>> if age < 3:
...     print("You can't even talk yet")
... elif age >= 3 and age < 6:
...     print("You are in kindergarten")
... elif age >= 6 and age < 11:
...     print("You are in primary school")
... elif age >= 11 and age < 17:
...     print("You are in secondary school")
... else:
...     print("Welcome to adulthood!")
... 
You are in secondary school
```

## Looping

### While Loops

The `while` keyword takes a single condition expression, and repeatedly executes the following code block until the condition evaulates to false. This code will print "Hello" 5 times:

```
count = 0
while count < 5:
    print("Hello")
    count = count + 1
```

At the Python prompt, this looks like:
```
>>> count = 0
>>> while count < 5:
...     print("Hello")
...     count = count + 1
... 
Hello
Hello
Hello
Hello
Hello
```

You can terminate the `while` loop prematurely using the `break` keyword. Here we search through a list to find the index of some item, or reach the end of the list. It isn't the best way to do this kind of thing, but it illustrates `break`:

```
lines = ['One', 'Two', 'Three', 'Four']
found = None
index = 0
while index < len(lines):
    if lines[index] == 'Three':
        found = index
        break
    index = index + 1
print(found)
```

If you wish to loop forever, you can use `while True:`, a condition which is never false, but you should probably include a break statement to test for some condition to end the loop. Here we ask the user to type lines of text, which we echo back, unless the user types "quit", in which case we terminated the looping:

```
>>> while True:
...     text = input()
...     if text == "quit":
...         break
...     print(f'You typed "{text}"')
... 
hello
You typed "hello"
goodbye
You typed "goodbye"
quit
>>> 
```

## For loops

To iterate through lists, or dictionary keys, use the `for...in` construct:

```
>>> for s in ["Hello", "Welcome", "Goodbye"]:
...     print(s)
... 
Hello
Welcome
Goodbye
```

Next, we iterate through items in a dictionary. Note that the `for` loop variable ("k" in this example) is assigned with *keys* of the dicionary, not the value parts. We are iterating through the keys, and then accessing the corresponding value by subscripting the dictionary object "singers".

```
singers = {
    1: "Robert Palmer",
    2: "Grace Jones",
    3: "Ariana Grande",
}

for k in singers:
    print(f"Singer number {k} is {singers[k]}")
```

This produces the following output:

```
Singer number 1 is Robert Palmer
Singer number 2 is Grace Jones
Singer number 3 is Ariana Grande
```

For loops can also use `break` to terminate them prematurely. Here we test if the value part of a dictionary member contains the text "Jones", and if so, terminate the loop before doing anything else:

```
singers = {
    1: "Robert Palmer",
    2: "Grace Jones",
    3: "Ariana Grande",
}

for k in singers:
    name = singers[k]
    if 'Jones' in name:
        break
    print(f"Singer number {k} is {name}")
```

The output is the single line:

```
Singer number 1 is Robert Palmer
```


Dictionaries have methods to facilitate iteration. For example the `values()` method returns a `generator` (which behaves much like a list, but is much more efficient), which can be iterated in a for loop:

```
>>> for v in {1: 'Hello', 2: 'Welcome', 3: 'Goodbye'}.values():
...     print(v)
... 
Hello
Welcome
Goodbye
```

The `items()` method of dictionaries returns a generator of tuples of the form (key, value):

```
>>> for item in {1: 'Hello', 2: 'Welcome', 3: 'Goodbye'}.items():
...     print(item)
... 
(1, 'Hello')
(2, 'Welcome')
(3, 'Goodbye')
```

You can take advantage of tuple unpacking to assign the key and value members of each tuple to indicidual variables simultaneously, like this:

```
>>> for k, v in {1: 'Hello', 2: 'Welcome', 3: 'Goodbye'}.items():
...     print(f"key={k}, value={v}")
... 
key=1, value=Hello
key=2, value=Welcome
key=3, value=Goodbye
```
