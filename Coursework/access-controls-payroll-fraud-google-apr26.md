# Access Controls — Payroll Fraud Investigation

**Scenario:**

*A deposit was made from the business to an unknown bank account. The finance manager denied making the transaction. Investigate the access logs to identify the threat actor and recommend mitigations.*

### Notes

The event log shows a payroll event adding 'FAUX_BANK' was executed on 10/03/2023 at 8:29:57 AM from IP address 152.207.255.255 under the Legal\Administrator account from a computer named 'Up2-NoGud'. Cross-referencing the employee directory identifies this IP address as belonging to Robert Taylor Jr., a legal contractor whose end date was 12/27/19 — over three years before the incident.

### Issues

- Robert Taylor Jr.'s account was not deprovisioned on his end date, leaving active admin credentials available to a threat actor more than three years after his contract ended
- All employees regardless of role are assigned admin authorisation, violating the principle of least privilege and creating unnecessary attack surface

### Recommendations

- Implement an offboarding process that automatically deprovisions accounts on the employee end date
- Implement role-based access control — admin privileges should not be a default for all users
- Implement MFA to prevent unauthorised use of compromised credentials
- Conduct regular audits of active credentials to identify and remove accounts that should no longer have access

---

## Skills Demonstrated

`Access log analysis` `Account lifecycle management` `Principle of least privilege` `Credential misuse investigation` `Root cause analysis`

---
[← Back to Coursework](README.md) | [← Back to Portfolio](../README.md)
