# Formant & Diphthong Dynamics

> **Tri-Platform Agent Skill** for Claude Desktop / Code, Grok CLI, and Google Antigravity / Gemini.  
> Formant Transitions and Diphthong Acoustic Analysis — Generates exhaustive Formant & Diphthong Dynamics reports specifying time-varying formant trajectories for FACE, PRICE, GOAT, MOUTH, CHOICE, consonant locus equations, and VSA.

---

## Overview

`formant-diphthong-dynamics` provides standardized capabilities across conversational AI platforms:
- 5-point time-normalized formant trajectory tracking (F1, F2, F3 from 20% to 80% duration).
- Consonant locus equations for plosive bursts (/b d g/, /p t k/).
- Euclidean Vowel Space Area (VSA) and Formant Centralization Ratio (FCR) calculation.
- Machine-readable formant_dynamics.json output specification.
- Tri-platform NTFS junctions connecting Claude, Grok, and Antigravity.
- Standard documentation suite: SKILL.md, HOW_TO_USE.txt, IMPLEMENTATION_PLAN.md, and README.md.

---

## Tri-Platform Architecture

Zero duplicate code across platforms. Canonical source resides in `.agents`:
- **Canonical Source**: `C:\Users\<you>\.agents\skills\formant-diphthong-dynamics`
- **Claude**: `C:\Users\<you>\.claude\skills\formant-diphthong-dynamics` (NTFS Junction)
- **Grok**: `C:\Users\<you>\.grok\skills\formant-diphthong-dynamics` (NTFS Junction)
- **Antigravity**: `C:\Users\<you>\.gemini\config\skills\formant-diphthong-dynamics` (NTFS Junction)

---

## Documentation Suite

- [`HOW_TO_USE.txt`](HOW_TO_USE.txt): Standardized user guide and prompt templates.
- [`IMPLEMENTATION_PLAN.md`](IMPLEMENTATION_PLAN.md): Feature checklist and roadmap.
- [`App Changes Tracker.html`](App%20Changes%20Tracker.html): Interactive visual version log.
- [`SKILL.md`](SKILL.md): Agent system instructions and triggers.
