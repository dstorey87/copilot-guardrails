# Developer's Checklist: Java and SQL

## Authority and scope

Source: [USPS Coding Secure Software Standards Procedure](https://blue.usps.gov/corptreasury/_pdf/paytech/coding-secure-software-standards-procedure.pdf).

This is a structured transcription of the Java and SQL requirements supplied by
the repository owner, covering sections 8.1-8.15 and 9.1-9.3 only. It is not the
complete procedure and has not been independently authenticated against the
intranet PDF. Wording is condensed; section identifiers and requirements are
retained. Do not infer a procedure version, effective date, or approval from this
copy. Other language checklists are outside this excerpt.

This file is the policy source of truth for the `agents-md` skill. Its bundled
[standards mapping](.github/skills/agents-md/references/standards.md) must be
updated together with this file. Compatibility notes are implementation guidance,
not replacements for USPS requirements or authorization to deviate.

## 8. Developer's checklist - Java language issues

### 8.1 Do not depend on initialization

Objects can be allocated without running their constructors. Do not assume that
an object was correctly initialized.

#### 8.1.1 Secure against access to non-initialized objects

- **8.1.1.1:** Make all instance variables private. Expose necessary access
  through get/set methods rather than direct access to non-initialized variables.
- **8.1.1.2:** Add a private Boolean `initialized` variable to each object. Each
  constructor must set it as its last action before returning. Each
  non-constructor method must verify initialization before doing anything.
  Exceptions may be needed for methods invoked by constructors; constructors
  should call only private methods in that case.

#### 8.1.2 Secure against access to non-initialized static classes

Apply these controls to classes with static initializers:

- **8.1.2.1:** Make all static variables private; expose necessary access through
  static get/set methods.
- **8.1.2.2:** Add private static Boolean `classInitialized`. Set the class flag
  at the end of static initialization. Each static method and constructor must
  verify class initialization before other work, after the mandatory superclass
  or same-class constructor call. The supplied text calls this a "static
  constructor" and refers to setting "initialized"; reconcile that terminology
  explicitly against Java's static initializer and `classInitialized` flag.

### 8.2 By default, make classes, methods, and variables private

Every nonprivate entry point can increase attack surface. Default to private;
document a good reason for each nonprivate class, method, or variable.

### 8.3 Whenever possible, make classes and methods final

Default classes and methods to final to prevent unsafe extension. Document a
good reason for nonfinal declarations. Nonpublic classes and package scope alone
are not security boundaries. Security can require limiting extensibility.

### 8.4 Protecting packages

#### 8.4.1 Protecting against package-insertion

The supplied procedure describes two defenses against rogue classes inserted
into a package:

- Configure `package.definition=Package#1 [,Package#2,...,Package#n]` in
  `java.security`, with `RuntimePermission("defineClassInPackage."+package)`
  controlling class definition.
- Alternatively, use a sealed JAR so the package cannot be extended by classes
  in other archives. The source refers readers to the J2SE EOL versions site.

#### 8.4.2 Protecting against package access

The supplied procedure describes
`package.access=Package#1 [,Package#2,...,Package#n]` in `java.security`, with
`RuntimePermission("accessClassInPackage."+package)` limiting package access
to permitted code.

### 8.5 Do not depend on package scope access restrictions

Do not treat default/package-private access as protection against attackers.
Rogue classes can join packages. Package closure support is inconsistent and
must not be assumed.

### 8.6 Do not use inner classes

Avoid inner classes where possible. The supplied rationale describes compilation
into separate classes, package exposure, and synthetic access to enclosing
private fields. It cites *Securing Java: Getting Down to Business with Mobile
Code* (1998). Assess that rationale against the target compiler/runtime rather
than treating historical bytecode behavior as universally current.

### 8.7 Avoid signing your code

Do not sign code without a specific, essential need. The supplied rationale
associates unsigned code with no special privileges. Minimize code that acquires
and uses privileges for dangerous operations and audit it more carefully.

### 8.8 Protect signed classes from mix-and-match attacks

Prevent adversaries from combining signed and malicious classes, or signed
classes not intended to work together:

- **8.8.1:** Put all signed code into one archive and sign it as a group. This
  only partially mitigates mix-and-match attacks.
- **8.8.2:** Where the signing system supports signer inspection, verify in
  static initialization that surrounding classes have the expected signer.
- **8.8.3:** Where cross-version mixing is a concern, put a version stamp in a
  public final variable in each class and verify surrounding classes' stamps.

### 8.9 Prevent attackers from cloning existing objects from memory

Cloning bypasses constructors and can expose unsafe object creation through
subclasses implementing `java.lang.Cloneable`.

- **8.9.1:** Make classes noncloneable; the supplied example declares a public
  final clone method throwing `CloneNotSupportedException`.
- **8.9.2:** If cloning is necessary and its risks are assessed and accepted,
  make the clone method final. If relying on an inherited nonfinal clone method,
  define a final forwarding override to prevent redefinition.

**Source example warning:** Both supplied examples use `public final void
clone()`, which cannot override `Object.clone()` (it returns `Object`).
The forwarding example also discards the cloned object. These examples are
recorded as policy defects, not executable recipes. Do not copy them into code;
resolve valid signatures and inheritance constraints explicitly.

### 8.10 Make your classes nonserializeable

Prevent serialization from revealing private state and referenced objects.
The supplied mechanism is a private final `writeObject(ObjectOutputStream out)`
method returning void and throwing `IOException("Object cannot be serialized")`.
Intended, necessary serialization is an explicit exception to assess.

### 8.11 Make your classes nondeserializeable

Prevent deserialization from constructing objects in uncontrolled states.
The supplied mechanism is a private final `readObject(ObjectInputStream in)`
method returning void and throwing `IOException("Class cannot be deserialized")`.
Intended, necessary deserialization is an explicit exception to assess.

The supplied rationale says final prevents subclass overrides of these hooks.
Private methods are not overridden in Java; record this limitation rather than
claiming these hooks prohibit every subclass or serialization mechanism.

### 8.12 Compare classes by equality, not by name

Compare `Class` objects directly, for example `a.getClass() == b.getClass()`,
rather than comparing class-name strings. Multiple class loaders can define
different classes with the same name. When resolving a class by name, use the
intended loader and compare the resulting `Class` identity; do not introduce
mix-and-match exposure through name-based comparisons.

### 8.13 Do not store secrets or keys in code

Never embed secrets, including cryptographic keys, in application or library
code. Anyone running or inspecting the code can recover them.

### 8.14 Code obfuscation is insufficient to make code secret

Obfuscation cannot provide data confidentiality or reliably conceal algorithms
from a dedicated adversary. Do not treat it as strong protection.

### 8.15 Clear sensitive information

Prefer mutable arrays over immutable Strings for credentials and other sensitive
information. Explicitly clear them at the earliest opportunity; garbage
collection may run late or never reclaim the memory.

## 9. Developer's checklist - SQL issues

### 9.1 Avoid use of dynamic SQL

- **Updates:** Always use compiled procedures rather than dynamic SQL.
- **Queries:** Whenever possible, use compiled procedures rather than dynamic SQL.

### 9.2 Avoid use of EVAL

Do not include SQL-variant `EVAL` statements that accept partial or complete SQL
statements in web applications.

### 9.3 Sanitize user input by removing metacharacters

Check user data for valid characters before using it in an SQL statement.
Only permit these characters when application logic requires them:

| Character | Meaning |
|-----------|---------|
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

Preserve this requirement. In implementation, parameter binding and field-specific
validation are complementary controls; stripping or escaping characters alone
does not prevent SQL injection. Do not silently corrupt legitimate input.

## Compatibility and approvals

Use the skill's [compatibility guidance](.github/skills/agents-md/references/compatibility.md)
to identify invalid examples, legacy Java assumptions, and framework conflicts.
An unsupported mechanism, different implementation, or security recommendation
does not itself authorize deviation. Record pending conflicts and seek approval
from the repository's authorized policy owner; never fabricate one.
