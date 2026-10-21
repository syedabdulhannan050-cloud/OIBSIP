# Task 8: Capture Network Traffic with Wireshark

## 1. Project Overview

This project uses Wireshark to capture and analyze network traffic on my own computer. I applied display filters to examine DNS, HTTP, and TCP packets and studied how a TCP connection is established.

## 2. Objective

- Capture live network traffic for at least two minutes.
- Filter and inspect DNS, HTTP, and TCP packets.
- Identify the TCP three-way handshake.
- Examine information visible in HTTP traffic.
- Understand the security risks of unencrypted communication.

## 3. Tools Used

- **Wireshark:** Network protocol analyzer.
- **Operating system:** Windows.
- **Network interface:** My active local network interface.

## 4. Methodology

1. Installed Wireshark and prepared it to capture network traffic.
2. Captured live traffic for at least two minutes.
3. Applied the `dns` display filter to inspect DNS packets.
4. Applied TCP filters to identify SYN, SYN-ACK, and ACK packets from the same connection.
5. Applied the `http` display filter to inspect HTTP packets.
6. Saved the capture as `wireshark_capture.pcap`.

## 5. Filters Used

| Display filter | Purpose |
|---|---|
| `dns` | Displays DNS packets. |
| `http` | Displays HTTP packets. |
| `tcp` | Displays TCP packets. |
| `tcp.flags.syn == 1 && tcp.flags.ack == 0` | Finds initial SYN packets. |
| `tcp.flags.syn == 1 && tcp.flags.ack == 1` | Finds SYN-ACK packets. |
| `tcp.flags.ack == 1 && tcp.flags.syn == 0` | Finds ACK packets, including ordinary ACKs. |

## 6. TCP Three-Way Handshake

The TCP three-way handshake establishes a connection between a client and a server.

1. **SYN:** The client requests a connection.
2. **SYN-ACK:** The server responds and acknowledges the request.
3. **ACK:** The client acknowledges the server's response.

I identified a matching sequence of SYN, SYN-ACK, and ACK packets in the captured traffic.

## 7. HTTP Security Observation

The `http` filter displayed HTTP packet rows in my capture. I inspected an HTTP packet and its protocol details.

HTTP traffic is not encrypted by itself. Depending on the request, an observer with access to the traffic may be able to read information such as the requested hostname, URL path, headers, and transmitted content.

**Finding:** The capture contained HTTP packets. The exact visible information should be documented from the inspected packet, without including sensitive data.

## 8. Why HTTP Is Dangerous and How HTTPS Helps

HTTP sends application data without encryption. An attacker who can intercept the traffic may be able to read or manipulate it.

HTTPS uses TLS to encrypt data exchanged between the client and server. This helps protect confidentiality and detect tampering, while also authenticating the server through its certificate. HTTPS does not make every website or endpoint automatically safe, but it protects the connection against many forms of network eavesdropping.

## 9. Glossary

- **Packet:** A small unit of data sent across a network.
- **Protocol:** A set of rules that devices follow to communicate.
- **Port:** A number used to direct network traffic to a particular service or application.
- **Payload:** The actual data carried inside a packet, apart from its protocol headers.
- **Handshake:** A sequence of messages used to establish a connection or agree on communication parameters.

## 10. Project Files

- `captures/wireshark_capture.pcap` — saved packet capture.
- `screenshots/` — screenshots showing installation, live capture, DNS filtering, TCP handshake, and HTTP packet inspection.

## 11. Ethical Considerations

I captured traffic from my own computer and used the
