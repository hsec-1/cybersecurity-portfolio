# AI-Assisted Documentation & Critical Evaluation

## Overview

AI assistance is used throughout this portfolio to help structure and articulate findings from hands-on work. This document describes the process — specifically the critical evaluation required to use AI assistance responsibly and accurately.

The goal is not to have AI write the portfolio, but to use it as a documentation tool while maintaining responsibility for accuracy, security and honest representation of the work done.

---

## Review Process

AI drafts are not accepted at face value. Every document in this portfolio goes through the following checks before publishing:

**Accuracy review** — Technical claims, model names, version numbers, tool capabilities and configuration details are verified against actual results.

**Sensitive information review** — AI-generated drafts are checked for accidental disclosure of hostnames, subnet addresses, service identifiers, API configuration details, and brand names for security tools. Anything that could reveal specifics about the network environment or security tooling is removed or generalised.

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

## Why This Process Matters

The review process above exists because AI tools have failure modes that are particularly dangerous in security contexts. Working with both cloud-based assistants and local models tested in the home lab has provided direct exposure to these:

**Hallucination** — Models sometimes produce confident but incorrect information rather than acknowledging uncertainty. Smaller local models are particularly prone to this. The technical inaccuracies caught in this portfolio — incorrect model parameters, fabricated configuration steps, inaccurate vendor capabilities — are all examples of this in practice.

**Sycophancy** — Models can show a tendency to agree with the user regardless of accuracy, reversing correct positions when challenged. This makes the framing and scope issues harder to catch, because the AI will readily agree that work was more extensive than it actually was and often err on the side of embellishment.

Acting on confidently incorrect technical information in a security context could have real consequences. The review process documented here is a direct response to that risk.

---

## Skills Demonstrated

`Critical evaluation of AI outputs` `AI-assisted documentation` `Information security (sensitive data handling)` `Technical accuracy review`

---

[← Back to Portfolio](README.md)
