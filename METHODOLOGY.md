# AI-Assisted Documentation & Critical Evaluation

## Overview

AI assistance is used throughout this portfolio to help structure and articulate findings from hands-on work. This document describes the process — specifically the critical evaluation required to use AI assistance responsibly and accurately.

The goal is not to have AI write the portfolio, but to use it as a documentation tool while maintaining responsibility for accuracy, security and honest representation of the work done.

---

## Review Process

AI drafts are not accepted at face value. Every document in this portfolio goes through the following checks before publishing:

**Sensitive information review** — AI-generated drafts are checked for accidental disclosure of hostnames, subnet addresses, service identifiers, API configuration details, and brand names for security tools. Anything that could reveal specifics about the network environment or security tooling is removed or generalised.

**Accuracy review** — Technical claims, model names, version numbers, tool capabilities and configuration details are verified against actual results.

**Scope and framing review** — AI assistance has a tendency to overstate or embellish the scope of work done. Drafts are reviewed to ensure they accurately reflect what was actually completed, not an inflated version of it.

**Structural review** — AI-suggested structures are evaluated for whether they'll scale as the portfolio grows. Suggestions that prioritise short-term neatness over long-term usability are rejected.

---

## Examples of Issues Caught

The following are real examples of issues identified and corrected during the documentation process.

**Sensitive information disclosure**
- A TLS hostname containing a unique service configuration ID was included in a DNS Security document — removed before publishing
- Internal subnet addresses were included where generic descriptions were sufficient
- Brand names for VPN and password management tools were included unnecessarily

**Inaccurate framing**
- AI agent security work was described as "prompt injection research" when the actual work involved reading published research and running a built-in audit tool — corrected to accurately reflect scope
- A remediation step was described as a deliberate security fix when it was not the purpose of the change — corrected to reflect that the finding was noted but not remediated

**Technical inaccuracies**
- A model parameter count was referenced incorrectly throughout a document (26b written as 27b)
- A DNS provider's free tier capabilities were described inaccurately — verified via independent search and corrected
- Steps that had not yet been completed were included as if they had been — removed
- A response time metric was undocumented — added based on actual testing

---

## Observations on AI Limitations

Working with AI tools — both cloud-based assistants and local models tested in the home lab — has provided direct exposure to failure modes relevant to security contexts:

**Hallucination** — Models sometimes produce confident but incorrect information rather than acknowledging uncertainty. Smaller local models are particularly prone to this.

**Sycophancy** — Models can show a tendency to agree with the user regardless of accuracy, reversing correct positions when challenged. This is a known training artefact that varies by model size and capability.

**Security implication** — Both behaviours are particularly dangerous in security contexts. Acting on confidently incorrect technical information could have real consequences, which reinforces the need to treat AI outputs as a starting point for critical evaluation rather than a source of truth.

---

## Skills Demonstrated

`Critical evaluation of AI outputs` `AI-assisted documentation` `Information security (sensitive data handling)` `Technical accuracy review`

---

[← Back to Portfolio](README.md)
