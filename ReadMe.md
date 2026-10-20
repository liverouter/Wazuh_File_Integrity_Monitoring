# Wazuh SOC Lab: File Integrity Monitoring (FIM)

## Overview

This project documents my practical experience using Wazuh for Security Operations Center (SOC) monitoring and Windows endpoint security.

The lab focused on configuring real-time File Integrity Monitoring (FIM) on a Windows 11 endpoint, generating file activity, and investigating the alerts produced in the Wazuh Dashboard.

The Wazuh server was provided as a pre-deployed environment by the academy. My work involved verifying the services, checking the Windows agent, configuring file monitoring, and analysing the resulting security events.

## Objectives

- Verify Wazuh Manager, Indexer, and Dashboard services.
- Confirm Windows endpoint agent connectivity.
- Configure real-time monitoring of a sensitive directory.
- Test file creation, modification, and deletion.
- Investigate alerts, file metadata, and checksum changes.
- Understand how FIM supports security monitoring and incident investigation.

## Lab Environment

| Component             | Details                   |
| --------------------- | ------------------------- |
| SIEM platform         | Wazuh                     |
| Server                | Ubuntu (`icdfa-server`)   |
| Endpoint              | Windows 11                |
| Wazuh Agent           | Version 4.12.0            |
| Virtualisation        | VirtualBox                |
| Network               | Host-only                 |
| Monitoring capability | File Integrity Monitoring |

## Lab Configuration

The monitored directory was:

`C:\Users\Juliet\Documents\SensitiveFiles`

The test file was:

`secret_plan.txt`

Real-time monitoring was enabled for the directory through the Wazuh agent configuration.

## Tests and Results

Three file operations were tested to verify that Wazuh could detect changes to the monitored file.

| Activity          | Alert Description          | Rule ID | Alert Level |
| ----------------- | -------------------------- | ------- | ----------- |
| File creation     | File added to the system   | 554     | 5           |
| File modification | Integrity checksum changed | 550     | 7           |
| File deletion     | File deleted               | 553     | 7           |

### File Modification Analysis

During the modification test, additional text was added to the existing file.

Wazuh detected the change and recorded:

- File size change from 93 bytes to 163 bytes.
- Changes to the MD5, SHA1, and SHA256 checksums.
- A real-time integrity alert with Rule ID 550 and alert level 7.

The deletion test also generated a real-time event with Rule ID 553.

These results confirmed that FIM was working for the monitored directory.

## Security Analysis

The lab also covered:

- Alert triage and interpretation.
- Directories that may generate excessive FIM alerts.
- How file monitoring can help identify potential ransomware activity.
- The benefits of centralised monitoring with Wazuh compared with relying exclusively on native Windows Event Logs.

No ransomware was executed during this exercise. The tests involved normal file creation, modification, and deletion.

## Evidence

Screenshots and supporting evidence can be organised in the repository to demonstrate:

- Wazuh service verification.
- Windows agent status.
- FIM configuration.
- File creation alert.
- File modification alert and checksum changes.
- File deletion alert.
- Analysis of the generated events.

## Key Takeaways

This exercise improved my practical understanding of Wazuh, endpoint monitoring, file integrity checks, security alert investigation, and the use of SIEM tools in a SOC environment.

It also demonstrated the importance of reviewing alerts in context, as file changes do not automatically indicate malicious activity.
