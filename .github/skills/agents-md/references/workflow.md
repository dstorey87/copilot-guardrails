# Inspection, applicability, and safe updates

## Repository context

Resolve the user-designated repository root before reading or writing. Honor
existing root and scoped agent instructions. Inspect existing AGENTS.md,
GUARDRAILS.md, README.md, build descriptors, documented commands, and relevant
source layouts. Report missing documentation instead of inventing it.

Record purpose, key paths, and established development/test commands with their
evidence. Do not copy credentials, sensitive configuration values, full code
extracts, or machine-specific absolute paths into generated documents. Never
execute SQL, project scripts, or application code to determine applicability.

## Inspection scope

Use version-controlled files plus relevant user-authored untracked source.
Honor repository ignore rules by default, but report known relevant ignored or
inaccessible source as a limitation. Inspect referenced modules when they are
inside the authorized target. Do not follow symlinks or submodules outside that
scope without permission.

Exclude .git internals, dependency/vendor directories, virtual environments,
compiled/generated outputs, caches, and the skill's own policy/templates/examples.
Do not count README code examples or generated guardrails as application code.
Include authored tests, migrations, deployment SQL, database grants, and build
source sets when relevant. Record when SQL exists only in tests or deployment.

Do not claim absence after a truncated search or a first-N filename sample.
Enumerate the relevant file inventory before making negative findings. Large
repositories may be inspected in batches; retain gaps as uncertain.

## Evidence-led classification

Read README technology, database, and architecture sections as human-maintained
context; corroborate them with source and build configuration. README-only claims
are not proof of implementation. Empty, missing, or stale README content must
not prevent classification from source. Report README/source disagreements.

### Java

Inspect authored .java files and declared source sets. Corroborate with pom.xml,
Maven parent/modules, build.gradle/build.gradle.kts, toolchains, compiler release
settings, and deployment runtime configuration. A build descriptor alone does
not establish Java source presence. Kotlin or Scala on a JVM is not Java source.
Distinguish main, test-only, and generated-only Java.

Record the declared Java version and constraints where supported by evidence;
contradictory compiler/runtime declarations remain unresolved. Do not infer a
Java version from Spring Boot or a filename alone.

### SQL and database access

Inspect .sql, .pks, .pkb, .pls, .plsql and repository-specific database formats.
Look at content, not extensions alone: scripts, DDL, DML, packages, procedures,
triggers, views, grants, migration XML/YAML/JSON, and database deployment assets.
Do not execute them.

Inspect application sources and resources for embedded query construction:
JDBC Statement/PreparedStatement/CallableStatement, Spring JDBC, @Query and
nativeQuery flags, entity-manager native queries, MyBatis mappings, jOOQ/other
query builders, stored-procedure calls, and SQL strings in other languages.
Search hits are leads: read surrounding code to distinguish actual queries from
comments, examples, safe bindings, and unrelated strings. Include dynamic SQL
inside stored procedures. This is classification, not an injection audit.

Record these dimensions separately:

| Dimension | Evidence examples |
|-----------|-------------------|
| Native SQL/PLSQL source | Authored scripts/packages, migration statements, native SQL strings |
| Database access | JDBC, stored-procedure calls, JPQL/HQL, ORM entities/repositories |
| Query form | Static native SQL, dynamic native SQL, JPQL/HQL, ORM-generated only, procedure invocation |
| Location | Production source, tests, migrations, database/deployment assets |

JPQL/HQL is not native SQL. ORM mappings, datasource dependencies, and a README
database mention do not alone prove handwritten SQL exists. A stored-procedure
call establishes database access but does not prove its procedure body is local.

### Applicability decisions

For Java and native SQL/PLSQL independently, choose `Present`,
`Not found in inspected scope`, or `Uncertain`, with repository-relative evidence
or an explicit inspection boundary. Also record database access and query form.

- Java present: include all sections 8.1-8.15, including conditional requirements
  and their actual applicability. Java absent: give an explicit not-applicable
  note instead of copying Java rules.
- Native SQL/PLSQL present: include 9.1-9.3, stating which rules are conditional
  (for example 9.2 applies to web applications).
- JPQL/HQL or ORM-only database access without native SQL: explicitly say
  "No native SQL/PLSQL code found in the inspected scope" and identify the
  database boundary. Include 9.1-9.3 as database-access review requirements:
  assess updates and queries against 9.1, prohibit unsafe query construction and
  EVAL where applicable, and require binding/validation at query boundaries.
  Do not call ORM-generated updates compiled procedures or automatically exempt
  them. Record a 9.1 conflict if supported by source and not already approved.
- Neither SQL nor database access found: explicitly say
  "No SQL code or database access found in the inspected scope"; mark 9.1-9.3
  not applicable based on that scope, and require reassessment if either is added.
- README-only database claims or incomplete inspection: use uncertain, describe
  what remains to inspect, and list 9.1-9.3 applicability as pending rather than
  claiming no SQL or resolved compliance.

If Java applicability is uncertain, list sections 8.1-8.15 as pending and identify
the evidence needed; do not fabricate runtime-specific controls.

## Managed document updates

Use exactly one marker pair per target file:

```text
<!-- agents-md:begin -->
<!-- agents-md:end -->
```

In AGENTS.md and GUARDRAILS.md, update only the content between the markers.
For a new file, use a descriptive heading and the corresponding template.
For an existing file without markers, preserve its bytes and append a separated
managed section. Never overwrite an existing human-authored file with a template.
Preserve the file's line endings where practical.

Before any writes, read both files and prepare both merges. If markers are
missing a partner, duplicated, reversed, or nested, stop and ask for resolution.
Do not guess a replacement range. Respect the user's unsaved drafts and edits.

Review existing unmanaged AND managed content for stricter requirements,
exceptions, approval evidence, and conflicts. Keep user-owned additions in a
managed section unless clearly superseded by an approved change. A previous run
does not authorize deleting approved exceptions. Existing template-like text is
not permission to discard real repository instructions.

Compare the proposed policy with existing instructions. Explain an actual
conflict and ask for a decision before writing either file; do not silently
weaken the stronger control or override instruction precedence. Preserve scoped
AGENTS.md files; do not create or rewrite them as part of this root-only task.

Use stable ordering and repository-relative paths. Do not add a changing
timestamp or random ID on every run. When evidence and instructions have not
changed, leave the files unchanged. Never leave placeholder tokens in output.
Write both complete documents before claiming generation is finished; surface
partial write failures and do not claim success.

## Acceptance criteria

- AGENTS.md contains repository purpose, key paths, evidence-backed commands (or
  an explicit absence note), applicability summary, and an instruction to read
  the relative GUARDRAILS.md link before changing applicable code.
- GUARDRAILS.md contains separate Java/native SQL/database access findings,
  source paths, inspection boundaries, applicable numbered policy requirements,
  compatibility notes, and unresolved/approved exception records.
- All 8.1-8.15 and 9.1-9.3 requirements are either included when applicable or
  explicitly marked not applicable/pending with rationale. No SQL absence is
  inferred from an empty extension search alone.
- Every copied rule retains its USPS identifier and separates policy from
  implementation notes. Links work from the target repository; do not leave
  links to this skill's uninstalled references or canonical checkout.
- Existing human instructions, stronger controls, and exception evidence survive
  the merge. Marker counts/order are valid. A second run with unchanged inputs
  makes no diff.
- No application code, secrets, database state, JVM configuration, personal skill
  directories, or unauthorized repository files are changed.
- Report instruction generation, not compliance certification, test coverage,
  or a vulnerability assessment.
