## Network Traffic Analysis

## Project Overview

This project documents my first practical network traffic investigation using Wireshark. The investigation is based on a training exercise from Malware-Traffic-Analysis.net and focuses on examining network traffic to identify potentially suspicious activity.

As an aspiring SOC analyst, I completed this exercise to develop my understanding of packet analysis, endpoint identification, suspicious network communications, and evidence-based investigation.

## Objectives

- Identify the endpoint of interest within the captured network traffic.
- Analyse HTTP requests and TLS handshake activity.
- Investigate an alleged executable file transfer.
- Document potential indicators of compromise (IOCs).
- Practise evidence-based investigation and reporting.

## Tools Used

- **Wireshark** — network packet capture analysis.
- **VirusTotal** — threat-intelligence lookup and file reputation research.
- **GitHub** — investigation documentation and portfolio development.

## Investigation Summary

During this investigation, I used Wireshark to identify an endpoint of interest and examine its network communications.

I investigated HTTP requests to an unfamiliar domain, reviewed TLS handshake activity, and examined network evidence relating to a suspicious Windows executable transfer involving an external IP address.

The findings raised concerns about potentially malicious activity. However, the available network evidence alone could not confirm whether the executable was downloaded and executed or establish the full extent of the suspected compromise.

## Skills Demonstrated

- Network traffic analysis
- Wireshark display filters
- Endpoint identification
- HTTP and TLS traffic investigation
- IOC documentation
- Threat-intelligence research
- Technical reporting and evidence handling

## Lesson Learned

Through this investigation, I learned how to use Wireshark to examine network traffic and identify an endpoint of interest within a PCAP file.

I gained a better understanding of how HTTP requests, TLS handshake activity, IP addresses, and network conversations can help an analyst investigate suspicious communications.

I also learned that identifying a suspicious file transfer does not automatically prove that a file was executed or that a system was compromised. Findings need to be supported by available evidence.

The exercise showed me areas where I still need to improve, particularly verifying file hashes and developing my understanding of DNS and encrypted traffic analysis.

## Project Files

- Investigation report: Detailed methodology, findings, IOCs, and lessons learned are documented in the report within this repository.
- Evidence screenshots: Screenshots supporting the investigation findings.

## References

- [Malware-Traffic-Analysis.net](https://www.malware-traffic-analysis.net/)
- [Wireshark User's Guide](https://www.wireshark.org/docs/wsug_html/)
- [VirusTotal](https://www.virustotal.com/)

