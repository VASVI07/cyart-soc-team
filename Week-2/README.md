# Week 2 - SOC Fundamentals

## Name:
Vatsala gupta

## Objective:
This week focuses on learning:
- Alert Priority Levels
- Incident Classification
- Basic Incident Response

## Tools Used:
- Splunk
- Ubuntu VM
- GitHub

## Status:
In Progress
## Alert Priority Levels

| Alert ID | Alert Type              | Priority  | Reason |
|----------|------------------------|----------|--------|
| 001      | Ransomware Detected    | Critical | System encrypted |
| 002      | Unauthorized Login     | High     | Admin access attempt |
| 003      | Brute Force SSH        | Medium   | Multiple login attempts |
| 004      | Port Scan              | Low      | Reconnaissance activity |
| 005 | Failed Login (EventID 4625) | High | Possible brute force or unauthorized access |


## Incident Classification
## MITRE ATT&CK Mapping

| Alert ID | Incident Type     | MITRE Technique | Description |
|----------|------------------|----------------|------------|
| 001      | Malware          | T1486          | Data Encrypted for Impact (Ransomware) |
| 002      | Unauthorized Access | T1078       | Valid Accounts |
| 003      | Brute Force      | T1110          | Brute Force Login Attempts |
| 004      | Reconnaissance   | T1046          | Network Service Scanning |
| 005      | Brute Force      | T1110          | Failed Login Attempts |

| Alert ID | Incident Type     | Description                     |
|----------|------------------|---------------------------------|
| 001      | Malware          | Ransomware attack detected      |
| 002      | Unauthorized Access | Suspicious admin login        |
| 003      | Brute Force      | Multiple login attempts         |
| 004      | Reconnaissance   | Port scanning activity          |
| 005      | Brute Force      | Failed login attempts (EventID 4625) |
