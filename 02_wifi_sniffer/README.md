# Network Traffic Analysis and VPN Performance Comparison

**Course:** ECE 4490/6490, Assignment 1  
**Author:** Lorenzo Reyes  
**Environment:** Oracle VirtualBox, two Ubuntu Linux virtual machines  
**Status:** Completed laboratory, documented with report and screenshots

## Project overview

This laboratory investigated the visibility of unencrypted remote access traffic, the protection offered by SSH, and the operation and performance of two VPN implementations: WireGuard and OpenVPN. All experiments took place between two Ubuntu virtual machines connected through an isolated VirtualBox Internal Network.

The project includes packet analysis with Wireshark, VPN configuration and verification, Bash control scripts, and quantitative throughput and latency testing.

## Network architecture

| System | Isolated network address | Role |
| --- | --- | --- |
| VM1 | `192.168.50.10/24` | Client and VPN peer |
| VM2 | `192.168.50.20/24` | Server and VPN peer |

The VirtualBox Internal Network was named `ece449lab`. Both virtual machines used static addresses on their isolated interfaces. ICMP connectivity was verified in both directions.

| Tunnel | VM1 | VM2 | Transport |
| --- | --- | --- | --- |
| WireGuard (`wg0`) | `10.44.0.1/24` | `10.44.0.2/24` | UDP 51820 |
| OpenVPN (`tun0`) | `10.55.0.1` | `10.55.0.2` | UDP 1194 |

## Experiments

### 1. Telnet versus SSH

Wireshark captured traffic on the isolated VM interface. A Telnet session over TCP port 23 exposed readable login information and terminal activity when inspected with Follow TCP Stream. An SSH session over TCP port 22 exposed connection metadata but not readable authentication data or terminal commands in the captured payload.

The report also documents a narrowly scoped Telnet capture filter and a display filter for client to server packets with nonzero TCP payload length.

### 2. WireGuard

Configured `wg0` interfaces on both VMs using peer public and private keys. Successful ping responses, a recent handshake, and increasing transfer counters verified tunnel operation. Wireshark showed the encapsulated UDP traffic on the underlying network.

### 3. OpenVPN

Configured a `tun0` tunnel between the VMs using self signed certificates, peer certificate SHA256 fingerprint verification, and TLS negotiation. ICMP testing verified the tunnel and Wireshark captured the underlying UDP traffic.

### 4. VPN automation

Created `vpnctl.sh` Bash control scripts on each VM to start and stop either VPN and stop the competing implementation when switching. The scripts are included in the laboratory report. See the report for the documented script contents.

### 5. Performance comparison

The experiment used `iperf3` for TCP throughput and `ping` for round trip latency. VM2 served the `iperf3` endpoint and VM1 acted as the client. Five ten second throughput trials were conducted per VPN, recording the receiver bitrate.

| Metric | WireGuard | OpenVPN |
| --- | ---: | ---: |
| Mean throughput | 74.04 Mbits/sec | 236.40 Mbits/sec |
| Sample standard deviation | 0.84 Mbits/sec | 21.08 Mbits/sec |
| Average round trip latency | 3.610 ms | 1.791 ms |
| Packet loss | 0% | 0% |

**Interpretation:** In this specific virtualized laboratory, OpenVPN had higher measured throughput and lower measured latency. WireGuard had lower throughput variation across the five trials. The results are environment specific and should not be generalized into a universal ranking of VPN implementations.

Detailed per trial data are in [VPN benchmark results](documentation/VPN_Benchmark_Results.md).

## Tools and technologies

Oracle VirtualBox, Ubuntu Linux, Wireshark, TCP/IP, Telnet, SSH, WireGuard, OpenVPN, Bash, iperf3, and ping.

## Documentation and evidence

- [Original 12 page laboratory report](documentation/ECE449_Assignment1_Report.docx)
- [Benchmark results and methodology](documentation/VPN_Benchmark_Results.md)
- [Virtual machine environment notes](vm_setup/README.md)
- [Screenshots](screenshots/)

The report contains 12 numbered figures documenting the network setup, traffic inspection, tunnel verification, and performance tests. The screenshots directory contains additional evidence.

## Reproduction and limitations

This repository documents a completed course laboratory, not a turnkey deployment. The original report does not specify every Ubuntu release, package version, VM hardware allocation, or full VPN configuration file. Those details are not invented here. Virtual machine images and private VPN keys are intentionally not distributed.

**Scope:** All traffic inspection and security demonstrations were conducted in an isolated, authorized virtual laboratory.
