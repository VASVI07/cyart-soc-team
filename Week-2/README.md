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

## Alert Triage Practice

| Alert ID | Description              | Source IP      | Priority | Status |
|----------|--------------------------|----------------|----------|--------|
| 002      | Brute-force SSH          | 192.168.1.100  | Medium   | Open   |
| 005      | Failed Login (Event 4625)| 192.168.1.50   | High     | Investigating |

### Analysis:
- Event ID 4625 indicates failed login attempts
- Multiple attempts suggest possible brute-force attack
- Requires monitoring and possible IP blocking

## CVSS-Based Alert Prioritization

| Alert ID | Alert Name                    | CVSS Score | Priority | Reason |
|----------|-------------------------------|------------|----------|--------|
| 001      | Log4Shell Exploit Detected    | 9.8        | Critical | Public exploit and severe impact |
| 002      | Unauthorized Admin Login      | 8.1        | High     | High risk of privilege misuse |
| 003      | Brute Force SSH Attempts      | 5.9        | Medium   | Repeated access attempts detected |
| 004      | Port Scan                     | 2.6        | Low      | Reconnaissance with limited impact |

## Incident Ticket

**Title:** [High] Failed Login Attempts Detected (Event ID 4625)

**Description:**
Multiple failed login attempts detected in Splunk logs indicating possible brute-force attack.

**Indicators of Compromise (IOCs):**
- Event ID: 4625
- Source IP: 192.168.1.50
- Log Source: Windows Security Logs

**Priority:** High  
**Status:** Open  
**Assigned To:** SOC Analyst  

**Actions Taken:**
- Monitored login attempts
- Identified suspicious IP activity
- Prepared for containment (IP blocking)

## Escalation Email

Subject: [Critical] Failed Login Attempts Detected – Immediate Attention Required

Dear Tier 2 Team,

Multiple failed login attempts (Event ID 4625) have been detected in Splunk logs from source IP 192.168.1.50. The pattern indicates a possible brute-force attack targeting user accounts. The activity has been ongoing and may lead to unauthorized access if not mitigated.

Initial analysis has been completed, and the IP has been identified as suspicious. Further investigation and containment actions such as IP blocking and account lockout are recommended.

Please prioritize this incident and proceed with deeper analysis.

Regards,  
SOC Analyst

## Incident Response Report

### Executive Summary
A potential brute-force attack was detected based on multiple failed login attempts (Event ID 4625) in Splunk logs. The activity indicates repeated unauthorized access attempts.

### Timeline
- 10:00 AM – Multiple failed login attempts detected  
- 10:05 AM – Alert generated in Splunk  
- 10:10 AM – Investigation started  

### Impact Analysis
The attack could lead to unauthorized access if successful. It poses a risk to system security and user accounts.

### Remediation Steps
- Monitor login attempts  
- Enable account lockout policy  
- Block suspicious IP addresses  

### Lessons Learned
- Need stronger password policies  
- Continuous monitoring is required  
- Alerts should be configured for early detection

## Investigation Action Log

| Timestamp            | Action Performed              |
|----------------------|-------------------------------|
| 10:00 AM            | Detected failed login attempts |
| 10:05 AM            | Opened Splunk logs             |
| 10:10 AM            | Identified Event ID 4625       |
| 10:15 AM            | Analyzed attack pattern        |
| 10:20 AM            | Documented findings            |

## Phishing Investigation Checklist

- [ ] Verify email headers  
- [ ] Check sender reputation  
- [ ] Analyze suspicious links (VirusTotal)  
- [ ] Identify affected users  
- [ ] Report phishing email  
