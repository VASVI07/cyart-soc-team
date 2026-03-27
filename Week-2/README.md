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


## Basic Incident Response

### Incident: Failed Login Attempts (EventID 4625)

**1. Identification:**
Detected multiple failed login attempts in Splunk logs.

**2. Containment:**
Blocked suspicious IP address and monitored login activity.

**3. Eradication:**
Checked system for unauthorized access and removed any suspicious accounts.

**4. Recovery:**
Reset affected user passwords and restored normal login operations.

**5. Lessons Learned:**
Implemented account lockout policy and stronger password rules.
## Splunk Log Analysis Proof

![Splunk Screenshot](https://github.com/user-attachments/assets/f7dbfd3d-f16f-424e-9522-096a3a36bb24)


## Practical Steps Performed

1. Started Splunk in Ubuntu VM using:
   sudo /opt/splunk/bin/splunk start

2. Opened Splunk Web at:
   http://localhost:8000

3. Uploaded log file (log.csv) using "Add Data"

4. Selected sourcetype as CSV

5. Indexed data into "main" index

6. Searched logs using:
   index="main" "4625"

7. Identified failed login attempts (Event ID 4625)

8. Analyzed logs and created alert classification
