# VirtualBox Laboratory Environment

This file records the environment actually described in the [laboratory report](../documentation/ECE449_Assignment1_Report.docx). It is an architecture and configuration reference, **not** a fully verified step by step installation guide.

## Host and guests

- Virtualization platform: Oracle VirtualBox
- Guest operating systems: Ubuntu Linux on two virtual machines
- Virtual network mode: Internal Network
- Internal Network name: `ece449lab`
- VM1 role: client and VPN peer
- VM2 role: server and VPN peer

The report does not identify the exact Ubuntu version, VirtualBox version, CPU/RAM allocation, or adapter device names. These values are deliberately omitted.

## Network addressing

| Interface / network | VM1 | VM2 |
| --- | --- | --- |
| Isolated VirtualBox network | `192.168.50.10/24` | `192.168.50.20/24` |
| WireGuard `wg0` | `10.44.0.1/24` | `10.44.0.2/24` |
| OpenVPN `tun0` | `10.55.0.1` | `10.55.0.2` |

The base isolated network was verified with ICMP echo requests in both directions.

## Software used

- Wireshark for packet inspection and TCP stream reconstruction
- Telnet and SSH for contrasting unencrypted and encrypted remote terminal sessions
- WireGuard with UDP port 51820
- OpenVPN with UDP port 1194 and certificate based peer authentication
- `iperf3` for TCP throughput measurements
- `ping` for connectivity and round trip latency
- Bash scripts named `vpnctl.sh` for tunnel start and stop operations

## Relevant Wireshark display filters

```text
tcp.port == 23
tcp.port == 22
udp.port == 51820
udp.port == 1194
```

The report also gives a Telnet client to server capture filter:

```text
src host 192.168.50.10 and dst host 192.168.50.20 and tcp dst port 23
```

And a more restrictive Wireshark display filter:

```text
ip.src == 192.168.50.10 &&
ip.dst == 192.168.50.20 &&
tcp.dstport == 23 &&
tcp.len > 0
```

## Tunnel verification

- WireGuard: verify `wg0`, peer handshake, transfer counters, and ICMP to `10.44.0.2`.
- OpenVPN: verify TLS negotiation, `tun0`, and ICMP between `10.55.0.1` and `10.55.0.2`.
- Inspect encrypted UDP traffic on the underlying isolated network using Wireshark.

## Reproducibility boundaries

The report does not include complete VPN configuration files, certificates, private keys, or package installation history. Reproducing the lab requires independently configuring those components and validating them in an authorized isolated environment. Do not upload live credentials, private keys, raw packet captures containing sensitive data, or VM disk images.
