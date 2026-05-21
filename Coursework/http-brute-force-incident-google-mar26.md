# Security Incident Report — HTTP & Brute Force Attack

**Scenario:**

*Customers report being prompted to download a suspicious file when visiting a website. Analyse traffic logs to document the incident and recommend remediation.*

### Network protocol involved

HTTP was the internet protocol involved in this incident. From viewing the tcpdump log we can see HTTP requests to GET files from yummyrecipesforme before a large volume of traffic on port 80 (HTTP). Following the traffic on port 80, the next request is a DNS request for greatrecipesforme.com. Following the connection to greatrecipes we see a further HTTP GET request followed by significant traffic on port 80. Suspect that this further traffic is the download of malware.

### Incident documentation

Incident occurred several hours ago. Customers contacted the support team complaining of being prompted to download a file when loading yummyrecipesforme.com and that their computers were running slowly after the download.

The cybersecurity team performed the following tasks to assess the incident:

- Ran network analysis in a sandbox to observe the suspicious behaviour
- It appears that admin access to the web server was obtained by a malicious actor
- We discovered that default credentials were not changed and therefore suspect that access was gained through a brute force attack
- After altering the website source code, the malicious actor changed the admin password, locking out the authorised user
- The threat actor used admin access to alter website source code and insert malicious JavaScript prompting users to download and run a file
- The file contained further malicious JavaScript that redirected users to greatrecipesforme.com
- Senior analyst has confirmed that this website is hosting malware

### Recommended remediation

- Implement password policies
- Implement CAPTCHA for admin access
- Implement MFA for admin access

---

## Skills Demonstrated

`Incident reconstruction` `tcpdump analysis` `HTTP` `DNS` `Brute force attack investigation` `Malware redirect chain analysis` `Sandbox analysis`

---

[← Back to Coursework](README.md) | [← Back to Portfolio](../README.md)
