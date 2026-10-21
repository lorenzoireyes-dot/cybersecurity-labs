# Virus Propagation and Binary Self Modification Laboratory

**Course:** ECE 4490/6490, Network Security  
**Platform:** Windows XP, Oracle VirtualBox  
**Language and toolchain:** C, Cygwin GCC  
**Status:** Laboratory implementation and execution documented

## Project overview

This assignment examined executable file infection, preservation of host behavior, repeated directory scanning, detection of previously affected files, and binary self modification within an isolated Windows XP virtual machine.

The work began with instructor provided code that targeted one executable. The assignment extended that foundation to demonstrate additional behaviors and validate the results using test executables.

## Assignment requirements and implementation

| Requirement | Documented implementation |
| --- | --- |
| Preserve original host behavior | Use NTFS Alternate Data Streams to retain the original executable while demonstrating host execution |
| Resume original program execution | Restore and execute the preserved host program during the laboratory test |
| Scan for additional targets | Replace the original single file target with directory enumeration of executable files |
| Avoid repeated infection | Check for a marker associated with prior processing and skip previously affected targets |
| Demonstrate binary variation | Append variable trailing data to change the executable's file hash between executions |

The final item demonstrates binary mutation and hash variation; it does not by itself establish full code polymorphism.

## Laboratory environment

| Component | Configuration |
| --- | --- |
| Guest operating system | Windows XP |
| Virtualization | Oracle VirtualBox |
| Network | Disconnected during testing |
| Language | C |
| Compiler | GCC through Cygwin |
| Documented test files | `helloWorld.exe`, `test1.exe`, `test2.exe`, `test3.exe` |

## Execution and verification

The original report records two execution passes. During the first pass, the program processed the test executables and demonstrated the original host program behavior. On the second pass, it identified the previously processed files and reported that those targets were skipped.

These results are observations from the documented laboratory, not evidence of operation across other operating systems or protected environments.

## Evidence and documentation

The original course report describes the five requirements, implementation details, environment, and observed first and second execution results. Execution screenshots should be added to the `screenshots/` directory after review for sensitive paths and unrelated information.

The original report has been retained locally; it is not yet attached to this repository directory.

## Distribution and safety scope

The experiment was conducted in a disconnected, controlled educational VM. This public repository documents learning outcomes and experimental observations, but does not publish the operational virus source code, executable files, infected samples, or VM image.

This is an academic laboratory record rather than a runnable malware distribution.
