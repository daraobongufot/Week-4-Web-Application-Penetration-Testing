# Week-4-Web-Application-Penetration-Testing

# PENETRATION TESTING REPORT

## Mediroza General Hospital


## Week 4 Cybersecurity Internship Project

## 👤 Researcher / Pentester: Ufot Daraobong Esthiet
## 🎓 Batch: B082
🏢 Training Program: NetworkWalks
📅 Week: 4
🔎 Assessment Type: Black-Box Web Application Penetration Test
🎯 Target: Mediroza General Hospital
🌐 Scope: Authorized Training Environment

---

# 1. Executive Summary

I was assigned to conduct a black-box penetration test against the Mediroza General Hospital web application as part of my Week 4 cybersecurity practical with NetworkWalks.

The objective of the assessment was to identify weaknesses within the web application, demonstrate the security impact of the identified vulnerabilities within the authorized training environment, access the confidential patient reports provided for the exercise, and assess the protection applied to the retrieved documents.

I began the assessment from a black-box perspective, meaning that I approached the application without relying on internal information about its infrastructure.

During the initial reconnaissance phase, I inspected the website's `robots.txt` file. This revealed several application directories, including:

```text
/patient/
/staff/
/old/
```

The discovery of these directories provided useful information about the structure of the application and helped guide further investigation.

I then investigated the patient portal. During testing of the login functionality, the application returned a **MySQL syntax error** when unexpected input was supplied. This indicated that user input was reaching the backend database query without being handled securely and provided evidence of a potential SQL injection vulnerability.

Within the controlled training environment, I was able to use the identified weakness to gain access to the restricted patient area.

Three patient laboratory reports were then identified:

```text
patient_report_1.pdf
patient_report_2.pdf
patient_report_3.pdf
```

The reports contained sensitive patient information.

I also assessed the password protection applied to the PDF documents. Using the NetworkWalks Hash Calculator, I processed the protected PDF and obtained a hash suitable for password analysis. The password was subsequently recovered successfully, demonstrating that the document's password protection was weak.

The assessment therefore demonstrated that weaknesses in web application security and document protection can be combined to create a larger confidentiality risk.

### Overall Assessment

**Overall Risk: CRITICAL**

The most significant concern is the potential exposure of sensitive healthcare information. In a real hospital environment, unauthorized access to patient records could have serious privacy, legal, operational, and reputational consequences.

---

# 2. Scope and Methodology

## 2.1 Scope

The assessment focused on the Mediroza General Hospital web application:

**Target:**

```text
https://medirozahospital.com
```

The testing was performed as part of an authorized NetworkWalks cybersecurity training exercise.

The assessment focused on:

* Web application reconnaissance
* Patient portal investigation
* Authentication testing
* SQL injection assessment
* Patient report access
* PDF security assessment
* Password recovery testing

The assessment was conducted within the defined educational environment.

---

## 2.2 Methodology

I followed a structured approach during the assessment.

### Phase 1 — Reconnaissance

I began by gathering publicly accessible information about the application.

The `robots.txt` file was inspected and revealed:

```text
/patient/
/staff/
/old/
```

These directories were recorded as potential areas for further investigation.

---

### Phase 2 — Application Enumeration

I investigated the application functionality exposed through the discovered paths.

The patient portal was identified as an important area because it provided access to functionality involving patient information.

---

### Phase 3 — Vulnerability Identification

I tested the patient portal login functionality and observed how the application responded to different types of input.

A MySQL syntax error was returned during testing.

This indicated that the application was exposing backend database errors and that the login input required further security assessment.

---

### Phase 4 — Controlled Exploitation

The identified SQL injection weakness was validated within the authorized training environment.

The weakness allowed access to the restricted patient area.

---

### Phase 5 — Sensitive Data Assessment

After gaining access to the patient area, I identified the three patient PDF reports provided as part of the exercise.

I then assessed the protection applied to the reports.

---

### Phase 6 — PDF Password Assessment

The first protected PDF was processed using the NetworkWalks Hash Calculator.

The extracted hash was then used during password-recovery testing.

The password was successfully recovered and subsequently used to open the protected document.

---

# 3. Tools Used

The following tools and resources were used during the assessment:

| Tool / Resource                   | Purpose                                                      |
| --------------------------------- | ------------------------------------------------------------ |
| **Kali Linux**                    | Penetration-testing environment                              |
| **Web Browser**                   | Application interaction and investigation                    |
| **cURL**                          | Retrieving web resources such as `robots.txt`                |
| **NetworkWalks Hash Calculator**  | Processing the protected PDF and extracting a crackable hash |
| **NetworkWalks Password Cracker** | Testing the extracted PDF hash                               |
| **PDF Viewer**                    | Verifying the recovered password                             |
| **GitHub**                        | Documentation and portfolio presentation                     |

---

# 4. Findings and Proof of Exploitation

## 4.1 Summary Table

| # | Vulnerability / Finding                | Location          | Risk        |
| - | -------------------------------------- | ----------------- | ----------- |
| 1 | SQL Injection in Patient Portal        | Patient Login     | 🔴 Critical |
| 2 | Unauthorized Access to Patient Reports | Patient Reports   | 🔴 Critical |
| 3 | Weak PDF Password Protection           | Patient PDF Files | 🟠 High     |

---

# 4.2 Finding 1 — SQL Injection in Patient Portal

### Risk Rating: Critical

**Location:** Patient Portal Login

### Description

SQL injection occurs when an application incorporates user-controlled input into database queries without properly separating the input from the SQL statement.

During testing of the Mediroza patient portal, the login functionality returned a MySQL syntax error when unexpected input was supplied.

The error revealed that the application was interacting directly with a MySQL database and was not handling the supplied input securely.

This provided evidence that the login functionality was potentially vulnerable to SQL injection.

### Steps Taken

I first accessed the patient login page.

I then tested the application's handling of user input.

The application returned a database-related error instead of a generic authentication response.

### Evidence

**Figure 1 — Patient Portal Login**

```text
evidence/01-patient-login.png
```

**Figure 2 — MySQL Error**

```text
evidence/02-sql-error.png
```

### Impact

A successful SQL injection vulnerability in a healthcare application could potentially allow an attacker to:

* Bypass authentication
* Access restricted functionality
* Retrieve database information
* Access patient records
* Access laboratory information
* Potentially compromise additional application data

During this assessment, the vulnerability provided a path to the restricted patient area.

### Recommendation

The application should:

* Use prepared statements
* Use parameterized SQL queries
* Implement server-side input validation
* Apply least-privilege database permissions
* Never display raw database errors to users
* Log detailed errors securely on the server
* Perform additional SQL injection testing across application inputs

---

# 4.3 Finding 2 — Unauthorized Access to Confidential Patient Reports

### Risk Rating: Critical

**Location:** Patient Reports Area

### Description

After validating the authentication weakness within the controlled training environment, I was able to access the restricted patient area.

The portal contained three patient laboratory reports:

```text
patient_report_1.pdf
patient_report_2.pdf
patient_report_3.pdf
```

These documents contained sensitive healthcare information.

### Steps Taken

After gaining access to the patient area, I identified the available PDF reports and retrieved the files required by the exercise.

### Evidence

**Figure 3 — Patient Portal Reports**

```text
evidence/03-patient-reports.png
```

### Sensitive Information Observed

The patient report contained information including:

* Patient name
* Patient ID
* Date of birth
* Laboratory information

### Impact

Unauthorized access to medical information could result in:

* Patient privacy violations
* Disclosure of medical information
* Identity-related risks
* Regulatory consequences
* Reputational damage
* Loss of patient trust

### Recommendation

Mediroza should:

1. Implement server-side authorization checks.
2. Ensure users can only access records they are authorized to view.
3. Prevent direct access to sensitive files.
4. Use secure document identifiers.
5. Require authentication before returning patient documents.
6. Validate authorization for every document request.
7. Monitor access to sensitive records.
8. Perform regular access-control testing.

---

# 4.4 Finding 3 — Weak PDF Password Protection

### Risk Rating: High

**Location:** Patient PDF Reports

### Description

The patient reports were protected with PDF passwords.

Although password protection had been applied, the password used for the first document was weak enough to be recovered during the authorized assessment.

I used the **NetworkWalks Hash Calculator** to process the protected PDF and obtain a crackable representation of the password protection.

The resulting hash was then tested using the available password-recovery functionality.

### Steps Taken

The process followed was:

```text
Protected PDF
      ↓
NetworkWalks Hash Calculator
      ↓
Extracted Hash
      ↓
Password Recovery
      ↓
Password Recovered
      ↓
PDF Opened Successfully
```

### Result

The password for the first PDF was successfully recovered as:

```text
123456
```

The recovered password was then used to open the protected PDF successfully.

### Evidence

**Figure 4 — PDF Hash Extraction**

```text
evidence/04-pdf-hash.png
```

**Figure 5 — Password Recovery**

```text
evidence/05-password-recovered.png
```

**Figure 6 — Opened Patient Report**

```text
evidence/06-opened-report.png
```

### Impact

The use of a predictable password significantly reduced the effectiveness of the PDF's protection.

If an attacker obtains an encrypted copy of a sensitive document, a weak password may allow the document's contents to be recovered.

Because the document contained sensitive medical information, the potential confidentiality impact is significant.

### Recommendation

The organization should:

* Use strong randomly generated passwords
* Avoid predictable passwords
* Avoid sequential numeric passwords
* Never reuse passwords for sensitive documents
* Use appropriate encryption mechanisms
* Apply centralized access controls
* Protect sensitive documents both at rest and in transit

---

# 5. Attack Chain Summary

The assessment demonstrated the following attack path:

```text
1. Reconnaissance
        ↓
2. robots.txt discovered
        ↓
3. /patient/ directory identified
        ↓
4. Patient portal investigated
        ↓
5. MySQL error observed
        ↓
6. SQL injection identified
        ↓
7. Restricted patient area accessed
        ↓
8. Three patient reports identified
        ↓
9. PDF protection assessed
        ↓
10. PDF hash extracted
        ↓
11. Password successfully recovered
        ↓
12. Protected patient report opened
```

The assessment demonstrated that vulnerabilities should not always be considered individually.

A weakness in authentication can become significantly more serious when it provides access to sensitive documents, particularly when those documents are protected using weak passwords.

---

# 6. Risk Analysis

| Finding                            | Severity    | Potential Impact                                        |
| ---------------------------------- | ----------- | ------------------------------------------------------- |
| SQL Injection                      | 🔴 Critical | Authentication bypass and potential database compromise |
| Unauthorized Patient Report Access | 🔴 Critical | Exposure of confidential healthcare information         |
| Weak PDF Password                  | 🟠 High     | Recovery of protected medical documents                 |

### Risk Rating Key

🔴 **Critical** — Immediate remediation recommended

🟠 **High** — High-priority remediation recommended

🟡 **Medium** — Remediation should be planned

🟢 **Low** — Monitor and improve where appropriate

---

# 7. Recommendations and Remediation

## 7.1 Fix SQL Injection

The patient portal should use prepared statements or parameterized queries.

User input should never be directly incorporated into SQL statements.

---

## 7.2 Strengthen Authentication

The login system should properly validate authentication attempts and prevent manipulation of database queries through user input.

---

## 7.3 Strengthen Access Control

Authentication alone should not determine whether a user can access a patient record.

Every request for sensitive information should be authorized on the server.

---

## 7.4 Protect Patient Documents

Patient PDF files should not be directly accessible through predictable URLs or publicly accessible directories.

Documents should be served through an authenticated application endpoint that verifies authorization before returning the file.

---

## 7.5 Improve Password Security

Sensitive documents should not use simple passwords such as sequential numbers.

Strong, randomly generated passwords should be used where document-level password protection is required.

---

## 7.6 Disable Detailed Database Errors

The application should never expose raw MySQL errors to users.

Instead, users should receive a generic error message while detailed technical errors are stored securely in server logs.

---

## 7.7 Implement Security Monitoring

The organization should monitor:

* Failed login attempts
* Unusual authentication activity
* Repeated requests for patient reports
* Database errors
* Requests to restricted directories
* Suspicious access patterns

---

## 7.8 Conduct Regular Penetration Testing

After remediation, the application should undergo another security assessment to confirm that the identified vulnerabilities have been properly resolved.

---

# 8. Evidence

The evidence collected during the assessment should be organized as follows:

```text
evidence/
│
├── 01-patient-login.png
├── 02-sql-error.png
├── 03-patient-reports.png
├── 04-pdf-hash.png
├── 05-password-recovered.png
└── 06-opened-report.png
```

### Evidence Mapping

| Evidence                    | Description                                     |
| --------------------------- | ----------------------------------------------- |
| `01-patient-login.png`      | Patient portal login page                       |
| `02-sql-error.png`          | MySQL error observed during testing             |
| `03-patient-reports.png`    | Patient reports accessible after the compromise |
| `04-pdf-hash.png`           | PDF hash extraction                             |
| `05-password-recovered.png` | Successful password recovery                    |
| `06-opened-report.png`      | Protected PDF successfully opened               |

---

# 9. Key Lessons Learned

This assessment gave me practical experience in several areas of web application security.

### Web Reconnaissance

I learned how publicly accessible resources such as `robots.txt` can reveal useful information about an application's structure.

### SQL Injection

I gained practical understanding of how insecure handling of user input can expose database-driven applications to SQL injection.

### Authentication & Authorization

The assessment reinforced the difference between authentication and authorization and why both are important when protecting sensitive information.

### Sensitive Data Protection

I learned that sensitive healthcare information requires strong access controls and multiple layers of protection.

### Password Security

The PDF exercise demonstrated how weak passwords can reduce the effectiveness of encryption.

### Vulnerability Chaining

The most important lesson was seeing how multiple weaknesses can be connected to increase the overall impact of a compromise.

---

# 10. Conclusion

This Week 4 assessment gave me practical experience conducting a black-box web application penetration test within an authorized cybersecurity training environment.

I began with reconnaissance and discovered application paths through `robots.txt`. I then investigated the patient portal and identified a MySQL-related error that indicated an SQL injection vulnerability.

The identified weakness provided access to the restricted patient area, where three confidential patient reports were located.

I subsequently assessed the security of the PDF documents and successfully recovered the password protecting the first report. The recovered password allowed the protected document to be opened and verified.

The exercise demonstrated how vulnerabilities in different parts of an application can be chained together to create a much larger security impact.

My major takeaway from this assessment is that cybersecurity is not simply about finding vulnerabilities. It is also about understanding their impact, collecting evidence, documenting the findings clearly, and recommending practical remediation.

This project has strengthened my interest in **web application security, ethical hacking, vulnerability assessment, and penetration testing**, and I look forward to applying what I have learned in future cybersecurity projects.

---

# 👨‍💻 Author

**Ufot Daraobong Esthiet**

**Cybersecurity Trainee | Ethical Hacking | Footprinting | Scanning | Web Application Security**

**Training:** NetworkWalks
**Batch:** B082
**Week:** 4 Capstone Project

The PDF sample itself contains additional findings—username enumeration, PDF metadata, the `/old/` backup, and staff/shareholder information.  Those should only be added to **your** GitHub project if you actually performed and have evidence for those steps.
