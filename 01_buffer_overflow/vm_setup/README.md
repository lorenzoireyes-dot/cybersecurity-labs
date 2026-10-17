# Virtual Machine Environment

This file summarizes the environment described in the [original laboratory report](../documentation/BufferOverflow_Assignment2_Report_Polished.docx). It is an environment record, not a complete installation guide.

| Component | Reported configuration |
| --- | --- |
| Virtualization | Oracle VirtualBox, course provided image |
| Guest OS | Windows XP, 32 bit |
| Guest memory | 512 MB RAM |
| ASLR | Disabled |
| Toolchain | Cygwin, GCC |
| Debugger | GDB 6.8.0, including Insight GUI |
| Shell utilities | `head`, `printf`, `od`, `seq`, `tr` |
| Target program | `VulnerableCode_2.exe` |

The target was compiled from the course supplied `VulnerableCode_2.c` using `gcc -ggdb -O0 -Wall`.

The report documents a demonstration using GDB and a crafted input file against case 2, `VulnerableLocalData()`. It also describes the observed stack layout and command execution verification.

**Archive policy:** No virtual machine image, exploit binary, or additional environment configuration will be uploaded. The original report and screenshots are the final evidence. This historical Windows XP environment is obsolete and should not be connected to untrusted networks.
