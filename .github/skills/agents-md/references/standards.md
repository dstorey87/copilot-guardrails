# Bundled USPS Java and SQL standards mapping

## Provenance and maintenance

Source: [USPS Coding Secure Software Standards Procedure](https://blue.usps.gov/corptreasury/_pdf/paytech/coding-secure-software-standards-procedure.pdf),
sections 8.1-8.15 and 9.1-9.3, as supplied by the repository owner.
This is a self-contained requirement mapping, not a full or independently
authenticated copy of the procedure. No version/effective date was supplied.

In the skill's source repository, root developers-checklist.md is canonical.
Update it and this mapping together. When distributing the skill, include this
entire folder with references and templates. Do not require access to the source
checkout at generation time. Generated GUARDRAILS.md must contain the applicable
requirements themselves, not merely links to a skill that may not be installed.

The following are USPS policy requirements. Compatibility guidance belongs in
separately labeled implementation notes; it cannot silently replace these rules.

## Java requirements

| USPS section | Requirement to include when Java applies |
|--------------|-----------------------------------------|
| 8.1 | Do not assume constructors ran or objects are initialized; protect non-initialized instance and static state. |
| 8.1.1 | Prevent access to non-initialized objects and check initialization before object behavior. |
| 8.1.1.1 | Make instance variables private; use getters/setters for necessary external access. |
| 8.1.1.2 | Add a private Boolean initialized flag per object, set it last in every constructor, and check it before non-constructor methods do work. Document exceptions for constructor-invoked helpers; prefer private helpers. |
| 8.1.2 | For classes with static initialization, protect non-initialized class state as well. |
| 8.1.2.1 | Make static variables private and use static accessors for necessary external access. |
| 8.1.2.2 | Add private static Boolean classInitialized; set the class flag last in static initialization. Check it before static methods and constructors do work, after required constructor chaining. Source terminology/flag ambiguity must be documented. |
| 8.2 | Default classes, methods, and variables to private; document the good reason for each nonprivate declaration. |
| 8.3 | Make classes and methods final whenever possible; document good reasons for nonfinal declarations. Nonpublic/package scope is not a substitute for security. |
| 8.4 | Protect packages against insertion and untrusted access, subject to the supplied mechanisms' runtime support. |
| 8.4.1 | The supplied defenses are java.security package.definition with RuntimePermission("defineClassInPackage."+package), or sealed JARs to restrict insertion. Do not claim universal enforcement. |
| 8.4.2 | The supplied access mechanism is java.security package.access with RuntimePermission("accessClassInPackage."+package), granting access only to specified code. Flag unsupported runtime enforcement. |
| 8.5 | Do not depend on package-private scope or inconsistent package closure to protect against hostile classes joining a package. |
| 8.6 | Avoid inner classes where possible; review enclosing-private-state exposure. Label the source's historical compiler/bytecode rationale as runtime-dependent. |
| 8.7 | Never sign code without a specific essential need. Minimize and specially audit code that acquires/uses privileges for dangerous operations. Do not assume unsigned code is sandboxed on current JVMs. |
| 8.8 | Protect signed classes from mixing with malicious classes, unintended combinations, or incompatible signed versions. |
| 8.8.1 | Put all signed code in one archive and sign the group; this is only partial mix-and-match mitigation. |
| 8.8.2 | Where the signing system permits inspection, verify surrounding classes' expected signers in static initialization. |
| 8.8.3 | Where cross-version mixing is a concern, use public final version stamps and verify surrounding classes' versions. |
| 8.9 | Prevent constructor-bypassing object cloning, including cloning enabled by subclasses. |
| 8.9.1 | Make classes noncloneable with a final clone rejection method as described by policy, but do not copy the invalid void clone() signature; resolve API compatibility explicitly. |
| 8.9.2 | Only permit cloning when necessary and risks are assessed/accepted. Make the clone implementation final, including a final forwarding override if otherwise inheriting a nonfinal implementation; use a valid return signature. |
| 8.10 | Make classes nonserializeable. The supplied rejection hook is private final void writeObject(ObjectOutputStream out) throwing IOException("Object cannot be serialized"). Intended necessary serialization requires an assessed exception; do not overstate hook enforcement. |
| 8.11 | Make classes nondeserializeable. The supplied rejection hook is private final void readObject(ObjectInputStream in) throwing IOException("Class cannot be deserialized"). Intended necessary deserialization requires an assessed exception; do not overstate hook enforcement. |
| 8.12 | Compare Class objects by identity/equality, not class-name strings. When name resolution is necessary, resolve with the intended class loader and compare Class objects, accounting for distinct same-named classes. |
| 8.13 | Never store secrets or cryptographic keys in application/library code. |
| 8.14 | Do not rely on code obfuscation for confidentiality or secrecy of embedded algorithms/data. |
| 8.15 | Prefer mutable arrays over immutable Strings for sensitive information; clear them at the earliest opportunity rather than relying on garbage collection. |

## SQL requirements

| USPS section | Requirement to include when SQL/database access applies |
|--------------|--------------------------------------------------------|
| 9.1 | Avoid dynamic SQL. Always use compiled procedures for updates; use compiled procedures for queries whenever possible. Review ORM-generated updates against this rule rather than assuming an exemption. |
| 9.2 | Do not include SQL-variant EVAL statements accepting partial or complete SQL in web applications. Mark the web-application condition explicitly. |
| 9.3 | Validate user data before SQL use; only permit single quote, double quote, vertical bar, semicolon, slash, backslash, percent, carriage return, line feed, and ASCII null when application logic requires them. |

For 9.3, retain the full metacharacter list in generated output, for example:

| Character | Name |
|-----------|------|
| `'` | Single quote |
| `"` | Double quote |
| `\|` | Vertical bar |
| `;` | Semicolon |
| `/` | Slash |
| `\` | Backslash |
| `%` | Percent |
| CR | Carriage return |
| LF | Line feed |
| NUL | ASCII null |

Label the following as complementary implementation guidance, not a policy waiver:
bind all untrusted data values; never concatenate them into SQL/JPQL/HQL.
Use fixed application-owned allowlists for identifiers and SQL structure that
cannot be bound. Review dynamic SQL within compiled procedures too. Field-specific
validation must not silently delete valid business data; validate/reject with an
explicit error or document permitted characters. Escaping/stripping alone is not
an injection defense. Parameter binding does not itself satisfy or waive 9.1.

## Conditional applicability and output

Use the workflow's Java/native SQL/database-access classifications. Copy the
applicable requirements into generated GUARDRAILS.md with their identifiers;
do not leave the requirement table here as the target's sole policy reference.
For conditional Java mechanisms (static initialization, signed archives, cloning,
serialization), retain the requirement and state whether its condition is present,
absent, or unknown. Do not invent evidence that every class complies.

When Java is absent, mark 8.1-8.15 not applicable with inspected-scope evidence.
When SQL and database access are absent, mark 9.1-9.3 not applicable and explicitly
record no SQL found. Uncertain classification means applicability is pending,
not waived. JPQL/HQL and ORM-only access require the boundary review described in
the workflow even if no native SQL/PLSQL source is found.
