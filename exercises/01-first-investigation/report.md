## Network Traffic Analysis 

## Exercise Information

-Exercise name: Malware analysis 2026-10-01

-Exercise source: Malware-Traffic-Analysis.net

-Analysis date: 2026-10-14

-Tools: Wireshark and Virus Total

## Summary
This investigation examines a packet capture containing suspicious network activity involving an internal endpoint in the natureforce.com network environment.
The investigation identified a potential victim host, observed HTTP communication with an unfamiliar external domain, identified subsequent TLS connections, and observed an apparent Windows executable transfer from an external IP address over a non-standard port.
These observations are consistent with a suspected malware delivery incident. Further validation is required to establish the executable's maliciousness, determine whether it was executed, and confirm the extent of the endpoint compromised

Identified Hosts
-Victim IP Address: 10.10.1.128
-Victim Mac address: 00:22:fb:ec:7e:e7
-Victim Hostname: DESKTOP-4VGYQX7
-User account name of the victim: bdiaz
-SHA-256 hash of the Windows EXE file sent from 107.175.82.242: 

Step-by-step investigations.

## Step 1: Identifying the Potential Victim

I began by examining the IPv4 endpoints in Wireshark under Statistics → Endpoints. I reviewed the communicating hosts and their traffic volumes to identify endpoints that warranted further investigation.
The internal IP address 10.10.1.128 stood out as a host of interest based on the observed network activity.
I then used DHCP traffic to investigate the host's network configuration and identify its hostname. Kerberos authentication traffic provided additional information associated with the user account.
Filters used:
## dhcp — inspect DHCP messages.
## kerberos.CNameString — inspect Kerberos client-name fields.
Evidence:
<img width="214" height="43" alt="host name" src="https://github.com/user-attachments/assets/194f4cc0-621d-4052-907c-77ad6bdfa48d" />
<img width="178" height="17" alt="User name" src="https://github.com/user-attachments/assets/d5c6120c-4dbc-4037-b4fa-e83e8b313c4d" />

## Finding: The host under investigation was identified as DESKTOP-4VGYQX7, associated with IP address 10.10.1.128 and user account bdiaz.

 ## Step 2: Investigating the Initial HTTP Activity

I filtered the capture for HTTP requests to investigate the web activity preceding the subsequent network connections.
Filter used:http.request
The investigation revealed an HTTP request to the unfamiliar domain holtandberyl.com. The server returned an HTML webpage, and the observed traffic included requests involving the paths /pre and /CRV.
This sequence warranted further investigation because it preceded additional suspicious network activity.
The domain and request paths should be treated as suspicious indicators requiring validation rather than proof of malicious activity on their own.
Evidence:
<img width="207" height="26" alt="http request" src="https://github.com/user-attachments/assets/62c73bcc-4f3e-4b0f-93be-4c91ac1e6656" />
<img width="457" height="29" alt="html webpage" src="https://github.com/user-attachments/assets/d60fd9c1-3fdf-4be7-9ea8-5221fcda444c" />

## Finding: The victim host communicated with an unfamiliar external website before the other suspicious connections observed in the capture.

## Step 3:Examining Subsequent TLS Connections

After the HTTP activity, I investigated subsequent encrypted network connections originating from the suspected victim.
Filter used:
tls.handshake.type == 1 && ip.src == 10.10.1.128
This filter isolates TLS ClientHello packets originating from the victim IP address. A ClientHello indicates an attempt to initiate a TLS handshake.
The observed TLS activity followed the earlier HTTP requests. This temporal relationship is relevant to the investigation, although the handshake alone does not establish the purpose or maliciousness of the connection.
Further investigation of destination IP addresses, DNS activity, TLS metadata, and the surrounding packet timeline would help determine whether these connections were associated with the suspected incident.
Evidence:
<img width="419" height="109" alt="TLS handshake" src="https://github.com/user-attachments/assets/68c71fe7-d0b9-4dfe-9147-eae59ba299aa" />

## Finding: The victim initiated TLS handshakes after the observed HTTP activity. The purpose of the encrypted connections requires further investigation.

## Step 4: Investigating the Executable Transfer

Further analysis revealed communication between the victim host and the external IP address 107.175.82.242 over a reported non-standard port.
The packet capture appeared to contain a transfer of a Windows executable (.exe) over this connection.
The transfer is a significant investigative lead because executable downloads can represent malware delivery. However, the file's contents, SHA-256 hash, and reputation must be examined before its maliciousness can be confirmed.
Investigation points:
Source host: 10.10.1.128
External IP address: 107.175.82.242
Reported destination port: 9000 — verify against the packet details.
Observed artifact: Windows executable (.exe)
Evidence:
<img width="531" height="15" alt="port 9000 ( exe file)" src="https://github.com/user-attachments/assets/a8f0e942-fbc0-42ea-a924-f9c4a5e9ea79" />

##Finding: The capture contains evidence of an apparent executable transfer involving an external host. The file should be extracted safely, hashed, and assessed using appropriate malware-analysis procedures.

## Indicators of Compromise (IoCs)

-Internal IP: 10.10.1.128 - Suspected victim host
-Hostname: DESKTOP-4VGYQX7 - Host associated with the investigation
-User account :bdiaz - Account associated with the host
-Domain: holtandberyl.com - Suspicious domain observed in HTTP traffic
-IP address: 35.170.55.9 - Reported IP associated with the suspicious domain; verify using DNS evidence
-IP address: 107.175.82.242 - External host involved in the reported executable transfer
-Port:9000 - Reported port associated with the transfer, verify against the capture

## Lesson Learned

- Learned to use Wireshark endpoints and protocol filters to identify hosts and investigate suspicious network activity.
-Improved my understanding of HTTP requests, TLS handshakes, and analysing network events chronologically.
-Learned that suspicious file transfers and network indicators require further validation before confirming malicious activity.
-Recognised the importance of evidence-based reporting and safe malware handling.

9. Areas for Improvement

-Improve my ability to identify and validate file hashes and indicators of compromise (IOCs).
-Develop stronger skills in analysing DNS, TLS, and executable-transfer traffic.
-Practise correlating packet evidence with threat-intelligence sources.
-Improve my confidence in documenting findings and distinguishing confirmed evidence from assumptions.

Reflection: I was unable to independently verify the executable's SHA-256 hash during this investigation. This highlighted the need to strengthen my file-identification and threat-intelligence research skills.

## References
-Malware-Traffic-Analysis.net
-Wireshark User's Guide
-VirusTotal



