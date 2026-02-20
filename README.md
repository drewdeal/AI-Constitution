# AI Constitution

This repository contains an open AI Constitution template designed to serve as a
foundational governance layer for AI systems, autonomous agents, and developer
platforms.

The Constitution provides:

- Core values and guiding principles
- Behavioral directives
- Safety and risk policies
- Persona and identity rules
- Interaction guidelines
- Autonomy and agent constraints
- Governance and versioning structure
- Extension modules for domain-specific policies

## Purpose

The goal of this Constitution is to offer a clear, adaptable, and permissive
framework that can be embedded into AI projects at any scale. It is written to
be technology-agnostic and model-agnostic, suitable for LLMs, agents, and
multi-persona systems.

This Constitution is released under a **CC0 Public Domain Dedication** so that
anyone may freely copy, modify, extend, or incorporate it into their own work —
including commercial and closed-source systems — without restriction.

## Files

- `constitution.md` — The core Constitution (clean, non-annotated)
- `constitution-annotated.md` — Commentary version explaining rationale behind each section
- `LICENSE` — CC0 Public Domain Dedication
- `.gitignore` — Git ignore rules suitable for general development
- `constitution.yaml` - Machine readable (YAML) of the core version
- `constitution-annotated.yaml` — Machine readable (YAML) commentary version explaining rationale
- `extensions/` — Domain-specific extension modules

### Extensions

- `extensions/openclaw-testing-requirements.md` — Testing and quality assurance requirements for OpenClaw development workflows
- `extensions/openclaw-testing-requirements.yaml` — Machine-readable version of OpenClaw testing requirements

## Usage

You may:

- Adopt the Constitution as-is
- Modify it to suit your domain
- Extend it with organization-specific guardrails
- Integrate it into system prompts, agent configs, or policy layers
- Embed it into documentation or governance structures

### Using Extensions

Extensions provide domain-specific policies that complement the core Constitution. To use an extension:

1. Review the base Constitution to understand core principles
2. Select relevant extensions for your use case (e.g., `openclaw-testing-requirements` for development workflows)
3. Integrate both the Constitution and extensions into your AI system's configuration
4. Customize thresholds and requirements to match your project's needs

The OpenClaw Testing Requirements extension demonstrates how to apply the Constitution's core values (competence, security, honesty) to ensure AI agents maintain adequate test coverage for critical code paths.

## Contribution

Because the Constitution is public domain, contributions are optional and
non-binding. If you wish to provide improvements, you may open pull requests or
fork the project freely.

## License

This work is dedicated to the public domain under the CC0 1.0 Universal license.
See the LICENSE.txt file for details.
