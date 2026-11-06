# GitHub Copilot Guardrails System

> **Transform GitHub Copilot into a zero-tolerance, research-driven, professional AI developer**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![GitHub Copilot](https://img.shields.io/badge/GitHub%20Copilot-Compatible-blue)](https://github.com/features/copilot)
[![MCP Compatible](https://img.shields.io/badge/MCP-Compatible-green)](https://modelcontextprotocol.io)

## What Is This?

This repository contains a comprehensive set of **guardrails** for GitHub Copilot that enforce professional software development practices. These are not suggestions—they are **hardwired rules** that make Copilot:

✅ **Zero-tolerance for bugs** - Loops until issues are fixed  
✅ **Research-driven** - Searches for best practices before implementing  
✅ **Test-obsessed** - Requires 80%+ coverage on all code  
✅ **Documentation-first** - Maintains manifest and docs automatically  
✅ **Security-aware** - Checks for vulnerabilities before shipping  
✅ **Context-aware** - Manages complexity and suggests repo splits  

## Why You Need This

### The Problem

Out-of-the-box, GitHub Copilot can:
- ❌ Write code with bugs and move on
- ❌ Use outdated patterns from its training data
- ❌ Skip tests entirely
- ❌ Leave projects poorly documented
- ❌ Ignore security best practices
- ❌ Create unmaintainable messes

### The Solution

With these guardrails, Copilot becomes a **disciplined professional developer** that:
- ✅ Stops when it encounters bugs and fixes them before proceeding
- ✅ Researches current best practices (October 2025) before implementing
- ✅ Writes comprehensive tests with every feature
- ✅ Maintains clear documentation and manifests
- ✅ Validates security at every step
- ✅ Manages technical complexity proactively

## Quick Start

### Option 1: Use in Your Existing Repository

```bash
# 1. Navigate to your repository
cd your-project

# 2. Create .github directory if it doesn't exist
mkdir -p .github/instructions

# 3. Download the guardrails
curl -o .github/copilot-instructions.md \
  https://raw.githubusercontent.com/dstorey87/copilot-guardrails/main/.github/copilot-instructions.md

# 4. Download specific instruction files
curl -o .github/instructions/zero-tolerance.instructions.md \
  https://raw.githubusercontent.com/dstorey87/copilot-guardrails/main/.github/instructions/zero-tolerance.instructions.md

curl -o .github/instructions/testing.instructions.md \
  https://raw.githubusercontent.com/dstorey87/copilot-guardrails/main/.github/instructions/testing.instructions.md

curl -o .github/instructions/research.instructions.md \
  https://raw.githubusercontent.com/dstorey87/copilot-guardrails/main/.github/instructions/research.instructions.md

curl -o .github/instructions/documentation.instructions.md \
  https://raw.githubusercontent.com/dstorey87/copilot-guardrails/main/.github/instructions/documentation.instructions.md

# 5. Create your manifest
touch manifest.md
```

### Option 2: Start a New Project With Guardrails

```bash
# 1. Clone this repository as a template
git clone https://github.com/dstorey87/copilot-guardrails.git my-new-project
cd my-new-project

# 2. Remove the git history and start fresh
rm -rf .git
git init

# 3. Customize for your project
# Edit manifest.md, README.md, etc.

# 4. Start coding with guardrails active!
```

## What's Included

### Java and SQL Repository Instructions Skill

The repository-local [`agents-md` skill](.github/skills/agents-md/SKILL.md)
creates or safely updates a target repository's root `AGENTS.md` and
`GUARDRAILS.md`. `AGENTS.md` provides repository context and explicitly directs
agents to the detailed standards in `GUARDRAILS.md`; the latter is not assumed
to be automatically discovered.

Ask Copilot, for example:

```text
Use the agents-md skill to create or update AGENTS.md and GUARDRAILS.md
for this repository. Determine Java and SQL applicability from README.md
and source files, and preserve existing instructions.
```

Use a Copilot surface supporting repository skills. To reuse it elsewhere, copy
the **entire** `.github/skills/agents-md` folder, including `references` and
`templates`, into the target repository's `.github/skills` directory. This is a
repository skill, not a personal installation, and it has no runtime dependencies.
See [GitHub's skill documentation](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/add-skills)
for supported locations.

The skill corroborates README descriptions with Java source, build descriptors,
SQL/PLSQL scripts and packages, migrations, and embedded queries. It distinguishes
native SQL from JPQL/HQL and ORM-only database access. It explicitly records when
no SQL is found, or when inspection is incomplete; absence of `.sql` files alone
does not establish absence of SQL. Database-access controls still receive review
when ORM is used without handwritten SQL.

The canonical [`developers-checklist.md`](developers-checklist.md) contains the
owner-supplied excerpt of USPS Java sections **8.1-8.15** and SQL sections
**9.1-9.3**, attributed to the
[Coding Secure Software Standards Procedure](https://blue.usps.gov/corptreasury/_pdf/paytech/coding-secure-software-standards-procedure.pdf).
It is not the full procedure or independently authenticated against the intranet
PDF. Keep it synchronized with the skill's bundled standards mapping.

Legacy Java guidance, invalid source examples, framework conflicts, and approved
exceptions are recorded separately rather than silently rewriting policy.
Parameter binding complements SQL controls but does not waive the compiled-
procedure requirement. Existing instructions and exception evidence are preserved
through managed sections; conflicting instructions require a decision.

The skill generates documentation only: it does not refactor application code,
execute database operations, modify sample repositories, or certify compliance.
There is no executable test runner for this documentation-only skill. Review
policy coverage, evidence, relative links, preserved content, and stable reruns
using the acceptance criteria in its
[workflow](.github/skills/agents-md/references/workflow.md).

### Core Instruction Files

#### `.github/copilot-instructions.md`
The master instruction file that Copilot reads for all operations. Includes:
- Zero-tolerance bug policy
- Research-first mandate
- Test-driven development requirements
- Manifest system
- Communication protocols

#### `.github/instructions/zero-tolerance.instructions.md`
Enforces absolute zero-tolerance for bugs:
- Bug severity classification (P0-P3)
- The bug loop protocol (fix until verified)
- Detection and validation methods
- Anti-patterns to avoid

#### `.github/instructions/testing.instructions.md`
Mandates comprehensive testing:
- 80% minimum coverage requirement
- Unit, integration, and E2E test standards
- Test quality guidelines (AAA pattern, independence)
- Mocking best practices
- CI/CD integration

#### `.github/instructions/research.instructions.md`
Requires research before implementation:
- When to search (always!)
- How to search effectively
- Source validation (official docs > blogs)
- The three-source rule
- Research documentation format

#### `.github/instructions/documentation.instructions.md`
Maintains comprehensive documentation:
- Manifest.md template and update requirements
- Component documentation standards
- Code comment guidelines
- Architecture Decision Records (ADRs)

### Supporting Files

#### `manifest.md`
Template for the critical manifest file that:
- Tracks project structure and components
- Documents dependencies and their purposes
- Records current status and known issues
- Provides setup instructions
- Maintains architecture decisions

#### `MCP-SETUP.md`
Step-by-step guide to configure Model Context Protocol servers:
- Official GitHub MCP server
- Playwright MCP for testing
- Web search integration
- Context7 for library documentation

## How It Works

### The Instruction Hierarchy

```
.github/copilot-instructions.md          # Global rules for all files
│
├── .github/instructions/*.instructions.md  # Specific guidelines
│   ├── zero-tolerance.instructions.md    # Bug handling
│   ├── testing.instructions.md             # Test requirements
│   ├── research.instructions.md            # Research mandate
│   └── documentation.instructions.md       # Docs standards
│
└── manifest.md                          # Project map
```

GitHub Copilot reads these files automatically and follows the instructions when:
- Generating code
- Answering questions
- Working in agent mode
- Creating pull requests

### The Loop Protocol

When Copilot encounters a bug:

```
Bug Detected → STOP → Categorize → Document → Analyze Root Cause
     ↑                                                      │
     │                                                      ↓
     │                                              Implement Fix
     │                                                      │
     │                                                      ↓
     │                                              Write Tests
     │                                                      │
     │                                                      ↓
     │                                              Run Test Suite
     │                                                      │
     │                                                      ↓
     │                                                   Pass?
     │                                                   /    \
     │                                                 No      Yes
     │                                                 /          \
     └─────────────────────────────────────────────────────┘            Done
```

**It cannot escape this loop until the bug is fixed and verified.**

## MCP Server Integration

### Why MCP Matters

Model Context Protocol (MCP) servers give Copilot access to:
- **Live web search** for current best practices
- **GitHub operations** for repo management
- **Browser automation** for E2E testing
- **Library documentation** from official sources

### Recommended MCP Servers (October 2025)

#### Essential
1. **GitHub MCP** - Official GitHub integration
   - Manage repos, issues, PRs
   - Search code across GitHub
   - Access organization data

2. **Web Search** - Current information retrieval
   - Research best practices
   - Find security advisories
   - Validate approaches

3. **Playwright MCP** - Official Microsoft browser automation
   - E2E testing
   - UI automation
   - Screenshot capture

#### Highly Recommended
4. **Context7/Upstash MCP** - Library documentation
   - Up-to-date official docs
   - Framework references
   - API documentation

5. **Microsoft Learn MCP** - Microsoft ecosystem docs
   - Azure documentation
   - .NET references
   - VS Code APIs

### Setup Guide

See [MCP-SETUP.md](./MCP-SETUP.md) for detailed installation and configuration.

Quick setup:

```bash
# Open VS Code settings
code --install-extension GitHub.copilot

# Configure MCP servers in settings.json
# See MCP-SETUP.md for full configuration
```

## Usage Examples

### Example 1: Bug Detection and Fix Loop

```typescript
// Copilot writes code
function processPayment(amount: number) {
  return amount * 1.1; // Add 10% fee
}

// Test fails: negative amounts not handled
// Copilot STOPS, enters bug loop

// Fixed version:
function processPayment(amount: number): number {
  if (amount < 0) {
    throw new Error('Amount cannot be negative');
  }
  if (amount === 0) {
    return 0; // No fee for zero amount
  }
  return amount * 1.1;
}

// Tests added:
test('processPayment handles negative amounts', () => {
  expect(() => processPayment(-10)).toThrow('Amount cannot be negative');
});

test('processPayment handles zero', () => {
  expect(processPayment(0)).toBe(0);
});

test('processPayment adds fee correctly', () => {
  expect(processPayment(100)).toBe(110);
});

// All tests pass ✓
// Copilot proceeds to next task
```

### Example 2: Research Before Implementation

```python
# User asks: "Implement password hashing"

# WITHOUT guardrails:
def hash_password(password):
    return hashlib.sha256(password.encode()).hexdigest()
# ❌ Wrong! SHA-256 is too fast, vulnerable to brute force

# WITH guardrails:
# Copilot searches: "password hashing best practices Python 2025"
# Finds: Use bcrypt or argon2, never plain SHA-256
# Source: OWASP Password Storage Cheat Sheet

import bcrypt

def hash_password(password: str) -> str:
    """
    Hash password using bcrypt with OWASP-recommended salt rounds.
    
    RESEARCH: "password hashing best practices 2025"
    SOURCE: https://owasp.org/www-community/Password_Storage_Cheat_Sheet
    REASONING: bcrypt is designed to be slow, resistant to brute force
    
    Args:
        password: Plain text password to hash
        
    Returns:
        Hashed password with salt
    """
    salt = bcrypt.gensalt(rounds=12)  # OWASP recommended
    return bcrypt.hashpw(password.encode('utf-8'), salt).decode('utf-8')

# Tests included:
def test_hash_password_produces_valid_hash():
    hashed = hash_password("test123")
    assert hashed.startswith('$2b$')
    assert len(hashed) == 60

def test_hash_password_produces_different_hashes():
    hash1 = hash_password("test123")
    hash2 = hash_password("test123")
    assert hash1 != hash2  # Different salts

def test_verify_password():
    password = "test123"
    hashed = hash_password(password)
    assert bcrypt.checkpw(password.encode('utf-8'), hashed.encode('utf-8'))
```

### Example 3: Automatic Documentation

```typescript
// Copilot creates a new service
// manifest.md is automatically updated:

// Added to Component Inventory:
/*
#### PaymentService
- **Location**: `src/services/payment-service.ts`
- **Purpose**: Handles payment processing via Stripe API
- **Dependencies**: stripe, logger, database
- **Tests**: `src/services/payment-service.test.ts`
- **Coverage**: 92%
- **Status**: ✅ Complete
*/

// Added to Dependencies:
/*
| stripe | ^15.0.0 | Payment processing | https://stripe.com/docs |
*/

// ADR created:
/*
docs/adr/0003-use-stripe-for-payments.md
- Why Stripe over PayPal
- Security considerations
- Cost analysis
- Integration complexity
*/
```

## Customization

### Language-Specific Instructions

Create additional instruction files for specific languages:

```bash
.github/instructions/
├── python.instructions.md      # Python-specific rules
├── typescript.instructions.md  # TypeScript-specific rules
├── react.instructions.md       # React-specific rules
└── security.instructions.md    # Security-specific rules
```

Example `python.instructions.md`:

```markdown
# Python-Specific Instructions

**Applies To**: `**/*.py`

## Style Guide
- Follow PEP 8
- Use Black for formatting
- Maximum line length: 100 characters
- Use type hints everywhere

## Testing
- Use pytest
- Test files: `test_*.py` or `*_test.py`
- Minimum coverage: 80%

## Dependencies
- Use Poetry for dependency management
- Pin exact versions in poetry.lock
- Regular security audits with pip-audit
```

### Project-Specific Overrides

You can override global rules for specific projects:

```markdown
# .github/copilot-instructions.md

# Custom rules for this project

## Overrides
- Minimum test coverage: 90% (higher than default 80%)
- All functions must have docstrings (not just public APIs)
- Commit messages must follow Conventional Commits
```

## Benefits

### For Solo Developers
✅ **Consistency** - Code quality doesn't vary based on your mood  
✅ **Learning** - Copilot researches and teaches you best practices  
✅ **Speed** - No debugging later because bugs are caught immediately  
✅ **Documentation** - Your future self thanks you  

### For Teams
✅ **Standards** - Everyone follows the same rules  
✅ **Onboarding** - New developers see examples of good practices  
✅ **Code Review** - Less time spent on basic issues  
✅ **Knowledge** - Research is documented and shared  

### For Enterprises
✅ **Security** - Vulnerabilities caught before merge  
✅ **Compliance** - Documentation requirements enforced  
✅ **Maintainability** - Codebases remain healthy over time  
✅ **Training** - AI enforces company standards automatically  

## FAQ

### Q: Will this slow down development?

**A**: Initially, maybe slightly. Long-term, it's much faster because:
- No debugging sessions later
- No refactoring poorly-designed code
- No security patches for vulnerabilities
- No documentation catch-up

### Q: Can I customize the rules?

**A**: Absolutely! Edit the instruction files to match your needs. The files are markdown and very readable.

### Q: Does this work with all GitHub Copilot features?

**A**: Yes! Works with:
- Copilot Chat
- Copilot Agent Mode
- Copilot Code Completions
- Copilot in CLI
- Copilot in IDE

### Q: What if Copilot ignores the instructions?

**A**: Rare, but can happen. Solutions:
1. Make instructions more explicit
2. Use stronger language ("MUST" vs "should")
3. Add examples
4. Report to Copilot team if persistent

### Q: Can I use this with other AI coding assistants?

**A**: The instruction format is specific to GitHub Copilot, but the principles apply to any AI assistant. You'd need to adapt the format.

### Q: How do I know it's working?

**A**: You'll notice:
- Copilot asks "Should I research best practices first?"
- Copilot mentions "I'll fix this bug before proceeding"
- Tests appear automatically with code
- Documentation gets updated

## Contributing

Contributions welcome! Please:

1. Fork this repository
2. Create a feature branch
3. Make your changes with tests
4. Update documentation
5. Submit a pull request

See [CONTRIBUTING.md](./CONTRIBUTING.md) for details.

## Roadmap

- [ ] Add language-specific instruction templates
- [ ] Create VS Code extension for easy setup
- [ ] Add pre-commit hooks for validation
- [ ] Build dashboard for compliance tracking
- [ ] Create tutorial videos
- [ ] Add more MCP server configurations

## License

MIT License - see [LICENSE](./LICENSE) for details.

## Acknowledgments

- GitHub Copilot team for the instruction file feature
- Model Context Protocol creators
- Open source community for best practices

## Support

- 🐛 [Report issues](https://github.com/dstorey87/copilot-guardrails/issues)
- 💡 [Request features](https://github.com/dstorey87/copilot-guardrails/discussions)
- 📚 [Read the docs](https://github.com/dstorey87/copilot-guardrails)
- ⭐ Star this repo if it helps you!

## Related Projects

- [GitHub Copilot Documentation](https://docs.github.com/copilot)
- [Model Context Protocol](https://modelcontextprotocol.io)
- [OWASP Guidelines](https://owasp.org)

---

**Made with ❤️ and enforced by AI**

*Transform your AI coding assistant from helpful to professional.*
