---
title: "DHCP Lease-Time Covert Channel: A Novel Approach to Network Steganography"
date: 2026-08-18
draft: false
tags: ["coursework", "cybersecurity", "networking", "python", "research"]
---

## Overview

During my coursework in covert communications at RIT, I had the opportunity to work on a research project that explored an unique area of network security: leveraging the DHCP lease-time parameter as a covert communication channel. This post documents a collaborative research effort that demonstrates how a common, trusted protocol can be weaponized for hidden data exfiltration, and more importantly, why defenders need to pay closer attention to protocol fields we often take for granted.

*This project was completed in collaboration with my collegaues Cayden Wright, Kelly Orjiude, and Chris Baudouin.*

---

## What is a Covert Channel?

A **covert channel** is a communication mechanism that exploits legitimate systems or protocols to transmit data without detection. Rather than using an obvious attack vector, covert channels hide information "in plain sight" by leveraging trusted infrastructure.

There are two primary classifications:

- **Storage Channels:** Hide data within system attributes or protocol fields
- **Timing Channels:** Manipulate the timing of events to encode information

Our research focused on a semantic storage channel — one that modifies data within a protocol while maintaining protocol compliance. The beauty of this approach is that it doesn't break the protocol; it just uses fields in ways they weren't intended.

---

## The Target: DHCP and the Lease-Time Field

DHCP (Dynamic Host Configuration Protocol) is fundamental to network operations. Every device that connects to a network needs an IP address, and DHCP automates this process through the **DORA** handshake:

1. **Discover** — Client broadcasts a request for an IP address
2. **Offer** — DHCP server responds with an available IP
3. **Request** — Client confirms the offered IP
4. **Acknowledge** — Server confirms the assignment

As part of this exchange, the server includes a **lease time** — the duration for which the client can use the assigned IP address before renewal. Lease times typically range from hours to days depending on network policy. This parameter is designed to balance network efficiency with IP availability.

This is where we saw an opportunity.

---

## The Approach: Modulating Lease Time

While previous DHCP covert channels exploited fields such as the transaction ID or hostname, we focused specifically on the lease-time parameter. Lease time varies legitimately in normal networks, making it a plausible candidate for data encoding without raising immediate red flags.

**How it works:**

- Each character in our message is encoded as its ASCII decimal value
- We transmit DHCP Discover packets with the lease-time field set to match that ASCII value
- Control signals (lease time of 0 or 1) mark the beginning and end of transmission
- The receiver passively listens to DHCP traffic, extracts lease times, and reconstructs the message

For example, to send the letter "C" (ASCII 67), we craft a DHCP Discover packet with a lease duration of 67 seconds. To the network, it appears as legitimate DHCP traffic — just with an unusually short lease.

---

## Implementation: Python and Scapy

We built this proof-of-concept using **Python** and the **Scapy** library, a powerful packet manipulation tool. Scapy allowed us to craft raw DHCP Discover packets with arbitrary values, set custom lease-time fields, control inter-packet timing, and build both sender and receiver components.

**The sender process:**
1. Accept message input (text or file, with Base64 encoding for binary data)
2. Transmit a control signal indicating message type (0 for text, 1 for file)
3. Loop through each character, creating a DHCP Discover packet with the ASCII value as lease time
4. Introduce configurable delays between packets to mimic normal client behavior
5. Send a termination signal

**The receiver process:**
1. Listen passively for DHCP Discover packets
2. Extract the lease-time value from each packet
3. Build a list of values until a control signal is detected
4. Convert values back to ASCII characters and reconstruct the message
5. Output to terminal or file depending on message type

The entire system is deterministic — no clock synchronization needed, no additional handshaking required.

---

## Evaluation: Throughput, Reliability, and Stealth

We tested the channel in a controlled environment using virtual machines on the same network.

**Throughput:** Limited but functional. At one packet per second, a 100-character message takes roughly 102 seconds to transmit. Slow, but sufficient for low-bandwidth scenarios like credential exfiltration or C2 signaling.

**Reliability:** Directly correlated with packet loss.

| Packet Loss | Message Success Rate |
|---|---|
| 0% | 100% |
| 10% | 90% |
| 20% | 80% |

If a control signal is dropped, the transmission fails. In a real scenario, redundant receivers could mitigate this.

**Detectability:** The channel exhibits moderate stealth.

Observable anomalies:
- Standard leases are hours or days — ours are 0–255 seconds, easily flagged by baseline analysis
- Legitimate clients send DHCP messages at boot or renewal intervals; we generate rapid sequences
- A lease time of 0 or 1 second is particularly suspicious — no real DHCP server would assign these

However:
- Packets remain protocol-compliant and structurally valid
- In networks without DHCP-specific monitoring, the channel blends with normal traffic
- Standard IDS/IPS tools don't typically inspect DHCP fields deeply

---

## Defensive Implications

Most organizations monitor traffic at the application layer (DNS, HTTP, etc.) but treat DHCP as a trusted, transparent protocol. This creates a blind spot.

Effective countermeasures include:

- **Lease-time baselining:** Establish normal lease-time distributions and flag deviations
- **Message-rate analysis:** Monitor for abnormally high frequencies of Discover packets
- **Strict lease policies:** Enforce minimum lease durations and reject extremely short requests
- **DHCP Snooping:** Switch-level protections to validate traffic and prevent rogue servers
- **Cross-correlation:** Correlate DHCP activity with ARP, DNS, and authentication logs

---

## Key Takeaways

**Trust is a vulnerability.** DHCP is ubiquitous and trusted, which makes it an attractive target for covert communication. Defenders must extend monitoring beyond the protocols they expect to be attacked.

**Semantic channels are subtle.** By encoding data within legitimate fields rather than breaking protocol structure, we avoided syntax-level detection.

**Low-bandwidth is still useful.** Exfiltrating a single API key, authentication token, or C2 command doesn't require high throughput. Sometimes covertness matters more than speed.

**Novel doesn't mean complex.** This research succeeded by focusing on an overlooked field rather than inventing new techniques. The best security research often identifies gaps in existing assumptions.

---

## Conclusion

This project sits at the intersection of offensive and defensive security research. By demonstrating a new attack vector, we aimed to raise awareness about the importance of comprehensive protocol monitoring. Network security isn't just about blocking bad domains or detecting malware — it's about understanding how legitimate infrastructure can be misused.

The work also serves as a reminder that security research requires both creativity and rigor. We didn't just identify an idea — we implemented it, tested it under various conditions, and evaluated its real-world detectability. That combination is what separates academic curiosity from actionable security knowledge.