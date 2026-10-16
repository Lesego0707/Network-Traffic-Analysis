# Wireshark Malware Traffic Analysis

## Project Overview

This project documents my first practical network traffic investigation using Wireshark. The investigation is based on a training exercise from Malware-Traffic-Analysis.net and focuses on identifying suspicious network activity through packet analysis.

As SOC Analyst, I created this project to develop my network investigation, threat identification, and technical reporting skills.

## Objectives

- Identify the endpoint of interest within the captured network traffic.
- Analyse HTTP requests and TLS handshake activity.
- Investigate an apparent executable file transfer.
- Document potential indicators of compromise (IOCs).
- Practise evidence-based investigation and reporting.

## Tools Used

- **Wireshark** — network packet capture analysis.
- **VirusTotal** — threat-intelligence lookup and file reputation research.
- **GitHub** — investigation documentation and portfolio development.

## Investigation Summary

During the investigation, I identified an internal endpoint and examined its network communications. I investigated HTTP requests to an unfamiliar domain, subsequent TLS handshake activity, and an apparent Windows executable transfer involving an external IP address.

These observations warranted further investigation. The executable's SHA-256 hash remains pending verification, and the available network evidence does not independently establish whether the file was executed or confirm the full extent of any compromise.

## Skills Demonstrated

- Network traffic analysis
- Wireshark display filters
- Endpoint identification
- HTTP and TLS traffic investigation
- IOC documentation
- Threat-intelligence research
- Technical reporting and evidence handling

## Key Learning Outcomes

This project strengthened my understanding of analysing network events chronologically, validating suspicious indicators, distinguishing observations from assumptions, and documenting investigation limitations.

I also identified areas for improvement, including file-hash verification and further analysis of DNS and encrypted traffic.

## Project Files

- **Investigation report:** Detailed methodology, findings, IOCs, and lessons learned are documented in the report within this repository.
- **Evidence screenshots:** Screenshots support the investigation findings.

## Safety and Scope

This project is for educational and defensive cybersecurity learning. Suspicious activity is described cautiously, and indicators are not treated as confirmed malicious without sufficient supporting evidence. No malware execution was required for this investigation.

## References

- [Malware-Traffic-Analysis.net](https://www.malware-traffic-analysis.net/)
- [Wireshark User's Guide](https://www.wireshark.org/docs/wsug_html/)
- [VirusTotal](https://www.virustotal.com/)
