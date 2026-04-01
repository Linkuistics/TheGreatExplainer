# TheGreatExplainer -- TODO

Next steps as Claude Code prompts, in recommended order.

---

## 1. Choose implementation language and set up project scaffolding

```
TheGreatExplainer is a documentation generation pipeline. Evaluate whether this should be
implemented in TypeScript (good for template/text manipulation, broad ecosystem), Rust (strong
typing, performance for validation), or Python (LLM integration, text processing). Consider
that it needs to: parse JSON IR, generate Markdown/HTML, run code snippets in containers,
integrate with TestSubject at runtime, and orchestrate an LLM-driven review pipeline. Set up
the chosen project structure with build tooling, linting, and a basic test harness.
```

## 2. Define the data model for structured inputs

```
Read docs/requirements.md sections 2.1 and 2.3. Design types/structs (in the chosen
implementation language) for the core data model: EnrichedIR, BindingStyleMetadata,
AppSpecification, LanguageConfig, and LearnerProfile. Write these to src/models/ with tests.
The data model must support the full integration contract described in the requirements
(enriched IR JSON, per-language config, app specs). Start with the input side only -- output
types come later.
```

## 3. Implement the documentation generator (core pipeline stage 1)

```
Read docs/requirements.md section 1.1. Implement the documentation generator that takes
enriched IR (JSON) and produces API reference documentation in Markdown. Start with a single
language target as proof of concept. The generator should: parse the enriched IR, extract
classes/methods/properties/protocols/enums, apply paradigm-appropriate templates, and produce
cross-referenced Markdown output. Do not implement tutorial generation yet -- just API
reference docs.
```

## 4. Implement paradigm adaptation engine

```
Read docs/requirements.md section 3.3. Implement the paradigm adaptation engine that presents
the same conceptual content differently for OO, functional, monadic, and relational paradigms.
This should be a pluggable system where each paradigm provides its own explanation templates
and terminology mappings. Test with at least three paradigms (OO, functional, monadic) using
the same source concept.
```

## 5. Implement tutorial generation (core pipeline stage 2)

```
Read docs/requirements.md section 1.2. Implement the tutorial generator that takes working
sample applications and produces step-by-step tutorials. Each tutorial must: explain the "why"
not just the "what", introduce concepts before using them, build incrementally, include
complete runnable code at each step, and use the paradigm adaptation engine for per-language
style. Start with a single sample app (Hello Window) across two paradigm styles.
```

## 6. Implement execution validation

```
Read docs/requirements.md section 1.3. Implement the execution validator that runs every code
snippet from generated tutorials in an isolated environment. For non-GUI steps, use containers
with the target language installed. For GUI steps, integrate with TestAnyware for macOS VM
execution. The validator should: extract code snippets from tutorials, run each snippet,
capture output, compare against expected output, and produce a validation report (JSON).
```

## 7. Implement instructional design validation

```
Read docs/requirements.md section 1.5. Implement the instructional design validator that
checks pedagogical structure: prerequisite ordering (no concept used before introduced),
circular dependency detection in explanations, knowledge gap analysis (missing explanations),
progressive complexity verification, and per-section learning objective verification. The
validator takes a tutorial and a LearnerProfile (from TestSubject) and produces a structural
review report.
```

## 8. Integrate TestSubject for user knowledge modelling

```
Read docs/requirements.md section 1.4. Integrate with TestSubject to model learner profiles.
TheGreatExplainer should: query TestSubject for the target audience's knowledge profile, use
that profile to calibrate explanation depth, avoid explaining concepts the reader already
knows, and identify knowledge gaps the tutorial must fill. This is a runtime integration --
TheGreatExplainer calls TestSubject APIs during generation.
```

## 9. Implement the multi-stage review pipeline

```
Read docs/requirements.md section 1.6. Wire together the full pipeline:
Generate -> Validate (execution) -> Review (structure) -> Refine -> Re-validate -> Publish.
Each stage can identify issues that feed back to earlier stages. The pipeline should support
LLM-driven refinement with human review gates. Implement pipeline orchestration, stage
transitions, feedback loops, and reporting.
```

## 10. End-to-end test with APIAnyware-MacOS

```
Read docs/requirements.md section 2 (full integration contract). Run the complete pipeline
against real APIAnyware-MacOS data: enriched IR for one framework, generated bindings for one
language, one sample app. Verify: API reference docs generated, tutorial generated, execution
validation passes, instructional design validation passes, cross-references to Apple docs are
correct. Fix any integration issues discovered.
```

## 11. Define output data model and rendering interface

```
Read docs/requirements.md section 2.2. Design the output data model: structured
representations for API reference pages, tutorial pages, and validation reports. Define a
clear rendering interface so that downstream consumers (static site generators, PDF renderers,
etc.) can produce final output from TheGreatExplainer's structured data. TheGreatExplainer
generates content, not presentation -- the output model must encode enough structure for any
renderer. Write types to src/models/ alongside input types, with tests.
```
