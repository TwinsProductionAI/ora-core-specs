# ora-core-specs

Public technical specifications for ORA Core OS.

This repository is the specification layer of the public ORA Core map. It is for readers who want implementation-facing documents, white papers, module contracts, and integration notes without runtime code.

## Repository Role

Read this after [ora-core-os](https://github.com/TwinsProductionAI/ora-core-os) when you need the technical documents behind the architecture.

| Public order | Repository role |
| ---: | --- |
| 4 | Public specs, white papers, and integration notes. |

## Scope

This repository is the publication-ready public bundle for:

- H-NERONS factual governance specifications
- ORCHESTRATEUR_LLM orchestration specifications
- HGOV epistemic governance specifications
- GPV2 backend and semantic transport specifications
- glyph and Rosetta-related technical notes useful for implementation
- public white papers and integration notes

## Module Directories

- `specs/h-nerons`
- `specs/orchestrateur-llm`
- `specs/hgov`
- `specs/gpv2`

## Public Repository Map

| Order | Repository | Role |
| ---: | --- | --- |
| 1 | [ora-core-os](https://github.com/TwinsProductionAI/ora-core-os) | Architecture and canonical module order. |
| 2 | [ora-core-runtime](https://github.com/TwinsProductionAI/ora-core-runtime) | Runnable runtime and tests. |
| 3 | [ora-core-rag](https://github.com/TwinsProductionAI/ora-core-rag) | Retrieval layer and RAG Governor. |
| 4 | `ora-core-specs` | Technical specifications and white papers. |
| 5 | [grenaprompt-linked](https://github.com/TwinsProductionAI/grenaprompt-linked) | GL/GPL/GL_G language layer. |

## Public/Private Boundary

Public here:

- technical specifications
- white papers
- integration notes
- implementation-facing visual reference assets

Private elsewhere:

- PME deployment playbooks
- ChatGPT Projects client instruction packs
- commercial positioning material
- client-specific onboarding and delivery templates

## Important Publication Note

The public specs in this repository are publication profiles. They keep technical content while excluding private delivery material and client-specific deployment instructions.

## License

Technical specifications and assets published in this repository are released under Apache 2.0 unless stated otherwise. See `LICENSE` and `NOTICE`.

Trademark, naming, logo and branding rights are not granted. See `TRADEMARKS.md`.
