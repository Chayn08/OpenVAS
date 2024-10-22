# OpenVAS Basic Scan Walkthrough

This document describes a basic vulnerability assessment conducted using OpenVAS. The goal is to showcase the process of setting up a scan, executing it, and interpreting the results. The target IP in this example is 192.168.XX.XX

## 1. Accessing the GSA Dashboard

![image](https://github.com/user-attachments/assets/e013968c-da25-4369-8609-402d0555ffe2)

Description: The Greenbone Security Assistant (GSA) dashboard is the main interface for managing scans. It provides an overview of ongoing tasks, CVE trends, and other relevant metrics.

Purpose: To monitor the system's vulnerability status and track the progress of your scans.

## 2. Creating a New Target

![image](https://github.com/user-attachments/assets/2b32ddeb-50c4-433f-8df8-d860178faad6)

Details: We define the scan target manually by entering the IP address 192.168.XX.X The port list is set to "All IANA assigned TCP", and the default "alive" test method is selected to verify if the target is reachable.

Objective: Establish the target system for the vulnerability scan.

## 3. Configuring the Scan Task

![image](https://github.com/user-attachments/assets/87167b3a-4eea-49c3-afac-b60492257db3)

Details: The scan task is configured with the name "Scan Basique - 192.168.XX.XX". We choose the previously defined target and select the "Full and fast" scan configuration. The task is set with a minimum Quality of Detection (QoD) at 70%.

Purpose: To set up a comprehensive scan task targeting the specified system and services.

## 4. Reviewing the Task Configuration

![image](https://github.com/user-attachments/assets/d6899f95-a23f-48c8-bd5e-b7cb2685ae3c)

Details: The task details include the scanner type, target information, and scan parameters, confirming that the task is ready for execution.

Importance: Ensures that the task configuration aligns with the intended scope and scan settings.

## 5. Monitoring the Scan Progress

![image](https://github.com/user-attachments/assets/a723dd9e-6fe7-48ee-b3f7-2107621feb56)

Details: The scan is actively running, with the status showing that vulnerabilities have been detected at a "Medium" severity level. The completion percentage indicates the progress of the scan.

Relevance: Provides real-time feedback on the scan’s status and detected vulnerabilities.*

## 6. Viewing the Scan Summary

![image](https://github.com/user-attachments/assets/762de3c8-a4fd-4d38-8191-b49bba76eaf6)

Details: The scan summary shows the number of vulnerabilities grouped by severity levels. In this case, it indicates the presence of "Medium" vulnerabilities.

Purpose: Summarizes the overall risk level based on detected vulnerabilities.

## 7.  Detailed Vulnerability Review

![Capture d'écran 2024-10-22 110719](https://github.com/user-attachments/assets/1f87e5c9-8c47-46e4-a9cf-ba313110f26b)

Details: Displays the specific vulnerabilities found, including descriptions, severities, and affected services.

Importance: Critical for understanding the nature of the risks and planning mitigations.


Vulnerabilities Detected and Recommendations

Below is a list of detected vulnerabilities along with explanations and recommended mitigations:

## DCE/RPC and MSRPC Services Enumeration Reporting (Medium)

![Capture d'écran 2024-10-22 112130](https://github.com/user-attachments/assets/fea917bb-e667-405f-91d6-73db562d8757)

Description: RPC services can be enumerated, revealing critical information such as service endpoints and processes (e.g., lsass.exe).

Recommendation: Restrict access to ports (135/tcp, 49664/tcp) using a firewall and disable unnecessary RPC services. Implement ACLs to control which IP addresses can access these services.

## ICMP Timestamp Reply Information Disclosure (Low)

![Capture d'écran 2024-10-22 112516](https://github.com/user-attachments/assets/19e1cf03-d20c-4a53-8ace-d59f79c246c3)

Details: The target responds to ICMP timestamp requests, potentially leaking system time information.

Recommendation: Disable ICMP timestamp responses at the system level (net.ipv4.icmp_timestamps = 0 on Linux) or configure the firewall to block these packets.

## OS Detection Consolidation and Reporting (Log)

![Capture d'écran 2024-10-22 112534](https://github.com/user-attachments/assets/3f16818c-a316-496c-8d26-0d476b2d457e)

Details: The scan consolidates OS information, identifying the system as running Microsoft Windows based on DCE/RPC information.

Recommendation: Ensure that unnecessary services are disabled and restrict access to sensitive ports to prevent OS fingerprinting.

## DCE/RPC and MSRPC Services Enumeration (Log)

![Capture d'écran 2024-10-22 112545](https://github.com/user-attachments/assets/6b7b9710-522d-47ae-9138-3c2991cfa62a)

Details: Enumeration of DCE/RPC services reveals endpoint information that could be leveraged for further attacks.

Recommendation: Limit network traffic to these services with strict firewall rules or by disabling the services if not required.

## SMB/CIFS Server Detection (Log)

![Capture d'écran 2024-10-22 112555](https://github.com/user-attachments/assets/6ed8b680-1e94-4423-9a18-77ffb2c4966b)

Details: Open SMB ports (139/tcp, 445/tcp) were detected, indicating that file sharing services are running.

Recommendation: Secure SMB services by using updated versions (SMBv3), restricting access to these ports via firewall rules, and disabling SMB if unnecessary.

## Traceroute Detection (Log)

![Capture d'écran 2024-10-22 112607](https://github.com/user-attachments/assets/62825944-1dc0-4eb2-b17b-69dede2486bd)

Details: The system allows traceroute, providing insights into the network route and topology.

Recommendation: Block traceroute probes by filtering ICMP Type 11 and TCP traffic used for traceroute using firewall rules.

## VMware ESX/GSX Server Detection (Log)

![Capture d'écran 2024-10-22 112618](https://github.com/user-attachments/assets/2c1c64c2-0c92-4e80-9c33-adbcbd40e0c5)

Details: A VMware authentication daemon was detected, indicating the presence of VMware services on the target.

Recommendation: Limit access to these services, ensure the VMware instance is updated, and harden the environment against unauthorized access.

## SMB Remote Version Detection (Log)

![Capture d'écran 2024-10-22 112632](https://github.com/user-attachments/assets/7dc6d093-f349-456e-8cbf-09bbd0692a43)

Details: The scan detected that SMBv2 and SMBv3 are enabled on the target.

Recommendation: Make sure only the latest and secure versions of SMB are enabled. Implement strong authentication and encryption for SMB traffic.

# Summary

This OpenVAS scan highlighted several low to medium-severity vulnerabilities, primarily related to service enumeration and information disclosure. Each finding was analyzed, and actionable recommendations were provided to mitigate potential risks.

This document can be used as a reference for setting up similar scans and understanding basic vulnerabilities encountered during pentesting activities. For further exploration, authenticated scans or more comprehensive configurations can be deployed.

















