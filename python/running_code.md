# Running Python

We will focus on Python version 3.

# Command line interpreter

Like Linux bash, Python comes with an interpreter. typing this command at the bash prompt:

    python3

will start the Python (version 3) interpreter, which is useful for trying out simple instructions or testing short Python scripts. You'll be presented with the python `>>>` prompt:

```
Python 3.10.6 (main, Aug 10 2022, 11:40:04) [GCC 11.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

To exit from the Python interpreter, and return to bash, call the `exit` function:

```
>>> exit()
```

To exit with a single keystroke, type `Ctrl+D`

You wouldn't use this interpreter to write Python programs, but it's very useful to try out python instructions and short scripts to see their results immediately, without having to create and execute `.py` files. To try the `print` function, for example, at the `>>>` prompt type:

```
>>> print("Hello World!")
Hello World!
```

In the rest of these notes, I'll be using the interpreter a lot, to demonstrate certain concepts, since the result of execution of an instruction is displayed immediately after pressing the `Enter` key. You'll know when I am using the interpreter, because I copy and paste the instruction(s) and result directly from my terminal, which will include the `>>>` prompt.

The instruction doesn't have to be a function which returns a value. Typing an expression at the `>>>` prompt will evaluate the expression and display the result:

```
>>> 2 + 3
5
>>> 4.5 / 3
1.5
>>> "Hello" + " " + "World!"
'Hello World!'
```

# Program Files

A Python program file will usually have the extension `.py`, and contain multiple Python instructions. Python program files (also called "modules") do not have to be compiled, and to execute them you simply run the python3 command at the bash prompt, with the file path as its only argument. If you have a file `/home/aphelion/squares.py`, it can be executed from the bash prompt like this:

    python3 /home/aphelion/squares.py

If the PWD is `/home/aphelion`, of course that command could be abbreviated to:

    python3 squares.py

