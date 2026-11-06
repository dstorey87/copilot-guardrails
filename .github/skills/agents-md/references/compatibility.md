# Compatibility notes and policy exceptions

These are implementation notes, not authority to replace USPS requirements.
Keep them visibly distinct in generated GUARDRAILS.md. Inspect the repository's
declared compiler/runtime, actual framework needs, trust boundaries, and database
dialect before making a recommendation.

## Java compatibility

| Sections | Issue and required handling |
|----------|-----------------------------|
| 8.1 | Constructor bypass and partial initialization need threat-aware review. Do not automatically inject flags or checks into every class. Flag framework construction, reentrancy, safe publication/concurrency, and callback conflicts; seek approval for a different control. Java has static initializer blocks, not static constructors. The source's static flag naming is inconsistent; use classInitialized in explanation and disclose the interpretation. |
| 8.2-8.3 | Top-level Java classes cannot be private, and required framework/API access or proxies may conflict with private/final defaults. Use the narrowest legal visibility and document the reason as policy requires. Record unresolved policy/framework conflicts; do not break framework contracts or claim exceptions without approval. |
| 8.4-8.5 | The Security Manager was deprecated for removal in Java 17 and permanently disabled in Java 24 (JEP 486). package.definition/package.access and RuntimePermission text must not be presented as reliable enforcement on unsupported runtimes or arbitrary class loaders. Sealing has different guarantees from access control. Assess supported mechanisms; isolate untrusted code at appropriate process/container boundaries, but do not label alternatives approved without evidence. |
| 8.6 | Legacy synthetic-access behavior is not universal: Java 11 introduced nest-based access control (JEP 181). Preserve the avoid-inner-classes requirement, label the historical rationale, and document actual exposure/framework constraints rather than claiming modern compilers make all private fields package-visible. |
| 8.7-8.8 | Unsigned Java code is not automatically unprivileged or sandboxed on modern JVMs. Signing can establish artifact provenance rather than grant runtime privilege. Do not remove required artifact signing or weaken supply-chain controls. Flag conflicts for policy-owner resolution; retain conditional archive, signer, and version checks. |
| 8.9 | Object.clone() returns Object; void clone() cannot override it. Use only a valid Object/covariant-return override if a code change is separately authorized. Consider inherited final methods, Cloneable, and subclass behavior. A final method does not make all instances immutable or eliminate every constructor-bypass mechanism. Never emit the policy's invalid example as runnable code. |
| 8.10-8.11 | Native Java serialization requires Serializable/Externalizable or special platform treatment; a nonserializable class is not made natively deserializable simply by receiving bytes. Private readObject/writeObject hooks are not overridden by subclasses; final does not globally prevent their alternative hooks/serialization paths. Review inherited serializability, Externalizable, records, replacement hooks, and framework formats separately. Reject unneeded native serialization; do not assume two hooks disable all mechanisms. Necessary serialization/deserialization needs an approved, scoped exception and suitable validation/filtering. |
| 8.12 | Class identity includes the defining loader. Class objects, not equal name strings, establish actual class identity. Do not copy malformed class-loading examples or infer authorization from a name alone. |
| 8.13-8.15 | Do not hardcode secrets, claim obfuscation protects them, or depend on garbage collection for prompt erasure. Prefer mutable data where supported; minimize lifetime/copies and clear in cleanup paths. Arrays do not guarantee removal of all runtime copies. Record unavoidable immutable credential handling without claiming perfect erasure. |

## SQL compatibility

- **9.1:** Compiled procedures are mandatory for updates and preferred for queries
  under the supplied policy. Prepared statements are an injection defense, not
  an automatic substitute authorized by this skill. Identify the actual database
  dialect and existing procedure/ORM boundary. Report a deviation or uncertainty
  without refactoring the application during instruction generation.
- **9.1-9.3:** Stored/compiled procedures can still construct injectable dynamic
  SQL. Bind procedure parameters and internal data values; constrain structural
  choices to approved allowlists. JPQL/HQL strings can also be injection targets.
- **9.2:** Preserve the web-application scope. If no web entry point exists,
  record that condition rather than inventing a ban on unrelated language eval
  functions as if it were the supplied SQL rule.
- **9.3:** Preserve all listed character restrictions and their business-logic
  exception. Do not implement indiscriminate character stripping that corrupts
  names, paths, or search values. Validate format/type/length and permitted
  characters at field boundaries; always bind data. Escaping and validation
  alone do not safely replace parameterization.

## Exception records

Include one record per real conflict, not a fictitious approval:

| Field | Required content |
|-------|------------------|
| USPS section | Exact affected identifier(s) |
| Scope/evidence | Repository-relative paths and affected behavior |
| Conflict | Policy requirement versus actual runtime/framework/business constraint |
| Proposed disposition | Proposed implementation, exception, or further evidence needed |
| Rationale and controls | Risk, justification, and compensating controls |
| Status | Pending, approved, rejected, or expired, supported by evidence |
| Approver/evidence | Authorized approver and supplied decision reference, or explicitly not supplied |
| Review conditions | Supplied expiry/review condition, or not specified; never invent dates |

A policy's own permission for a documented reason (for example nonfinal classes)
is not blanket permission to bypass other requirements. Distinguish such reasons
from exceptions needing approval. Do not invent an organizational approval chain.
If the user cannot authorize a deviation, leave it pending for their policy owner.
Instruction generation may finish with clearly reported pending decisions; do
not call the application compliant or implement the proposed workaround.

## Official implementation references

- [Oracle Secure Coding Guidelines for Java SE](https://www.oracle.com/java/technologies/javase/seccodeguide.html)
- [OpenJDK JEP 486: Permanently Disable the Security Manager](https://openjdk.org/jeps/486)
- [OpenJDK JEP 181: Nest-Based Access Control](https://openjdk.org/jeps/181)
- [Java Object API, including clone](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/lang/Object.html)
- [Java Object Serialization Specification](https://docs.oracle.com/en/java/javase/21/docs/specs/serialization/serial-arch.html)
- [OWASP SQL Injection Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)

Java 21 API links illustrate the compatibility issues; consult the target
runtime's matching official API/specification before prescribing code changes.
