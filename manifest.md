# Project Manifest

## Project overview

This repository distributes GitHub Copilot development guardrails and a
repository-local `agents-md` skill for generating repository instructions with
applicable USPS Java and SQL secure coding standards. It is documentation-only;
it has no application runtime, database service, or executable generator.

## Directory structure and components

| Location | Purpose |
|----------|---------|
| `.github/copilot-instructions.md` | General development instructions |
| `.github/instructions/` | Bug handling, testing, research, and documentation rules |
| `.github/skills/agents-md/SKILL.md` | Agent instruction generation workflow |
| `.github/skills/agents-md/references/` | Detection, merging, bundled policy mapping, compatibility guidance, and acceptance scenarios |
| `.github/skills/agents-md/templates/` | Managed AGENTS.md and GUARDRAILS.md sections for target repositories |
| `developers-checklist.md` | Canonical owner-supplied USPS Java/SQL policy excerpt |
| `README.md` | Public usage and setup documentation |
| `MCP-SETUP.md` | Existing optional MCP setup guidance |
| `LICENSE` | Repository license |
| `manifest.md` | Repository inventory and status |

## Dependencies and setup

No package/runtime dependencies or environment variables are required by the
skill. Use a Copilot surface supporting repository skills and grant access to the
target repository. Clone this repository and use the bundled skill, or copy the
entire `.github/skills/agents-md` folder into an authorized target repository's
`.github/skills` directory. No personal installation is performed.

Optional MCP integrations are described in MCP-SETUP.md; they are not required
for this instruction-only skill. There is no build, deployment, application
startup, or configured automated test command in this repository.

## Current status

- Existing general guardrail instructions remain unchanged.
- The repository skill generates root AGENTS.md linking to detailed GUARDRAILS.md.
- Java/native SQL applicability uses README plus source evidence, with separate
  database-access classification, explicit absence/uncertainty, safe merges,
  and policy compatibility/exception records.
- Sample repositories used for applicability review are read-only.

## Known limitations

- The USPS excerpt was supplied by the owner; the intranet PDF has not been
  independently authenticated. Its version and effective date are unknown.
- Historical Java guidance and invalid clone examples require explicit
  compatibility handling, not automatic changes or unapproved policy waivers.
- Agent-driven inspection and document generation are not a deterministic
  scanner, a security audit, or a compliance certification.
- There is no automated skill-evaluation runner or code-coverage metric.

## Maintenance and validation

Update developers-checklist.md and the bundled standards mapping together.
Preserve section identifiers and verify all applicable requirements are emitted.
Review source detection, relative links, self-contained packaging, existing
instruction preservation, and unchanged-input repeat runs when changing the
skill. Exercise Java-only, SQL-only, mixed, neither, embedded SQL, ORM-only,
stale/empty README, incomplete scope, and conflict scenarios.

## Architecture decisions and recent changes

- Keep the skill in version control only; do not install a personal copy.
- Use AGENTS.md as the discoverable entry point and GUARDRAILS.md for details.
- Bundle a self-contained policy mapping so copied skills remain usable.
- Preserve USPS requirements separately from modern compatibility guidance and
  require evidence for approved exceptions.
- Added the Java/SQL policy excerpt, skill resources/templates, and usage docs.

## Resources

- [Usage](README.md#java-and-sql-repository-instructions-skill)
- [Policy excerpt](developers-checklist.md)
- [Skill workflow](.github/skills/agents-md/SKILL.md)
- [Compatibility references](.github/skills/agents-md/references/compatibility.md)
