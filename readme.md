## CLR Managed Debugger (mdbg) Sample 4.0

### Sample Overview

This sample provides the source files for CLR command line debugger, mdbg.  These sources demonstrate how to use the CLR Debugging interfaces.  As a corollary, they also show usage of the CLR MetaData, Symbol Store, and Process Publishing interfaces.

This debugger is also accompanied by five extensions that enhance its functionality: 
(Once built, simply type "load <file>" to load the desired extension.)

- [IronPython extension](./demo/IronPythonExtension/IronPython-Extension.md) that adds Python's scripting engine to mdbg (pythonExt)
- Winforms Graphical User Interface extension for easier debugging (gui)
- Edit & Continue extension for modification of debugged programs (enc)
- IL disassembler extension for display of IL code being executed (ildasm)
- Silverlight 4 debugging extension for mdbg (silverlight)

### Building the Sample

To build the mdbg sample you will need to have Visual Studio 2010 installed on your system. The sample must be built using the Visual Studio 2010 solution file.

- Open the mdbg.sln file.
- From the "Build" menu, select "Build Solution"
- The solution file uses "Debug" as the default, but you can simply select "Release" from the dropdown menu at the top if you want that instead.

**NOTE:** The IronPython extension project is not built by default. More details here - [IronPython Extension](./demo/IronPythonExtension/IronPython-Extension.md).

### Running the Sample

Run **mdbg.exe** from the bin directory, or by pressing F5 in Visual Studio.  Mdbg commands are similar to cordbg commands. Please refer to the cordbg manual, mdbg's help command, or the source code for more information on how to use various debugger commands.

Be sure to try the Graphical User Interface extension which makes debugging managed programs easier and more natural.  To load this extension simply type "load gui" on the mdbg command line.

This sample also contains API-level documentation for two libraries, mdbgeng.dll and mdbgext.dll.  Documentation for these libraries can be found in the DOC subdirectory.

### Feedback on the Sample

This sample is presented courtesy of the CLR Debugger Team. It is intended for use as a demonstration on writing .NET managed debuggers in managed code. If you have any questions about the sample or the managed debugging APIs, or if you would like to send us a suggestion about the sample, please participate in our [discussion forum](https://social.msdn.microsoft.com/Forums/vstudio/en-US/home?forum=clr).

### Links

[Visual Studio 2010 & .NET Framework 4](https://visualstudio.microsoft.com/)
