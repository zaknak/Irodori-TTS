# AGENTS.md

## Goal

This repository is a fork of Irodori-TTS originally from Aratako/Irodori-TTS.

The original repository provides:

* Training and inference code for a Flow Matching-based TTS model
* Architecture based on Echo-TTS
* DACVAE continuous latent representation as generation target

This fork MUST:

* Introduce controlled modifications without breaking original behavior
* Follow specification-driven development
* Maintain reproducibility of training and inference

---

## Source of Truth

* Original behavior is defined by:

  * README.md
  * Existing implementation

* New or modified behavior MUST be defined in:

  * `docs/` directory

Rules:

* Do not infer specifications from assumptions
* Do not implement undocumented behavior
* If behavior is unclear, refer to existing implementation

---

## Specification-Driven Development (MANDATORY)

All changes MUST follow this order:

1. Create or update specification in `docs/`
2. Ensure spec is clear, explicit, and testable
3. Implement code based strictly on the spec

Do NOT:

* Implement first and document later
* Modify behavior without updating docs

---

## Constraints

* Do not break existing training or inference pipelines
* Do not remove existing features unless explicitly specified
* Maintain compatibility with existing checkpoints if possible
* Avoid unnecessary refactoring

---

## Coding Rules

* Follow existing code style and structure
* Reuse existing modules whenever possible
* Keep changes minimal and localized
* Do not introduce new dependencies unless documented in `docs/`

---

## Architecture Rules

* Respect existing architecture derived from Echo-TTS
* Do not redesign model structure unless specified in `docs/`
* Maintain compatibility with DACVAE latent representation

---

## Documentation Rules

All specifications in `docs/` MUST:

* Be explicit (no ambiguous wording)
* Define inputs / outputs clearly
* Describe expected behavior
* Include edge cases if relevant

Recommended structure:

* Overview
* Motivation
* Specification
* Constraints
* Examples

---

## Do

* Extend existing functionality
* Follow documented specifications strictly
* Keep implementation consistent with original design philosophy
* Validate changes against existing behavior

---

## Don't

* Do not implement undocumented features
* Do not rewrite large parts of the system without specification
* Do not introduce breaking changes silently
* Do not diverge from original architecture without justification

---

## Examples

### Correct

* Add a new feature AFTER defining it in `docs/`
* Modify inference behavior ONLY if documented
* Reuse existing training pipeline components

### Incorrect

* Adding new model layers without documentation
* Changing latent representation format silently
* Refactoring architecture without specification

---

## Priority

When conflicts occur, follow this priority:

1. Specification in `docs/`
2. Existing implementation
3. README.md
4. General assumptions

---

## Notes

This repository is NOT a greenfield project.

It is a controlled extension of an existing system.
All modifications must be traceable, documented, and justified.

