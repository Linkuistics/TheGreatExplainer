# TheGreatExplainer

> Automated documentation generation, tutorial creation, and instructional validation.

A [Linkuistics](https://github.com/linkuistics) project.

---

TheGreatExplainer generates technical documentation and tutorials that are paradigmatically appropriate, validated by execution, correctly sequenced, and adapted to the reader. It is a general-purpose documentation engine -- not scoped to any single project -- though its first customer is [APIAnyware-MacOS](https://github.com/linkuistics/APIAnyware-MacOS).

## Why TheGreatExplainer Exists

Most auto-generated documentation is technically correct but pedagogically useless. It explains *what* each function does but not *why* you'd use it, presents APIs in alphabetical order instead of conceptual order, and treats all readers as identical. Worse, code examples frequently don't compile because nobody validated them against the actual API.

TheGreatExplainer solves this by combining documentation generation with instructional design validation and execution verification. Every code snippet is compiled and run. Every tutorial is checked for correct prerequisite ordering. And the same conceptual tutorial is explained differently for each language paradigm -- a Haskell user reads about monadic resource management, not "create an object and call methods on it."

## Planned Capabilities

### Documentation Generation

- Generate API reference documentation from structured IR (not source code scraping)
- Paradigm-appropriate explanations -- OO, functional, monadic, relational, dependently-typed
- Cross-referenced with upstream documentation (e.g., Apple developer docs)

### Tutorial Generation

- Step-by-step tutorials from working sample applications
- Per-paradigm adaptation: the same concept explained through each language's lens
- Progressive complexity -- prerequisites before dependents, concepts before details

### Execution Validation

- Every code snippet compiled and run against the actual API
- Non-GUI steps executed in containers with the target language installed
- GUI steps executed in macOS VMs via [TestAnyware](https://github.com/linkuistics/TestAnyware)
- Expected output compared against actual output

### Instructional Design Validation

- Prerequisite ordering verification -- no concept used before it's introduced
- Circular dependency detection in explanation structure
- Knowledge gap analysis -- identifies missing explanations

### User Knowledge Modelling

- Track what the reader is assumed to know at each point
- Adapt explanation depth based on the reader's profile
- Integration with [TestSubject](https://github.com/linkuistics/TestSubject) for modelling specific learner profiles

## Multi-Stage Pipeline

```
Generate -> Validate -> Review -> Refine -> Re-validate -> Publish
```

Documentation passes through multiple stages. Execution validation catches technical errors. Instructional design validation catches pedagogical errors. The pipeline iterates until both are satisfied.

## First Customer: APIAnyware-MacOS

APIAnyware generates idiomatic bindings for 11+ languages across multiple paradigms. This provides a demanding set of requirements:

- **Inputs:** Enriched IR (JSON), generated bindings, sample apps, binding style metadata, Apple documentation URLs
- **Outputs:** API reference (Markdown/HTML), tutorials (Markdown/HTML), validation reports
- **Per-language configuration:** Each language has its own idioms, assumed knowledge, and key concepts

The same conceptual tutorial (e.g., "build a window with a button") is generated differently for each paradigm:
- **OO (Racket, Smalltalk):** Create instance, set properties, add to view hierarchy
- **Functional (Chez Scheme):** Call functions with parameters, compose results
- **Monadic (Haskell):** Use bracket for lifecycle management, sequence with do-notation
- **Relational (Prolog):** Declare relationships, query for the UI configuration

## Status

**Requirements phase.** The requirements document is complete ([docs/requirements.md](docs/requirements.md)). No implementation code exists yet.

## TheGreatExplainer is NOT

- A static site generator (it generates content; rendering is separate)
- A documentation linter (it generates documentation, not just checks existing docs)
- Scoped to APIAnyware (it is a general-purpose product)

## Related Projects

- **[APIAnyware-MacOS](https://github.com/linkuistics/APIAnyware-MacOS)** -- first customer; provides enriched IR, bindings, and sample apps
- **[TestAnyware](https://github.com/linkuistics/TestAnyware)** -- validates GUI tutorial steps in macOS VMs
- **[TestSubject](https://github.com/linkuistics/TestSubject)** -- models learner profiles for adaptive documentation (runtime integration)
- **[InTheLoop](https://github.com/linkuistics/InTheLoop)** -- interactive teaching tool that can use TheGreatExplainer's content

## License

Apache-2.0. See [LICENSE](LICENSE).
