---
title: "Lab 1 - Phishing"
excerpt: "This lab focuses on identifying and investigating phishing attempts targeting an organization. The analyst reviews email headers, examines suspicious URLs and attachments, checks sender authenticity, and determines whether the email is part of a wider phishing campaign. The objective is to validate the threat, contain potential impact, and escalate as necessary.<br/><img src='/images/500x300.png'>"
collection: portfolio
---

# Lab 1: Phishing Mail Detection

## Goal
The aim of this lab is to analyze a suspicious email and determine whether it is a phishing attempt.

## Tools Used
- VirusTotal  
- SIEM (LetsDefend Platform)  

## Environment
The analysis was conducted using a Windows Virtual Machine provided by LetsDefend, simulating a user workstation equipped with Outlook, a web browser, and endpoint protection tools. This controlled environment allows safe inspection of potentially malicious emails and attachments.

---

## Investigation Steps

### 1. Alert Review  
Reviewed the alert to gather initial information:
- **Date/Time:** 13 June 2021, 02:11 PM  
- **SMTP Address:** 24.213.228.54  
- **Sender:** trenton@tritowncomputers.com  
- **Recipient:** lars@letsdefend.io  
- **Action:** Allowed (email was delivered)

![Alert Details](images/alert_details.png)

---

### 2. Case Creation  
Created and assigned a case for investigation. Initiated the playbook for structured analysis.  
![Case Creation](Assets/Lab%201/Picture%201.png))

---

### 3. Email Content Review  
Used **Email Security** to locate the email and reviewed its content. The email contained poor grammar—often an indicator of phishing.

![Email Content](images/email_content.png)

---

### 4. Attachment Analysis  
Downloaded the attachment which included:
- One Excel file
- Two `.dll` files

Uploaded all files to **VirusTotal**:
- Excel file flagged by 39/61 vendors
- Both `.dll` files also marked as malicious

![VirusTotal Excel](images/virustotal_excel.png)  
![VirusTotal DLL](images/virustotal_dll.png)

---

### 5. Email Delivery Verification  
Confirmed the email was delivered via the **Monitoring module** (status: **Allowed**).  
![Monitoring Log](images/email_delivery.png)

---

### 6. Email Deletion  
Deleted the malicious email from the recipient’s inbox using the Email Security module.  
![Email Deletion](images/delete_email.png)

---

### 7. Endpoint & Log Review  
Located the user's device and IP via **Endpoint Security**.  
Searched logs to confirm the Excel file triggered outbound HTTP requests to malicious URLs.

![Endpoint Security](images/endpoint_security.png)  
![Log Management](images/log_management.png)

---

### 8. Containment  
Contained the affected device using the **Contain** function in Endpoint Security.  
![Device Containment](images/contain_device.png)

---

## Analysis

A malicious email was delivered to an internal user containing an Excel attachment with embedded VBA macros. These macros initiated HTTP requests to known malicious URLs. Log analysis confirmed the user opened the file, leading to execution of the macros and contact with the attacker's infrastructure. The affected device was isolated, and further forensic analysis is underway.

---

## Key Learnings

- Gained hands-on experience analyzing phishing emails and identifying malicious attachments.
- Learned how macro-enabled Excel files can execute automated HTTP requests to attacker-controlled servers.
- Strengthened skills in log analysis and endpoint monitoring to confirm user activity and detect post-compromise behavior.
- Understood the importance of swift containment actions to prevent lateral movement and data loss.
- Gained insight into structured incident response workflows including containment, eradication, and investigation.
- Recognized the critical role of user awareness and proactive email security in preventing phishing attacks.

