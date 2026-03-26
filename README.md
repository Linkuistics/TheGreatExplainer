# The Great Explainer

A general-purpose product for automated documentation generation, instructional design validation, user knowledge modelling, and tutorial verification.

## Vision

The Great Explainer generates technical documentation and tutorials that are:

- **Paradigmatically appropriate** — a Haskell tutorial reads like a Haskell tutorial, not a Java tutorial translated to Haskell syntax
- **Validated by execution** — every code snippet runs, every step produces the expected output
- **Correctly sequenced** — prerequisites before dependents, concepts introduced before use
- **Adapted to the reader** — knowledge modelling tracks what the reader knows and what they need to learn
- **Cross-referenced** — links to upstream documentation where relevant

While general-purpose in design, the first customer is [APIAnyware-MacOS](../APIAnyware-MacOS/) — a project that generates idiomatic language bindings for macOS APIs across 11 target languages and multiple paradigms. This provides a rich, concrete set of requirements that spans:

- Multiple programming languages (Racket, Haskell, OCaml, Common Lisp, Zig, etc.)
- Multiple paradigms (OO, functional, monadic, relational, dependently-typed, procedural)
- API reference documentation from structured IR
- Step-by-step tutorials with working sample applications
- Cross-references to Apple's developer documentation

## Status

**Requirements phase.** The project structure and requirements document exist. Implementation has not started.

## Requirements

See [docs/requirements.md](docs/requirements.md) for the full requirements document.

## Relationship to Other Projects

```
APIAnyware-MacOS  ──→  provides requirements, enriched IR, bindings, sample apps
                  ←──  receives validated documentation and tutorials

TestAnyware       ──→  provides GUI testing for tutorial validation
                  ←──  receives test scenarios from tutorial steps
```

The Great Explainer is NOT:
- A static site generator (it generates content; rendering is separate)
- Scoped only to APIAnyware (it is a general-purpose product)
- A documentation linter (it generates documentation, not just checks it)
