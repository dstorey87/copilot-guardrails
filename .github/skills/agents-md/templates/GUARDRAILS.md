<!-- agents-md:begin -->
## Secure software standards

### Policy source and scope

Requirements are mapped from the owner-supplied Java sections 8.1-8.15 and SQL
sections 9.1-9.3 of the
[USPS Coding Secure Software Standards Procedure](https://blue.usps.gov/corptreasury/_pdf/paytech/coding-secure-software-standards-procedure.pdf).
This excerpt has not been independently authenticated against the intranet PDF;
no procedure version or effective date was supplied. This document guides coding
and does not certify existing code as compliant.

### Applicability and evidence

| Dimension | Status | Evidence and rationale |
|-----------|--------|------------------------|
| Java source | {{Present / Not found in inspected scope / Uncertain}} | {{Relative paths, source scope, declared Java version or unknown}} |
| Native SQL/PLSQL source | {{Present / Not found in inspected scope / Uncertain}} | {{Relative paths, production/test/deployment scope}} |
| Database access and query form | {{Native SQL / JPQL/HQL / ORM-only / procedure calls / none found / uncertain}} | {{Relative paths and actual access pattern; distinguish from local SQL bodies}} |

{{Describe inspected scope, exclusions, inaccessible modules, README/source
disagreements, and other uncertainty. Explicitly state no SQL found when
supported; do not claim absence after incomplete inspection.}}

### Applicable USPS requirements

{{Include applicable requirements from the bundled standards mapping with every
section identifier and nested requirement intact. For SQL 9.3 include all ten
metacharacters. For absent Java or SQL/database access explicitly mark the
corresponding sections not applicable with rationale. For uncertain findings
mark applicability pending and list evidence needed. Include the database-boundary
review requirements for ORM-only/JPQL even when native SQL source is absent.}}

### Implementation and compatibility notes

{{Keep modern implementation guidance visibly separate from policy. Include only
relevant notes and official links that resolve from this target. Explain binding
and validation as complementary controls, not a waiver of compiled procedures.
Flag unsupported Java mechanisms, invalid examples, and framework constraints.}}

### Exceptions and unresolved decisions

{{Preserve existing exception evidence. For each actual conflict record section,
scope/evidence, conflict, proposed disposition, rationale/controls, status,
approver/decision evidence or not supplied, and supplied review conditions or not
specified. If none are identified in this instruction-generation scope, say so
without claiming a full audit. Never fabricate approvals.}}

### Reassessment

Recheck applicability when Java, SQL scripts, embedded queries, ORM/database
access, framework constraints, or deployment runtimes change. New or unresolved
policy conflicts require an explicit decision; do not silently waive standards.
<!-- agents-md:end -->
