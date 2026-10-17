# VPN Performance Measurements

Source: [ECE 4490/6490 Assignment 1 laboratory report](ECE449_Assignment1_Report.docx), sections 7.1 through 7.3.

## Test method

- Two Ubuntu virtual machines in an isolated Oracle VirtualBox Internal Network.
- VM1 ran the `iperf3` client and VM2 ran the server.
- WireGuard destination: `10.44.0.2`.
- OpenVPN destination: `10.55.0.2`.
- Five TCP throughput trials per VPN, each lasting ten seconds.
- The final **receiver** bitrate was recorded for every trial.
- Round trip latency was measured with `ping`.

## Recorded throughput

| Trial | WireGuard (Mbits/sec) | OpenVPN (Mbits/sec) |
| ---: | ---: | ---: |
| 1 | 74.0 | 250 |
| 2 | 73.0 | 213 |
| 3 | 73.5 | 256 |
| 4 | 74.6 | 249 |
| 5 | 75.1 | 214 |
| **Mean** | **74.04** | **236.40** |
| **Sample standard deviation** | **0.84** | **21.08** |

## Latency

| Metric | WireGuard | OpenVPN |
| --- | ---: | ---: |
| Average round trip time | 3.610 ms | 1.791 ms |
| Packet loss | 0% | 0% |

## Interpretation

OpenVPN achieved approximately 3.19 times the mean measured throughput of WireGuard and lower average latency in this experiment. WireGuard showed much less variation in throughput across the five trials.

These results describe this particular virtualized setup only. CPU scheduling, tunnel configuration, virtualization overhead, and implementation differences can affect performance. They do not establish that OpenVPN generally outperforms WireGuard.

The original report contains supporting `iperf3` and ping screenshots.
