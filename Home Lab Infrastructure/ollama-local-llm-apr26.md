# Local LLM Deployment with Ollama — April 2026

## Overview

Deployed Ollama on a Windows workstation and evaluated multiple open source large language models for use as a private, locally hosted inference backend. Models were evaluated for reasoning quality and inference speed relative to available hardware.

---

## Hardware

| Component | Spec |
|-----------|------|
| CPU | AMD Ryzen 5800x |
| RAM | 32GB DDR4 |
| GPU | NVIDIA RTX 3080Ti (12GB VRAM) |
| OS | Windows |

---

## What I Did

- Installed Ollama on Windows using the official installer
- Evaluated multiple models across different parameter sizes and architectures
- Assessed network exposure implications of making Ollama accessible across the local network before implementing — deferred pending further security consideration

---

## Model Evaluation

| Model | Architecture | Total Parameters | Active Parameters | Assessment |
|-------|-------------|-----------------|-------------------|------------|
| Gemma3:27b | Dense | 27B | 27B | Good reasoning, slow (~90s+/response) — spills into RAM |
| Gemma3:12b | Dense | 12B | 12B | Significant reasoning failures, unsuitable for technical use |
| Llama3.2:3b | Dense | 3B | 3B | Fast but unreliable, frequent hallucination |
| Gemma4:26b | Mixture of Experts | 26B | ~4B | Strong reasoning, ~45s/response — good balance of speed and quality |

**Selected: Gemma4:26b** — The Mixture of Experts architecture activates only ~4 billion parameters during inference despite having 26 billion total, delivering reasoning quality comparable to much larger dense models at a fraction of the compute cost. This makes it well suited to consumer hardware with limited VRAM.

---

## Key Finding — Mixture of Experts Architecture

The Gemma4:26b model demonstrated that architecture matters as much as raw parameter count for local inference. Traditional dense models activate all parameters for every inference pass, creating a hard relationship between model size and speed. MoE models route each input through a subset of specialised sub-networks, meaning a 26B parameter model can run at speeds closer to a 4B model.

For constrained hardware this is practically significant — it allows access to stronger reasoning capabilities without requiring proportionally more VRAM or RAM.

---

## Model Behaviour Observations

Testing smaller models revealed consistent failure patterns relevant to cybersecurity tooling decisions:

**Hallucination** — Smaller models confidently produced incorrect information when encountering knowledge gaps rather than acknowledging uncertainty. In one test, a 12b model incorrectly asserted that a smaller model would produce higher quality responses than a larger one, and maintained this position under initial challenge before eventually capitulating.

**Sycophancy** — Smaller models showed a strong tendency to agree with the user regardless of accuracy, reversing correct positions when challenged. This is a known training artefact less pronounced in larger models.

**Practical implication for security use** — Both behaviours are problematic in a security context. Acting on confidently incorrect technical information could have real consequences. Larger models are meaningfully better at expressing appropriate uncertainty and maintaining accurate positions under challenge.

---

## Privacy Considerations

Running local models means inference occurs entirely on-device with no data transmitted to third party APIs. This is relevant when working with sensitive information or when API data retention policies are a concern. The tradeoff is capability — consumer hardware local models are significantly less capable than frontier API models, though the gap is narrowing with architectures like MoE.

---

## Skills Demonstrated

`Local LLM deployment` `Model evaluation` `Architecture assessment` `Hardware constraint analysis`

---

[← Back to Home Lab Infrastructure](README.md) | [← Back to Portfolio](../README.md)
