# Cybersecurity Labs

A portfolio archive documenting completed educational cybersecurity experiments in stack memory corruption, network traffic analysis, encrypted communications, and VPN performance testing.

## Projects

### [01 | Stack Buffer Overflow and Control Flow Hijacking](01_buffer_overflow/README.md)

**ECE 4490/6490, Assignment 2.** Analyzed an unchecked stack buffer in a course supplied Windows XP executable, used GDB to investigate the saved return address and x86 calling convention, redirected execution to an existing function, and verified command execution. The report explains the key debugging finding involving a missing return address slot when entering a function through `RET` instead of `CALL`.

[Read the buffer overflow laboratory documentation](01_buffer_overflow/README.md).

### [02 | Network Traffic Analysis and VPN Performance Comparison](02_wifi_sniffer/README.md)

**ECE 4490/6490, Assignment 1.** Used two Ubuntu virtual machines on an isolated Oracle VirtualBox network to examine Telnet and SSH traffic in Wireshark, configure WireGuard and OpenVPN, automate VPN switching with Bash, and compare measured throughput and latency.

[Read the network security laboratory documentation](02_wifi_sniffer/README.md).

### [03 | Virus Propagation and Binary Self Modification Laboratory](03_virus_propagation/README.md)

**ECE 4490/6490, virus propagation assignment.** Extended instructor provided C code in an isolated Windows XP VM to examine NTFS Alternate Data Streams, executable directory scanning, repeat infection detection, preservation of host program behavior, and binary hash variation. The public archive documents the experiment but does not distribute operational malware.

[Read the virus propagation laboratory documentation](03_virus_propagation/README.md).

## Documentation policy

The existing two assignments are complete portfolio archives supported by their original reports and screenshots. No additional source files, VM exports, raw packet captures, or configuration uploads are planned. Some directories remain empty from the initial repository organization and do not represent outstanding deliverables.

The archives document verified laboratory results but are not distributed as fully reproducible VM packages. Unrecorded environment details are not invented.

## Laboratory scope

These experiments were conducted in controlled educational environments. The repository does not distribute VM disks, private keys, credentials, or sensitive network captures.
