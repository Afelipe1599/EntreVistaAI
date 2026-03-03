# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

EntreVista AI is a **product specification project** (not a software codebase) for a Latin American SaaS platform that uses agentic AI to conduct screening interviews via Telegram with human-in-the-loop oversight.

**Target Market:** High-volume hiring companies (BPO, retail) and mid-market tech/SaaS firms in LATAM
**Core Value:** Agentic AI conducts dynamic screening interviews → generates structured evidence → human recruiter makes final decision

## Repository Structure

```
docs/           # Input: research and analysis documents
  overview.md   # Agentic interview platform analysis, regulatory landscape, case studies
  icp.md        # Ideal Customer Profile (buyer personas, pain points)
  mercado.md    # LATAM market analysis, competitive landscape

specs/          # Output: generated product specifications
  prd.md        # Complete Product Requirements Document (v1.0)

prompts-especificacion.md  # Co-creation methodology (three sequential prompts)
```

## Co-Creation Methodology

This project uses iterative co-creation with Claude AI as defined in `prompts-especificacion.md`. Follow these principles:

1. **Analyze conflicts first** - Review input documents for contradictions before generating
2. **Segment-by-segment production** - Produce one section, pause, wait for approval
3. **Document rationale** - Explain decisions and cite source documents
4. **No data invention** - Use "TBD" when information is missing; propose 2-3 reasonable options
5. **Human-in-the-loop** - User reviews and approves each segment before proceeding

## Specification Prompts

Three prompts are available in `prompts-especificacion.md`:

| Prompt | Purpose | Output |
|--------|---------|--------|
| Prompt 1 (PRD) | Product requirements | `specs/prd.md` ✅ Complete |
| Prompt 2 (Arquitectura) | Technical architecture | `specs/arquitectura.md` (pending) |
| Prompt 3 (Backlog) | Engineering backlog | `specs/backlog.md` (pending) |

## Current Status

- **PRD:** Complete (v1.0, all 13 segments approved)
- **Architecture:** Not yet created
- **Backlog:** Not yet created
- **Source Code:** None (specification phase only)

## Key Design Principles (Non-Negotiable)

1. **HITL Explicit** - AI recommends, human decides. No auto-reject/auto-advance.
2. **Transparency** - Candidates always know they talk to AI. Consent required.
3. **Auditable** - Every score linked to transcript quote. No black box.
4. **Anti-Hallucination** - Confined to knowledge base. Escalates unknowns.
5. **Privacy** - No biometrics, no emotion recognition, data purge policy.

## Language

All documentation is in **Spanish** (targeting LATAM market).
