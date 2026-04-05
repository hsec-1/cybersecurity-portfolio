# OpenClaw AI Agent Security Audit & Research — April 2026

## Overview

Installed and configured OpenClaw, an open source autonomous AI agent framework, in an isolated VM environment. Conducted a security audit using the built-in tooling and reviewed published research on prompt injection vulnerabilities in agentic AI systems.

---

## Environment

- **Platform:** Ubuntu 25.10 VM (isolated, no personal accounts connected)
- **Model backend:** OpenRouter (free tier)
- **Purpose:** Evaluation and security research ahead of an OpenClaw community meetup

---

## What I Did

- Installed OpenClaw via the official install script on Ubuntu 25.10
- Configured API integration and debugged authentication issues by directly editing the JSON config file
- Ran `openclaw security audit` and reviewed findings
- Reviewed published security research from CrowdStrike, Kaspersky, Cisco and academic sources on OpenClaw vulnerabilities

---

## Security Audit Finding

Running `openclaw security audit` surfaced the following notable finding:

**Critical — Small model with web tools enabled:** The configured model was below the threshold recommended for tool-enabled agents. OpenClaw's own documentation states that models below this threshold have unacceptably high prompt injection susceptibility when given access to web tools such as `web_fetch`. This finding was noted but not remediated within the scope of this project, as the deployment remained sandboxed with no personal accounts connected, limiting the practical risk.

---

## Research Summary

Reviewing published research highlighted the following risks relevant to agentic AI deployments:

**Prompt injection** — Malicious instructions embedded in emails, documents or web pages can cause the agent to execute unintended actions without user awareness. This is particularly relevant when the agent has access to tools such as web fetch, shell execution or messaging platforms.

**Indirect prompt injection** — An attacker does not require direct access to the agent. Embedding malicious instructions in data the agent ingests (e.g. a malicious email sent to a connected inbox) is sufficient to influence agent behaviour. Researchers demonstrated extraction of private SSH keys via this method.

**Supply chain risk** — Third party skills downloaded from the OpenClaw skills catalogue have been documented causing silent data exfiltration. Skills are loaded with operator-level trust, meaning malicious skill content can issue commands as if authored by the operator.

**Model tier and susceptibility** — OpenClaw's documentation explicitly states that smaller and cheaper models are more susceptible to prompt injection and instruction hijacking. The recommendation is to use the latest generation, highest-tier model for any agent with tool access or untrusted input.

**Persistent backdoor via SOUL.md** — Researchers demonstrated that injected instructions can modify OpenClaw's persistent identity file, creating durable behavioural changes that survive restarts.

---

## Key Observation

The core security issue with agentic AI is that usefulness and security are in direct opposition. The more integrations and tool access an agent has, the more useful it becomes — and the larger the attack surface and ramifications of a breach. For a sandboxed deployment with no connected accounts this risk is manageable. For a deployment connected to email, messaging and file systems, the risk is significant and not yet well mitigated.

---

## Skills Demonstrated

`AI agent deployment` `Security auditing` `Threat research` `Risk assessment` `Prompt injection awareness` `API configuration`

---

[← Back to AI Security Research](README.md) | [← Back to Portfolio](../README.md)
