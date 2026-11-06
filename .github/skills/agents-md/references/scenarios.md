# Skill acceptance scenarios

These are repeatable manual evaluation scenarios for the instruction-only skill,
not an automated scanner or evidence that arbitrary repositories are compliant.
Use temporary repositories/documents or read-only authorized samples. Never
modify sample application code to exercise generation.

| Scenario | Inspection input | Required outcome |
|----------|------------------|------------------|
| Java without database access | Authored Java, build configuration, no SQL or database access across inspected source | Include 8.1-8.15. Explicitly record no SQL code or database access found; mark 9.1-9.3 not applicable in that scope. |
| SQL only | SQL migration and PL/SQL package bodies/specifications, no Java | Include 9.1-9.3 with conditional scope. Mark 8.1-8.15 not applicable with source evidence. |
| Mixed | Authored Java and a grant/deployment SQL script | Include both checklists even if application Java uses only ORM. Identify the deployment SQL separately. |
| Neither | Documentation-only repository without application database code | Record both languages not found in inspected scope; no Java/SQL boilerplate. This skill's own examples/templates must not trigger detection. |
| Embedded native SQL only | Java JDBC or native query strings, no .sql files | SQL present; include both checklists. Cite query source, not a nonexistent script. |
| JPQL/HQL | Java entity query without nativeQuery, ORM entities and writes | Java present; distinguish JPQL/HQL from native SQL. State native SQL/PLSQL not found if supported, but include 9.1-9.3 database-boundary review. Do not waive 9.1 for ORM writes. |
| ORM-only | Entity/repository operations, no authored query text | Separate database access from native SQL source; retain database-boundary controls and assess compiled-procedure policy. |
| Empty or stale README | README missing detail or contradicting source | Classify from corroborated source; record missing context or disagreement. Do not edit README as a side effect. |
| Incomplete inspection | Inaccessible module or truncated results | Uncertain, with gaps and pending applicability; no confident no-SQL claim. |
| Existing unmanaged instructions | Human content before/after managed sections, or no markers yet | Preserve all existing bytes outside the managed section; append once when absent. Never weaken stricter instructions. |
| Repeat run | Identical evidence and existing managed documents | No content diff, duplicate sections, changing timestamps, or lost exception evidence. |
| Broken markers | Missing end, reversed, duplicate, or nested markers in either document | Stop before writing either document; ask for resolution. |
| Policy conflict | Unsupported JVM control, incompatible framework constraint, or unapproved ORM writes | Explain the exact section and evidence, preserve requirement, and record pending disposition without inventing approval. |
| Approved exception | Existing scoped decision with approver/evidence | Preserve decision, scope, controls, status, and supplied review conditions. Do not turn it into a broader exception. |
| Copied skill | Only this skill folder is available in another repository | All required resources resolve inside the folder. Generated target links must not depend on the source guardrails checkout. |

For each generation case, inspect both output files, confirm requirement coverage
against standards.md, verify relative links, and ensure no template placeholders
remain. Then repeat with unchanged inputs and compare document contents.

For SQL 9.3, independently confirm all ten character entries survive generation.
For Java, check nested requirements as well as top-level section numbers.
Keep compatibility notes separate and ensure invalid source examples are never
presented as compilable Java.
