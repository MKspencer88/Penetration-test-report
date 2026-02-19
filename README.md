# Penetration Test Report

This project documents my participation in a CTF even where I approached each challenge using a structured penetration test methodology. My ficitonal company **BBNC Security** was hired by simulated company **Rekall** to conduct a full penetration test on their web application host at 192.168.14.35. The goal was to identify, exploit, and document real-world vulnerabilities. 

This repository inculdes:
- A summary of all vulnerabilities discovered
- Impact analysis and remeditation recommendations
- Tools and methodologies used
- A link to the full penetration test report

# Objectives
- Practice structured penetration testing methodology
- Identify and exploit critical web application vulnerabilities
- Demonstrate offensive security skills including enumeration, exploitation and reporting
- Produce a professional penetration test summary

# Tools and Technologies
- Nmap
- Nessus
- Metasploit
- Burp Suite / Browser DevTools
- curl
- Linux command-line utilities
- Custom payloads

# Methodology
1. Reconnaissance - Identified exposed services, endpoints and application behavior
2. Enumeration - Mapped inputs, parameters and attack surfaces
3. Vulnerability Analysis - Tested for injection flaws, miconfigurations, and insecure components
4. Exploitation - Executed payloads to gain access, escalate privileges, and extract sensitive data
5. Documentation - Recorded findings, impact, and remediation steps in formal report

# Vulnerability Summary
Below is a high-level summary of all **12 critical vulnerabilities** identified during the engagement.

# 1. Reflected Cross-Site Scripting (XSS-Reflected)
- **Type:** Web Application
- **Risk:** Critical
- Unsanitized input in the "name" field allowed immediate JavaScript execution in the browser. Any user interacting with this field could trigger malicious scripts. 
- **Impact:** Session hijacking, credential theft, forced redirects
- **Remediation:** Input sanitization, output encoding, Content Security Policy (CSP), and secure frameworks

# 2. Stored Cross-Site Scripting (XSS-Stored)
- **Type:** Web application
- **Risk:** Critical
- Malicious scripts submitted through the comment box were stored server-side and executed for every visitor.
- **Impact:** Persistent compromise of all users
- **Remediation:** Sanitize stored input, encode output, and enfoce CSP

# 3. Sensitive Data Exposure
- **Type:** Web application
- **Risk:** Critical
- A curl -v request to http://192.168.14.35/About-Rekall.php revealed server information and internal metadata.
- **Impact:** Increased attack surface and targeted exploitation
- **Remediation:** Strong encryption, patching, secure storage, and key rotation

# 4. Local File Inclusion (LFI)
- **Type:** Web application
- **Risk:** Critical
- The file upload feature allowed manipulation of file paths, enabling access to local server files.
- **Impact:** Potiential RCE and sensitive file access
- **Remediation:** Validate file paths, restrict directories, and enforce allow lists

# 5. Directory Traversal
- **Type:** Web application
- **Risk:** Critical
- URL manipulation allowed attackers to navigate the server's file system and execute commands.
- **Impact:** Unauthorized file access and system exposure
- **Remediation:** Block traversal sequences, restrict permissions, and enforce boundaries

# 6. Command Injection
- **Type:** Web Application
- **Risk:** Critical
- A lookup feature accepted unsanitized input, allowing system command execution. I used this to retrieve vendor information.
- **Impact:** Full server compromise potiential
- **Remediation:** Safe functions, strick input validation, and permission restrictions

# 7. PHP Injection
- **Type:** Web Application
- **Risk:** Critical
- Malicious PHP code could be injected through text fields or URLs. I used this to enumerate all users on the server.
- **Impact:** Arbitrary code execution and data exposure
- **Remediation:** Treat all input as untrusted, validate input and use prepared statements

# 8. Open-Sourced Exposed Data
- **Type:** Web Application
- **Risk:** Critical
- Public OSINT tools revealed sensitive information about the application and domain.
- **Impact:** Attackers can gather intelligence without touching the server
- **Remediation:** Use robots.txt, authentication gates, anti-scraping controls and honeytokens

# 9. Nessus Scan --> Apache Struts Exploit
- **Type:** Web Application
- **Risk:** Critical
- A Nessus scan identified major vulnerabilities. Using Metasploit, I exploited Apache Struts and gained server access.
- **Impact:** Remote code execution and full system compromise.
- **Remediation:** Patch management, disable unsused services, and firewall hardening

# 10. Brute Force Attack
- **Type:** Web Application
- **Risk:** Critical
- After gaining terminal-like access, I retieved /etc/passwd and could attempt password cracking or access /etc/shadow.
- **Impact:** Account takeover and privilege escalation
- **Remediaion:** MFA, login attempt limits, strong password policies and WAF rules

# 11. SOL Injection
- **Type:** Web Application
- **Risk:** Critical
- Unsanitized SQL input allowed bypassing authentication and manipulating database queries.
- **Impact:** Credential bypass, data extraction, and account takeover
- **Remediation:** Prepared statements, stored procedures, and strict input validation

# 12. Nmap Network Enumeration
- **Type:** Linux
- **Risk:** Critical
- Agressive Nmap scanning revealed multiple hosts on the subnet(192.168.13.10-14) and exposed open ports and services.
- **Impact:** Attack surface mapping and targeted expoitation
- **Remediation:** Firewall restrictions, rate limiting, and port knocking

# Lessons Learned
- Importance of input validation and secure coding practices
- How small misconfigurations lead to full system compromise
- Value of OSINT in early reconnaissance
- How automated scanners (Nessus) complement manual testing
- Reinforced understanding of OWASP top 10 vulnerabilities
- Strengthened exploitation and reporting skills

# Full Report
[**View the compelete penetration test report**](artifacts/MK Spencer Rekall Penetration Test Report Project 2.pdf)

