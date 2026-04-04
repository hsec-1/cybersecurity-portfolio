# AI-Assisted Documentation & Critical Evaluation — April 2026

## Overview

Used an AI assistant to help document a day of hands-on cybersecurity and home lab work. This document captures that process — specifically the critical evaluation skills required to use AI assistance responsibly and accurately.

---

## Context

After completing a day of practical work covering VM deployment, network segmentation, DNS configuration, AI agent security research and local AI infrastructure, AI assistance was used to help structure and articulate the findings into portfolio documentation.

The goal was not to have AI write the portfolio, but to use it as a documentation tool while maintaining responsibility for accuracy, security and honest representation of the work done.

---

## What Critical Evaluation Looked Like in Practice

Using AI assistance for documentation is not a passive process. The following issues were identified and corrected during the review process:

**Sensitive information disclosure**
- The AI included a specific TLS hostname containing a unique service config ID in the DNS Security document — caught and removed before publishing
- Initial drafts referenced specific internal subnet addresses — assessed as low risk but replaced with generic descriptions for good practice
- Brand names for security tools (VPN provider, password manager) were removed as unnecessary disclosure

**Inaccurate framing**
- Initial documentation framed the AI agent security work as "prompt injection research" — this overstated what was actually done. The work involved reading published research and running a security audit tool, not conducting original research. Corrected to accurately reflect the scope.
- The DNS solution comparison table contained an inaccuracy about Control D's free tier ad blocking capabilities — identified, verified via independent search, and corrected.
- The OpenClaw security audit document described a remediation step that did not occur — the AI framed switching models as a deliberate security fix when it was not the purpose of switching models. Corrected to accurately reflect that the finding was noted but not remediated.

**Incomplete or inaccurate technical details**
- The local AI infrastructure document included steps that had not yet been completed (network configuration to expose Ollama across the local network, OpenClaw integration) — caught and removed
- The Gemma4:26b model was incorrectly referenced as Gemma4:27b throughout the document — caught and corrected
- The response time for Gemma4:26b was initially undocumented — corrected to ~45s based on actual testing

**Structural decisions**
- Pushed back on several subpar AI-suggested structures for the portfolio repository before implementing a logical topic-based organisation that will scale over time
- Identified that date-based folder naming made less sense than topic-based folders with dates in filenames for long term usability

---

## Observations on AI Limitations

As part of the day's work, multiple local large language models were tested and evaluated. This provided direct firsthand exposure to AI failure modes relevant to security contexts:

**Hallucination** — Smaller models confidently produced incorrect information when encountering knowledge gaps rather than acknowledging uncertainty. In one test, a model incorrectly asserted that a smaller model would produce higher quality outputs than a larger one, and then got confused regarding logic and previous statements.

**Sycophancy** — Smaller models showed a strong tendency to agree with the user regardless of accuracy, reversing correct positions when challenged. This is a known training artefact that is less pronounced in larger, more capable models.

**Security implication** — Both behaviours are particularly dangerous in security contexts. Acting on confidently incorrect technical information from an AI tool could have real consequences. This reinforces the need to treat AI outputs as a starting point for critical evaluation rather than a source of truth.

---

## Reflection

The ability to use AI tools effectively is a professional skill in its own right. However, effective use requires:

- Actively reviewing outputs rather than accepting them passively
- Verifying factual claims independently where accuracy matters
- Recognising when AI is overstating, understating or misrepresenting
- Maintaining responsibility for the final output regardless of how it was produced

---

## Skills Demonstrated

`Critical evaluation of AI outputs` `AI-assisted documentation` `Information security (sensitive data handling)` `Technical accuracy review`

---

[← Back to AI Security Research](README.md) | [← Back to Portfolio](../README.md)
