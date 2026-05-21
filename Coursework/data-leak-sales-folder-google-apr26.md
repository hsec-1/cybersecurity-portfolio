# Data Leak — Sales Folder Exposure

**Scenario:**

*A sales manager shared access to a folder of internal-only documents with their team during a meeting. The folder contained files associated with a new product that has not been publicly announced. It also included customer analytics and promotional materials. After the meeting, the manager did not revoke access to the internal folder, but warned the team to wait for approval before sharing the promotional materials with others. During a video call with a business partner, a member of the sales team forgot the warning from their manager. The sales representative intended to share a link to the promotional materials so that the business partner could circulate the materials to their customers. However, the sales representative accidentally shared a link to the internal folder instead. Later, the business partner posted the link on their company's social media page assuming that it was the promotional materials.*

### Issue(s)

*What factors contributed to the information leak?*

The root cause was the failure to revoke folder access once the meeting ended. Access was granted for the meeting but remained active afterwards, leaving the link available for accidental sharing. A verbal warning to the team was the only control preventing further sharing, which relies on memory rather than enforcement.

### Review

*What does NIST SP 800-53: AC-6 address?*

NIST SP 800-53: AC-6 addresses the principle of least privilege, where a user must be identified and only granted the least access required to perform their function. It suggests controls such as role-based restriction and automatic access revocation as enhancements to bolster security posture.

### Recommendation(s)

*How might the principle of least privilege be improved at the company?*

PoLP Improvements:

1. Ability to share for set time with automatic revocation
2. Role-based access restrictions
3. Structural separation of sensitive and non-sensitive data

### Justification

*How might these improvements address the issues?*

1. Automatic revocation removes reliance on manual offboarding and would have closed access at the end of the meeting, preventing the incident.
2. Role-based access restriction creates a baseline to ensure that users do not have access to information they do not need to fulfil their function.
3. Structural separation of data categories reduces the consequences of accidental sharing by keeping confidential material out of folders used for routine external sharing.

---

## Skills Demonstrated

`NIST SP 800-53` `Principle of least privilege` `Access control` `Root cause analysis`

---

[← Back to Coursework](README.md) | [← Back to Portfolio](../README.md)