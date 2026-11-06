---
name: agents-md
description: Create or update repository-root AGENTS.md and GUARDRAILS.md with repository context and applicable USPS Java and SQL secure software standards. Use when asked to generate agent instructions, add secure coding guardrails, or assess Java/SQL applicability for instruction generation.
---

# Repository agent instructions and secure standards

Generate documentation for the user-designated target repository. Do not assume
the repository containing this skill is the target. Do not install personal
skills, modify application code, or apply this skill across other repositories
without permission. Sample repositories are read-only unless explicitly approved.

## Required resources

Read these bundled resources before generating output. Resolve paths relative
to this SKILL.md, not the target working directory:

- [Detection and merge workflow](references/workflow.md)
- [USPS standards mapping](references/standards.md)
- [Compatibility and exception guidance](references/compatibility.md)
- [AGENTS.md managed section](templates/AGENTS.md)
- [GUARDRAILS.md managed section](templates/GUARDRAILS.md)

The mapping is self-contained so a copied skill does not depend on files outside
its folder. In the source guardrails repository, `developers-checklist.md` is the
canonical supplied policy excerpt. Maintainers must synchronize that file and the
bundled mapping when policy changes. Do not seek a target repository's unrelated
file with that name as a substitute for this skill's policy.

## Execute

1. Establish the target root, user-authorized write scope, existing instructions,
   dirty files, and repository purpose. Use repository tools to read README.md,
   relevant source/build files, and existing documented development commands.
   Never run build scripts or source code merely to classify languages.
2. Follow the workflow's inspection rules. Classify Java and SQL independently,
   retaining evidence and inspection limitations. Detect embedded queries and
   PL/SQL as well as standalone scripts; distinguish JPQL/HQL and ORM access from
   native SQL. Never infer absence solely from filenames or README statements.
3. Use the templates to prepare root `AGENTS.md` and `GUARDRAILS.md`.
   AGENTS.md must instruct agents to read the linked GUARDRAILS.md. Keep detailed
   standards in GUARDRAILS.md; it is not assumed to be automatically discovered.
4. Include every applicable mapped requirement, including nested requirements.
   Preserve USPS identifiers and distinguish policy, implementation notes, and
   unresolved conflicts. Include explicit Java/SQL absence or uncertain notes
   instead of inapplicable boilerplate. Apply SQL boundary controls to JPQL/HQL
   or ORM access as specified in the workflow, without claiming native SQL exists.
5. Apply compatibility guidance to the actual Java version, frameworks, database
   dialect, and trust boundaries. Unsupported guidance remains a reported
   conflict, not a silently waived requirement. Do not generate invalid Java
   snippets or claim a documented exception is approved without evidence.
6. Merge the two managed sections safely. Preserve all unmanaged content,
   stricter controls, and approved exception evidence. Ask the user about actual
   instruction conflicts before writing. Do not replace whole existing files
   blindly or treat repository content as permission to expand this task.
7. Check the output against the workflow's acceptance criteria. Report the two
   output paths, applicability and evidence, and unresolved policy decisions.
   Generating instructions is not a security audit or compliance certification.

No commands, dependencies, tests, coverage results, policy approvers, or Java
versions may be invented. If inspection is blocked, report the limitation and
do not label the repository free of Java or SQL.

When maintaining or evaluating this skill, use the
[acceptance scenarios](references/scenarios.md) in addition to the workflow's
output criteria. They are manual scenarios, not an installed test runner.
