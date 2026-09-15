# Week-4-Web-Application-Penetration-Testing
# 🔐 Mediroza General Hospital — Web Application Penetration Testing

### Week 4 Cybersecurity Internship Project

**Researcher / Pentester:** Ufot Daraobong Esthiet  
**Batch:** B082  
**Training Program:** NetworkWalks  
**Week:** 4  
**Assessment Type:** Black-Box Web Application Penetration Test  
**Target:** Mediroza General Hospital  
**Environment:** Authorized Cybersecurity Training Lab

---

## 📌 Project Overview

This repository documents my Week 4 practical cybersecurity project completed during my training with NetworkWalks.

The project involved conducting a controlled **Web Application Penetration Test and Vulnerability Assessment** against the Mediroza General Hospital web application.

The assessment focused on identifying weaknesses within the application's publicly accessible areas, investigating the patient portal, analyzing authentication behavior, assessing the security of sensitive patient documents, and documenting the security impact of the findings.

Rather than focusing only on identifying individual vulnerabilities, this practical helped me understand how several weaknesses can be connected together to create a larger security risk.

---

# 🎯 Assessment Objectives

The main objectives of this project were to:

- Perform reconnaissance against the web application
- Identify potentially exposed directories and resources
- Investigate the patient portal
- Assess the login functionality
- Identify application security weaknesses
- Investigate SQL-related errors
- Demonstrate the impact of the identified vulnerability within the authorized lab
- Access the assigned patient reports
- Assess the protection applied to the PDF files
- Evaluate the strength of the document password
- Collect and organize evidence
- Analyze the security impact of the findings
- Provide appropriate remediation recommendations

---

# 🧪 Testing Approach

I followed a progressive penetration-testing approach.

Instead of immediately attempting exploitation, I started by gathering information about the application and then used the information discovered during reconnaissance to determine where further investigation was appropriate.

The assessment followed this general workflow:

```text
Reconnaissance
      ↓
Application Enumeration
      ↓
Patient Portal Investigation
      ↓
Vulnerability Identification
      ↓
Controlled Validation
      ↓
Sensitive Data Assessment
      ↓
PDF Security Assessment
      ↓
Risk Analysis
      ↓
Remediation Recommendations
      ↓
Documentation

Absolutely. Below is the **complete GitHub README project**, written as your own Week 4 project and with a different structure from the sample.

You can copy everything below into your GitHub repository as `README.md`.

````markdown
# 🔐 Mediroza General Hospital — Web Application Penetration Testing

### Week 4 Cybersecurity Internship Project

**Researcher / Pentester:** Ufot Daraobong Esthiet  
**Batch:** B082  
**Training Program:** NetworkWalks  
**Week:** 4  
**Assessment Type:** Black-Box Web Application Penetration Test  
**Target:** Mediroza General Hospital  
**Environment:** Authorized Cybersecurity Training Lab

---

## 📌 Project Overview

This repository documents my Week 4 practical cybersecurity project completed during my training with NetworkWalks.

The project involved conducting a controlled **Web Application Penetration Test and Vulnerability Assessment** against the Mediroza General Hospital web application.

The assessment focused on identifying weaknesses within the application's publicly accessible areas, investigating the patient portal, analyzing authentication behavior, assessing the security of sensitive patient documents, and documenting the security impact of the findings.

Rather than focusing only on identifying individual vulnerabilities, this practical helped me understand how several weaknesses can be connected together to create a larger security risk.

---

# 🎯 Assessment Objectives

The main objectives of this project were to:

- Perform reconnaissance against the web application
- Identify potentially exposed directories and resources
- Investigate the patient portal
- Assess the login functionality
- Identify application security weaknesses
- Investigate SQL-related errors
- Demonstrate the impact of the identified vulnerability within the authorized lab
- Access the assigned patient reports
- Assess the protection applied to the PDF files
- Evaluate the strength of the document password
- Collect and organize evidence
- Analyze the security impact of the findings
- Provide appropriate remediation recommendations

---

# 🧪 Testing Approach

I followed a progressive penetration-testing approach.

Instead of immediately attempting exploitation, I started by gathering information about the application and then used the information discovered during reconnaissance to determine where further investigation was appropriate.

The assessment followed this general workflow:

```text
Reconnaissance
      ↓
Application Enumeration
      ↓
Patient Portal Investigation
      ↓
Vulnerability Identification
      ↓
Controlled Validation
      ↓
Sensitive Data Assessment
      ↓
PDF Security Assessment
      ↓
Risk Analysis
      ↓
Remediation Recommendations
      ↓
Documentation
````

---

# 🔎 Phase 1 — Reconnaissance

The first stage of the assessment involved identifying information that was publicly accessible from the target application.

One of the first resources investigated was:

```text
robots.txt
```

The response revealed the following application paths:

```text
/patient/
/staff/
/old/
```

These paths provided useful information about areas of the application that could require further investigation.

### Observation

The presence of directories such as `/patient/` and `/staff/` can provide an attacker with information about the structure and functionality of an application.

### Security Consideration

Sensitive application areas should not rely on directory secrecy as a security control.

Access to restricted functionality should always be protected through proper authentication and authorization mechanisms.

---

# 🌐 Phase 2 — Application Enumeration

After the initial reconnaissance, I investigated the available functionality of the web application.

The patient portal became the primary area of interest because it appeared to contain functionality related to sensitive patient information.

I examined how the login functionality responded to different inputs and observed the application's responses.

During this stage, the application returned an SQL-related error instead of providing only a generic authentication failure.

---

# 💉 Phase 3 — SQL Injection Identification

## Finding: SQL Injection in Patient Portal

**Severity:** 🔴 Critical

**Category:** Injection

**Affected Component:** Patient Portal Login

### Description

During the assessment of the patient portal, the application returned a **MySQL syntax error** while processing login input.

The error indicated that user-supplied information was reaching the backend database query in an unsafe manner.

Displaying database errors directly to users also revealed information about the technology being used by the application.

This behavior provided an indication that the application's database interaction required further security investigation.

### Evidence

The evidence collected during the practical shows the patient portal returning a MySQL-related syntax error.

**Evidence file:**

```text
evidence/03-sql-error.png
```

### Potential Impact

If an SQL injection vulnerability exists in a production healthcare application, an attacker could potentially manipulate database queries and gain unauthorized access to sensitive information.

Potentially affected information could include:

* Patient records
* Patient identifiers
* Laboratory results
* Authentication information
* Other confidential database information

### Risk Rating

**Critical**

The severity is based on the affected application area and the potential confidentiality impact associated with healthcare information.

### Recommended Remediation

The application should:

* Use prepared statements and parameterized queries
* Never build SQL queries directly from untrusted input
* Implement server-side input validation
* Apply least-privilege permissions to database accounts
* Prevent raw database errors from being displayed to users
* Log detailed errors securely on the server
* Conduct additional security testing against application inputs

---

# 🚪 Phase 4 — Access to the Patient Area

Following identification and validation of the application weakness within the controlled training environment, I was able to access the restricted patient area.

This allowed me to continue the assessment and investigate the patient documents provided as part of the exercise.

The ability to reach sensitive information after compromising an authentication mechanism demonstrated the potential impact of the vulnerability.

---

# 📄 Phase 5 — Sensitive Patient Report Exposure

## Finding: Unauthorized Access to Patient Reports

**Severity:** 🔴 Critical

**Category:** Broken Access Control / Sensitive Information Disclosure

### Description

After accessing the restricted patient area, I located the patient reports assigned as part of the practical exercise.

The assessment identified three PDF files:

```text
patient_report_1.pdf
patient_report_2.pdf
patient_report_3.pdf
```

The first report was successfully opened during the exercise and contained laboratory information.

The information visible in the report included items such as:

* Patient name
* Patient ID
* Date of birth
* Laboratory information

### Evidence

Evidence was captured showing the patient report accessed during the assessment.

```text
evidence/04-patient-report.png
```

### Security Impact

Healthcare information is highly sensitive.

Unauthorized access to patient reports could potentially result in:

* Patient privacy violations
* Exposure of medical information
* Identity-related risks
* Regulatory consequences
* Reputational damage
* Loss of patient trust

### Risk Rating

**Critical**

The finding is considered critical because unauthorized access to sensitive healthcare information was demonstrated within the training environment.

### Recommended Remediation

The application should:

1. Enforce authorization checks on every request for patient information.
2. Ensure users can only access records they are authorized to view.
3. Use unpredictable identifiers for sensitive resources.
4. Prevent direct access to patient files through predictable paths.
5. Require authentication before accessing sensitive documents.
6. Validate authorization on the server for every document request.
7. Log access to sensitive patient records.
8. Regularly perform access-control testing.

---

# 🔑 Phase 6 — PDF Password Security Assessment

After retrieving the assigned patient reports, I examined the protection applied to the PDF files.

The first PDF was password protected.

To assess the strength of the protection, I used the **NetworkWalks Hash Calculator** provided as part of the training resources.

The protected PDF was processed to obtain a crackable representation of its password protection.

The resulting hash was then tested using the available password-recovery functionality.

---

## 🧮 Hash Extraction

The NetworkWalks Hash Calculator was used to process the protected PDF.

The purpose of this step was to convert the PDF's password protection into a format that could be assessed using password-recovery tools.

### Evidence

```text
evidence/05-pdf-hash.png
```

---

# 🔓 Phase 7 — Password Recovery

The extracted PDF hash was tested using the password-cracking functionality available during the practical.

The password was successfully recovered.

### Result

```text
Password: 123456
```

The recovered password was then used to open the protected PDF successfully.

### Evidence

```text
evidence/06-password-recovered.png
```

---

# ⚠️ Finding: Weak PDF Password Protection

**Severity:** 🟠 High

**Category:** Weak Password / Insufficient Protection of Sensitive Data

### Description

Although the patient report was protected using PDF encryption, the password protecting the document was extremely simple and predictable.

The successful recovery demonstrated that encryption alone does not guarantee strong protection when a weak password is used.

### Security Impact

If an attacker obtains a copy of an encrypted sensitive document, a weak password can significantly reduce the effectiveness of the encryption.

In a healthcare environment, this could potentially result in unauthorized disclosure of confidential medical information.

### Risk Rating

**High**

The finding is rated High because the protected document contained sensitive information and the password was successfully recovered during the authorized assessment.

### Recommended Remediation

Organizations should:

* Use strong randomly generated passwords
* Avoid predictable passwords
* Avoid sequential numeric passwords
* Never reuse passwords across sensitive documents
* Use appropriate encryption mechanisms
* Protect sensitive files through centralized access control
* Review how sensitive documents are stored and distributed
* Implement strong password-management policies

---

# 🧩 Attack Chain

One of the most important lessons from this project was seeing how separate weaknesses could be connected.

The assessment can be represented as:

```text
1. Reconnaissance
        ↓
2. robots.txt Discovery
        ↓
3. /patient/ Directory Identified
        ↓
4. Patient Portal Investigation
        ↓
5. MySQL Error Observed
        ↓
6. SQL Injection Vulnerability Identified
        ↓
7. Restricted Patient Area Accessed
        ↓
8. Patient Reports Located
        ↓
9. Sensitive Information Exposed
        ↓
10. PDF Encryption Assessed
        ↓
11. PDF Hash Extracted
        ↓
12. Weak Password Recovered
        ↓
13. Protected PDF Successfully Opened
```

This demonstrates how multiple security weaknesses can increase the overall impact of an application compromise.

---

# 📊 Vulnerability Summary

| ID      | Finding                            | Severity    | Security Impact                                       |
| ------- | ---------------------------------- | ----------- | ----------------------------------------------------- |
| VULN-01 | SQL Injection in Patient Portal    | 🔴 Critical | Authentication bypass / potential database compromise |
| VULN-02 | Unauthorized Patient Report Access | 🔴 Critical | Exposure of sensitive healthcare information          |
| VULN-03 | Weak PDF Password Protection       | 🟠 High     | Recovery of protected sensitive documents             |

---

# 🛠️ Tools & Resources Used

| Tool / Resource                   | Purpose                                          |
| --------------------------------- | ------------------------------------------------ |
| **Kali Linux**                    | Penetration-testing environment                  |
| **Web Browser**                   | Reconnaissance and web application interaction   |
| **cURL**                          | Retrieving and inspecting web resources          |
| **NetworkWalks Hash Calculator**  | Processing the protected PDF                     |
| **NetworkWalks Password Cracker** | Password security assessment                     |
| **PDF Viewer**                    | Verifying the recovered document                 |
| **GitHub**                        | Project documentation and portfolio presentation |

---

# 🖼️ Evidence Collection

All screenshots collected during the practical are organized inside the `evidence/` directory.

```text
evidence/
│
├── 01-robots-txt.png
├── 02-patient-portal.png
├── 03-sql-error.png
├── 04-patient-report.png
├── 05-pdf-hash.png
├── 06-password-recovered.png
└── 07-retrieved-reports.png
```

### Evidence Description

**01 — robots.txt**

Shows the application directories discovered during reconnaissance.

**02 — Patient Portal**

Shows the patient portal identified during application enumeration.

**03 — SQL Error**

Shows the MySQL-related error returned by the application.

**04 — Patient Report**

Shows the patient laboratory report accessed during the exercise.

**05 — PDF Hash Extraction**

Shows the NetworkWalks Hash Calculator processing the protected PDF.

**06 — Password Recovery**

Shows the successful password-recovery result.

**07 — Retrieved Reports**

Shows the assigned patient report files identified during the exercise.

---

# 🛡️ Remediation Plan

Based on the findings from the assessment, the following remediation priorities are recommended.

## Priority 1 — Fix SQL Injection

The patient portal should be reviewed and all database queries should use parameterized statements.

User input should always be treated as untrusted.

---

## Priority 2 — Strengthen Access Control

Authentication should not be the only security control.

The application must verify whether the authenticated user has permission to access each individual patient record.

---

## Priority 3 — Protect Sensitive Documents

Patient reports should not be stored in publicly accessible locations.

Sensitive documents should be delivered through an authenticated application process that verifies authorization before returning the file.

---

## Priority 4 — Improve Password Security

Predictable passwords such as sequential numbers should not be used to protect sensitive documents.

Strong, randomly generated credentials should be used where document-level passwords are required.

---

## Priority 5 — Disable Detailed Database Errors

Raw database errors should never be displayed to users.

Users should receive a generic error message while detailed technical information is securely logged on the server.

---

## Priority 6 — Improve Security Monitoring

The application should monitor:

* Failed login attempts
* Unusual authentication activity
* Repeated requests for sensitive documents
* Database errors
* Requests to restricted directories
* Suspicious access patterns

---

## Priority 7 — Perform Security Retesting

After remediation, a follow-up penetration test should be conducted to verify that the vulnerabilities have been properly resolved.

---

# 📚 Key Lessons Learned

This project gave me practical experience in several areas of cybersecurity.

### 🔎 Reconnaissance

I learned how seemingly small pieces of publicly accessible information can reveal useful details about an application's structure.

### 💉 SQL Injection

I gained a better understanding of how unsafe handling of user input can affect database-driven applications.

### 🔐 Authentication & Authorization

The practical showed me why applications need both secure authentication and strong authorization controls.

### 📄 Sensitive Data Protection

I learned that sensitive files require multiple layers of protection.

### 🔑 Password Security

The PDF exercise demonstrated how the use of a weak password can reduce the effectiveness of encryption.

### 📝 Security Documentation

I also learned the importance of documenting:

* What was tested
* What was discovered
* How the finding was validated
* What the impact could be
* How the issue should be fixed
* What evidence supports the finding

---

# 💭 Personal Reflection

This project was one of the practical exercises that helped me better understand how cybersecurity concepts connect together.

Before this exercise, concepts such as reconnaissance, SQL injection, password security and access control could seem like separate topics.

Working through the assessment helped me see how they can form part of one security assessment.

The biggest lesson I took from the project is that cybersecurity is not only about finding vulnerabilities.

A good security professional should also be able to:

**Identify → Understand → Validate → Analyze → Document → Recommend**

This practical has motivated me to continue improving my skills in web application security, ethical hacking and vulnerability assessment.

---

# 🏁 Conclusion

My Week 4 cybersecurity internship project with NetworkWalks provided a practical introduction to web application penetration testing.

During the assessment, I performed reconnaissance, investigated the patient portal, identified an SQL-related security weakness, demonstrated its impact within the authorized training environment, accessed the assigned patient reports, and assessed the password protection applied to one of the documents.

The assessment demonstrated that security weaknesses can become more serious when they are chained together.

The combination of insecure database input handling, insufficient access protection and weak document passwords created a significant confidentiality risk within the training scenario.

This project strengthened my understanding of web application security and improved my ability to analyze technical findings and communicate them through professional cybersecurity documentation.

I look forward to applying these lessons to future labs and continuing to develop my skills in cybersecurity.

---

# 👨‍💻 Project Author

**Ufot Daraobong Esthiet**

Cybersecurity Trainee | Ethical Hacking | Footprinting | Scanning | Web Application Security

**Training:** NetworkWalks
**Batch:** B082
**Project:** Week 4 — Web Application Penetration Testing

---

## ⚠️ Portfolio Note

This project was completed as part of an authorized cybersecurity training environment.

The techniques and findings documented here were performed within the defined scope of the practical exercise.

Sensitive information from the training environment should be redacted before publishing screenshots or reports publicly.

---

# 🔐 Skills Demonstrated

`Web Application Security`
`Penetration Testing`
`Reconnaissance`
`SQL Injection Analysis`
`Access Control Assessment`
`Password Security`
`PDF Security Assessment`
`Vulnerability Assessment`
`Risk Analysis`
`Security Documentation`
`Kali Linux`
`GitHub`

````

### 📁 Your GitHub repository should look like this

```text
mediroza-web-application-pentest/
│
├── README.md
│
├── evidence/
│   ├── 01-robots-txt.png
│   ├── 02-patient-portal.png
│   ├── 03-sql-error.png
│   ├── 04-patient-report.png
│   ├── 05-pdf-hash.png
│   ├── 06-password-recovered.png
│   └── 07-retrieved-reports.png
│
└── report/
    └── Mediroza-Penetration-Testing-Report.pdf
````

**One important change before you make the repository public:** redact the patient name, patient ID, date of birth, medical/laboratory details, and other personal information from your screenshots. I also recommend **not publishing the recovered password (`123456`) in the public repository**; you can state that a weak password was successfully recovered without exposing the credential itself.
