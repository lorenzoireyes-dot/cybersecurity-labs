# Stack Buffer Overflow and Control Flow Hijacking Laboratory

**Course:** ECE 4490/6490, Assignment 2  
**Platform:** Windows XP, 32 bit, Oracle VirtualBox  
**Status:** Completed and verified in the course laboratory; final documentation archive

## Project overview

This laboratory investigated a stack based buffer overflow in the course supplied `VulnerableCode_2.exe`. By examining the vulnerable program in GDB, a crafted input file was used to overwrite stack frame data, redirect execution to the program's existing `ArcInjection()` function, and pass an attacker selected command to its `system()` call.

The demonstration was performed against an intentionally vulnerable executable in a controlled, isolated educational environment. The report documents the vulnerability, stack layout analysis, payload construction, debugging, and successful command execution.

## Environment and tools

| Component | Laboratory configuration |
| --- | --- |
| Virtualization | Oracle VirtualBox, course provided VM |
| Guest operating system | Windows XP, 32 bit, 512 MB RAM |
| Address randomization | ASLR disabled |
| Toolchain | Cygwin, GCC |
| Debugging | GDB 6.8.0 with command line and Insight GUI |
| Shell tools | `head`, `printf`, `od`, `seq`, `tr` |
| Target | Course supplied `VulnerableCode_2.exe` |

The target was built from `VulnerableCode_2.c` with `gcc -ggdb -O0 -Wall`.

## Vulnerability analysis

The targeted path is case 2, `VulnerableLocalData()`, which allocates a local integer array `BufOve[14]`. The program passes this array to `EnterDataToVulnerableBuffer()`, which reads four byte integers from a file and writes them into the array without enforcing its capacity.

In the observed stack frame, input exceeding the array reached the saved frame pointer and return address. Overwriting the return address redirected control flow to the existing `ArcInjection()` function, which calls `system()` using its argument. This reused existing executable code rather than injecting shellcode.

## Key engineering finding: function entry via RET versus CALL

The initial overwritten return address successfully transferred execution to `ArcInjection()`, but the command argument was incorrect.

GDB inspection established that the stack layout did not match the normal x86 function calling convention: entry through a corrupted `RET` does not push the return address that a normal `CALL` would supply. As a result, the first candidate argument was placed one stack word too early.

The final payload included a four byte placeholder occupying the callee's expected return address position, followed by the argument pointer at the expected `[ebp+8]` location. This corrected the function argument and allowed the intended command to execute.

The report also discusses little endian address encoding, a whitespace landing zone to tolerate limited stack address differences, and Cygwin path conventions.

## Verification and results

The report documents three stages of validation:

1. A GDB breakpoint confirmed that execution reached `ArcInjection()` and that its argument resolved to the intended command path.
2. After the `system()` call, the observed return value in `EAX` was zero, indicating successful shell command completion.
3. A separate proof of execution used a command that created `hack_success.txt`; the file was confirmed to exist afterward with a current timestamp.

The final exploit was developed and verified in GDB, where the laboratory's stack behavior was repeatable. This does not establish portability to other operating systems, compiler settings, or hardened environments.

## Other vulnerability classes examined

The report also identifies other intentionally unsafe paths in the supplied programs, including heap and global buffer overflows, indirect calls through a function pointer, uncontrolled recursion, and a format string vulnerability in the separate `VulnerableCode_1.c` example. These were analyzed as additional vulnerabilities, **not** presented as separately completed exploits.

## Evidence

- [Original assignment report](documentation/BufferOverflow_Assignment2_Report_Polished.docx)
- [Laboratory screenshots](screenshots/)
- [Virtual machine environment notes](vm_setup/README.md)

## Archive scope

The report and screenshots are the final portfolio deliverables. No separate exploit source, payload binary, or virtual machine image is distributed, and no additional uploads are planned. The report contains the original technical methodology and experimental observations.

This repository is a technical evidence archive rather than a turnkey reproducible exploitation environment.
