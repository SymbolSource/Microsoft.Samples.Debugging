## MDbg Iron Python Extension: Getting Started

### Building the IronPython Extension:

The IronPython extension project is not built by default. You would need to execute the following sequence of steps in order to build this extension.

1. Download the binaries for IronPython from https://github.com/IronLanguages/ironpython2
2. Add a reference to IronPython.dll from the pythonExt project in this solution.
3. Finally, build the ironpython extension project (After adding reference to ironpython.dll, you can also have this project built by default. From the Visual Studio IDE, click on the Build menu and select the configuration manager. Click checkbox for PythonExt project).

### Basic commands for MDbg's IronPython Extension:

> **lo[ad]** : Loads an mdbg extension or python script file.

> **py[thon]** : Executes a single python command or expression.<br/>
> `py print 1+2`<br/>
> `py def MyAdd(a,b): return a + b`<br/>
> `py print MyAdd(1,2)`

> **pe[val]** : Evaluates a python expression and prints the result.<br/>
> `pe 1+2`<br/>
> `pe MyAdd(1,2)`<br/>

> **pyin[teractive]** : Enters python interactive mode, which drops user to a python prompt.<br/>
> To exit python interactive mode, enter `pyout`.

> **pyr[efresh]** : Reloads previously loaded and since modified python scripts.<br/>
> `pyr` : Displays a numbered list of all previously loaded and since modified python scripts<br/>
> `pyr all` : Reloads all previously loaded and since modified python scripts<br/>
> `pyr num [num [num ...]]` : Reloads scripts corresponding to numbers (in the list displayed if no arguments are entered)<br/>
> Example inputs: `pyr` ; `pyr all` ; `pyr 2` ; `pyr 1 3 5`

### Python Interactive Mode

The `pyin` command drops a user from the regular MDbg command line to a python prompt within MDbg. The prompt is a fully functional python prompt which also has access to the MDbg CommandBase class. This allows python code to access the MDbg object model.

Example: To print the name of the current process, in python interactive mode you can execute the following code:

    >>> print CommandBase.Debugger.Processes.Active.Name

To execute a regular MDbg command from the python prompt:

    >>> CommandBase.ExecuteCommand(<CommandName>)

e.g.:

    >>> CommandBase.ExecuteCommand(go)

Python is an interpreted language, so you can define variables, functions, etc. at the command line.

Example: To print the callstack:

    >>> callstack = CommandBase.Debugger.Processes.Active.Threads.Active.Frames
    >>> for frame in callstack:
    ...      print frame
    ...
    >>> 

This can also be done by defining a function at the command line to print the callstack:

    >>> def PrintStack():
    ...      for frame in CommandBase.Debugger.Processes.Active.Threads.Active.Frame:
    ...          print frame
    ...
    >>> PrintStack()

### Loading Python Scripts

Loading a python script is the equivalent of executing the code in that script in python interactive mode. Therefore, all code in scripts has access to the same variable, methods, etc. that python code executed in python interactive mode does. Once a script is loaded (executed), python code in python interactive mode and all other loaded scripts have access to the functions and classes defined in the newly loaded script, and vice versa. If a script is modified after it has been loaded, the user can reload the script using the pyrefresh command.

Steps to load a python script

1. Load the python extension (`load pythext`)
2. Load the python script. Specify the full path to the script (`load [full path to python script]`)

A sample script ([pyfuncs.py](pyfuncs.py)) has been included in this package.

### Tips for Writing Python Scripts

Using the IronPython implementation of the python language, python code can access all .NET libraries and use any CLS types. For example, if you want to access the `System.Int32.MaxValue` field, in a python script or at the MDbg python command line, enter this:

    from System import Int32
    maxval = Int32.MaxValue

Once you have imported the `System.Int32` type, you can also call any static functions that type has:

    myint = Int32.Parse(10)

You can also instantiate objects of imported types:

    from System.Collections import ArrayList
    mylist = ArrayList()
    mylist.Add(myobject)

Note that python does not use the new keyword to instantiate objects.

To import an entire namespace:

    from System.Collections import *

To add a directory to the python path:

    import sys
    sys.path.append(mydir)

To import a class library, mydir\mylib.dll :

    import clr
    import sys

    sys.path.append(mydir)
    clr.AddReferenceToFile("mylib.dll")
