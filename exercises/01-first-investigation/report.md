## Network Traffic Analysis 

## Exercise Information

-Exercise name: Malware analysis 2026-10-01

-Exercise source: Malware-Traffic-Analysis.net

-Analysis date: 2026-10-14

-Tools: Wireshark and Virus Total

## Summary
This investigation examines a packet capture containing suspicious network activity involving an internal endpoint in the natureforce.com network environment.
The investigation identified a potential victim host, observed HTTP communication with an unfamiliar external domain, identified subsequent TLS connections, and observed an apparent Windows executable transfer from an external IP address over a non-standard port.
These observations are consistent with a suspected malware delivery incident. Further validation is required to establish the executable's maliciousness, determine whether it was executed, and confirm the extent of the endpoint compromised.

## Identified Hosts

-Victim IP Address: 10.10.1.128

-Victim Mac address: 00:22:fb:ec:7e:e7

-Victim Hostname: DESKTOP-4VGYQX7

-User account name of the victim: bdiaz

-SHA-256 hash: Pending verification. The file hash could not be independently confirmed during this investigation.


## Step 1: Identifying the Potential Victim

**My Observation:**

I used Wireshark's Endpoints statistics to identify a host that stood out for further investigation. By examining the available DHCP and Kerberos traffic, I was able to identify the host as DESKTOP-4VGYQX7, with IP address 10.10.1.128 and the associated user account bdiaz.

Filters used:
## dhcp — inspect DHCP messages.
## kerberos.CNameString — inspect Kerberos client-name fields.

Evidence:
<img width="214" height="43" alt="host name" src="https://github.com/user-attachments/assets/194f4cc0-621d-4052-907c-77ad6bdfa48d" />
<img width="178" height="17" alt="User name" src="https://github.com/user-attachments/assets/d5c6120c-4dbc-4037-b4fa-e83e8b313c4d" />

## Finding: The host under investigation was identified as DESKTOP-4VGYQX7, associated with IP address 10.10.1.128 and user account bdiaz.

 ## Step 2: Investigating the Initial HTTP Activity

**My Observation:**

I noticed that the identified host made an HTTP request to holtandberyl.com. The domain was unfamiliar in the context of the investigation, so I considered it worth looking into. I also noticed requests involving the paths /prw and /CRV. These observations raised questions about the host's web activity, but did not prove that the domain was malicious.

Evidence:

<img width="207" height="26" alt="http request" src="https://github.com/user-attachments/assets/62c73bcc-4f3e-4b0f-93be-4c91ac1e6656" />

<img width="457" height="29" alt="html webpage" src="https://github.com/user-attachments/assets/d60fd9c1-3fdf-4be7-9ea8-5221fcda444c" />

## Finding: The victim host communicated with an unfamiliar external website before the other suspicious connections observed in the capture.

## Step 3:Examining Subsequent TLS Connections

**My Observation:**

After examining the HTTP activity, I looked at the TLS connections originating from the suspected victim. I found ClientHello packets showing that the host attempted to establish TLS connections after the earlier HTTP requests. This helped me understand the sequence of network activity, although I could not determine what was communicated through the encrypted connections from the handshake information alone.

Evidence:

<img width="419" height="109" alt="TLS handshake" src="https://github.com/user-attachments/assets/68c71fe7-d0b9-4dfe-9147-eae59ba299aa" />

## Finding: The victim initiated TLS handshakes after the observed HTTP activity.

## Step 4: Investigating the Executable Transfer

**My Observation:**

The part that caught my attention most was the apparent transfer of a Windows executable between the victim host and the external IP address 107.175.82.242 over the reported port 9000. This raised concerns because executable files can be used to deliver malware. However, I could not establish from the available evidence whether the file was executed or whether the endpoint was successfully compromised.

Investigation points:

-Source host: 10.10.1.128

-External IP address: 107.175.82.242

-Reported destination port: 9000 - verify against the packet details.

-Observed artifact: Windows executable (.exe)

Evidence:

<img width="531" height="15" alt="port 9000 ( exe file)" src="https://github.com/user-attachments/assets/a8f0e942-fbc0-42ea-a924-f9c4a5e9ea79" />

## Finding: The capture contains evidence of an apparent executable transfer involving an external host. 

## Indicators of Compromise (IoCs)

-Internal IP: 10.10.1.128 - Suspected victim host

-Hostname: DESKTOP-4VGYQX7 - Host associated with the investigation

-User account : bdiaz - Account associated with the host

-Domain: holtandberyl.com - Suspicious domain observed in HTTP traffic

-IP address: 35.170.55.9 - Reported IP associated with the suspicious domain; verify using DNS evidence

-IP address: 107.175.82.242 - External host involved in the reported executable transfer

-Port: 9000 - Reported port associated with the transfer, verify against the capture


## Analyst Conclusion

Based on my investigation of the packet capture, I identified network activity that raised concerns about a possible malware delivery incident.

The main findings included HTTP communication with an unfamiliar external domain, subsequent TLS connection attempts, and an apparent Windows executable transfer involving the external IP address 107.175.82.242 over the reported port 9000.

These findings gave me reason to treat the activity as suspicious and worthy of further investigation. However, I could not confirm whether the executable was malicious, whether it was executed, or whether the endpoint was compromised.

I would recommend further examination of the transferred file, verification of its SHA-256 hash, and additional endpoint investigation before making a final determination.

This investigation helped me understand how different pieces of network evidence can be examined together to build a picture of potentially suspicious activity.


## Lesson learned

This investigation helped me become more comfortable using Wireshark to examine network traffic. I learned how to use the Endpoints statistics to identify a host of interest and how DHCP and Kerberos traffic can provide useful information about a device and its associated user account.

I also gained a better understanding of HTTP requests and how to identify the domains a device communicates with. Examining the TLS ClientHello packets helped me understand how to follow connection attempts and why encrypted traffic can limit what an analyst is able to see.

One of the most important things I learned was that an apparent executable transfer deserves attention, but it does not automatically mean that malware was successfully installed or executed. I had to be careful not to make conclusions that the packet capture could not support.

I also faced a challenge when trying to independently verify the executable's SHA-256 hash. I learned that identifying a suspicious file is only part of the investigation; being able to verify and document its hash is also important.

Overall, this exercise taught me to approach network investigations step by step, pay attention to the available evidence, and recognise when further investigation is needed before reaching a conclusion.

 ## Areas for Improvement

- Practise extracting files from packet captures and independently verifying their SHA-256 hashes using safe methods.
- Improve my understanding of DNS traffic and TLS connection analysis.
- Gain more experience examining suspicious file transfers and researching relevant indicators.
- Continue improving my confidence in documenting findings and separating confirmed evidence from assumptions.

## Reflection: I was unable to independently verify the executable's SHA-256 hash during this investigation. This highlighted the need to strengthen my file-identification and threat intelligence research skills.

## References

-Malware-Traffic-Analysis.net

-Wireshark User's Guide

-VirusTotal



