# Project Manifest

> **Last Updated**: 2025-10-10  
> **Version**: 1.0.0  
> **Status**: Production

## Project Overview

### Purpose

The Copilot Guardrails System is a comprehensive set of instruction files and best practices that transform GitHub Copilot from a helpful code assistant into a professional, zero-tolerance, research-driven AI developer. It enforces strict development standards including mandatory bug fixes, comprehensive testing, security validation, and automatic documentation.

### Key Features

- ✅ **Zero-Tolerance Bug Policy** - Forces Copilot to fix bugs before proceeding
- ✅ **Research-First Mandate** - Requires searching for best practices before implementing
- ✅ **Test-Driven Development** - Enforces 80%+ test coverage on all code
- ✅ **Automatic Documentation** - Maintains manifest and documentation files
- ✅ **Security Validation** - Checks for vulnerabilities before shipping
- ✅ **Context Management** - Suggests repository splits when complexity grows
- ✅ **MCP Integration** - Leverages Model Context Protocol for enhanced capabilities

### Tech Stack

- **Format**: Markdown instruction files
- **Compatible With**: GitHub Copilot (VS Code, CLI, GitHub.com)
- **MCP Servers**: GitHub, Playwright, Web Search, Context7, Microsoft Learn
- **Standards**: October 2025 best practices

## Directory Structure

```
copilot-guardrails/
├── .github/
│   ├── copilot-instructions.md          # Main instruction file
│   └── instructions/
│       ├── zero-tolerance.instructions.md   # Bug handling rules
│       ├── testing.instructions.md          # Test requirements
│       ├── research.instructions.md         # Research mandate
│       └── documentation.instructions.md    # Documentation standards
├── README.md                            # Public documentation
├── MCP-SETUP.md                         # MCP configuration guide
├── manifest.md                          # This file - project map
├── LICENSE                              # MIT License
└── CONTRIBUTING.md                      # Contribution guidelines (planned)
```

## Component Inventory

### Core Instruction Files

#### copilot-instructions.md
- **Location**: `.github/copilot-instructions.md`
- **Purpose**: Master instruction file that Copilot reads for all operations
- **Key Sections**: 
  - Core principles and zero-tolerance rule
  - Workflow protocols (research, testing, loop, incremental development)
  - Code quality standards
  - Manifest system requirements
  - Communication protocols
  - Validation checklists
- **Status**: ✅ Complete
- **Coverage**: N/A (documentation)

#### zero-tolerance.instructions.md
- **Location**: `.github/instructions/zero-tolerance.instructions.md`
- **Purpose**: Enforces absolute zero-tolerance for bugs with loop protocol
- **Key Sections**:
  - Bug severity levels (P0-P3)
  - The bug loop flowchart
  - Detection and validation methods
  - Communication protocols for bugs
  - Anti-patterns to avoid
- **Status**: ✅ Complete
- **Coverage**: N/A (documentation)

#### testing.instructions.md
- **Location**: `.github/instructions/testing.instructions.md`
- **Purpose**: Mandates comprehensive testing with 80% minimum coverage
- **Key Sections**:
  - Coverage requirements by component type
  - Test types (unit, integration, E2E)
  - Test quality standards (AAA pattern, independence)
  - Mocking best practices
  - CI/CD integration
  - Testing anti-patterns
- **Status**: ✅ Complete
- **Coverage**: N/A (documentation)

#### research.instructions.md
- **Location**: `.github/instructions/research.instructions.md`
- **Purpose**: Requires research before ANY implementation
- **Key Sections**:
  - When to research (always!)
  - Effective search query patterns
  - The three-source validation rule
  - Research documentation format
  - MCP server usage for research
  - Anti-patterns (assuming, using outdated info, copying without understanding)
- **Status**: ✅ Complete
- **Coverage**: N/A (documentation)

#### documentation.instructions.md
- **Location**: `.github/instructions/documentation.instructions.md`
- **Purpose**: Maintains comprehensive documentation including manifest.md
- **Key Sections**:
  - Manifest.md template and requirements
  - Component documentation standards
  - README requirements
  - Code documentation (JSDoc/docstrings)
  - Architecture Decision Records (ADRs)
  - Documentation update schedule
- **Status**: ✅ Complete
- **Coverage**: N/A (documentation)

### Supporting Documentation

#### README.md
- **Location**: `README.md`
- **Purpose**: Public-facing documentation explaining the guardrails system
- **Key Sections**:
  - What the system is and why it exists
  - Quick start guides (existing repo vs new project)
  - File inventory and descriptions
  - How the instruction hierarchy works
  - Usage examples
  - Customization options
  - FAQ
- **Status**: ✅ Complete
- **Coverage**: N/A (documentation)

#### MCP-SETUP.md
- **Location**: `MCP-SETUP.md`
- **Purpose**: Complete guide to configuring MCP servers for GitHub Copilot
- **Key Sections**:
  - What MCP is and why it matters
  - Prerequisites and requirements
  - Essential MCP servers (GitHub, Web Search, Playwright, Context7, Microsoft Learn)
  - Installation and configuration for each server
  - Complete configuration example
  - Verification and troubleshooting
  - Security best practices
  - Enterprise configuration
- **Status**: ✅ Complete
- **Coverage**: N/A (documentation)

#### manifest.md
- **Location**: `manifest.md`
- **Purpose**: This file - provides complete project map and current status
- **Status**: ✅ Complete and maintained
- **Coverage**: N/A (documentation)

## Dependencies

### Production Dependencies

| Package | Version | Purpose | Documentation |
|---------|---------|---------|---------------|
| GitHub Copilot | Latest | AI code assistant | [Docs](https://docs.github.com/copilot) |
| VS Code | 1.85+ | IDE with MCP support | [Docs](https://code.visualstudio.com) |

### Optional MCP Servers

| Package | Version | Purpose | Documentation |
|---------|---------|---------|---------------|
| @modelcontextprotocol/server-github | Latest | GitHub integration | [GitHub](https://github.com/modelcontextprotocol/servers) |
| @microsoft/playwright-mcp | Latest | Browser automation | [VS Code MCP](https://code.visualstudio.com/mcp) |
| @upstash/context7-mcp | Latest | Library documentation | [Upstash](https://upstash.com/context7) |
| @microsoftdocs/mcp | Latest | Microsoft docs | [Microsoft Learn](https://learn.microsoft.com) |

## Setup Instructions

### Prerequisites

- GitHub Copilot subscription (Individual, Business, or Enterprise)
- VS Code version 1.85 or later
- Node.js 18+ (for MCP servers)
- Git

### Installation for Existing Repository

```bash
# 1. Navigate to your repository
cd your-project

# 2. Create .github directory structure
mkdir -p .github/instructions

# 3. Download guardrails files
curl -o .github/copilot-instructions.md \
  https://raw.githubusercontent.com/dstorey87/copilot-guardrails/main/.github/copilot-instructions.md

curl -o .github/instructions/zero-tolerance.instructions.md \
  https://raw.githubusercontent.com/dstorey87/copilot-guardrails/main/.github/instructions/zero-tolerance.instructions.md

curl -o .github/instructions/testing.instructions.md \
  https://raw.githubusercontent.com/dstorey87/copilot-guardrails/main/.github/instructions/testing.instructions.md

curl -o .github/instructions/research.instructions.md \
  https://raw.githubusercontent.com/dstorey87/copilot-guardrails/main/.github/instructions/research.instructions.md

curl -o .github/instructions/documentation.instructions.md \
  https://raw.githubusercontent.com/dstorey87/copilot-guardrails/main/.github/instructions/documentation.instructions.md

# 4. Create manifest
touch manifest.md

# 5. Configure MCP servers (see MCP-SETUP.md)
```

### Installation as Template for New Project

```bash
# 1. Clone as template
git clone https://github.com/dstorey87/copilot-guardrails.git my-project
cd my-project

# 2. Remove git history
rm -rf .git
git init

# 3. Customize files
# Edit manifest.md, README.md for your project

# 4. Start development with guardrails active
```

### Environment Variables

| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `GITHUB_TOKEN` | Yes (for GitHub MCP) | - | GitHub Personal Access Token for MCP server |

## Development Workflow

### Using Guardrails

1. **Open VS Code** in project with guardrails installed
2. **Use Copilot Chat** (Ctrl+Alt+I / Cmd+Alt+I)
3. **Copilot automatically reads** `.github/copilot-instructions.md` and `.github/instructions/*.instructions.md`
4. **Request features**: Copilot will:
   - Research best practices first
   - Implement with tests
   - Fix bugs before proceeding
   - Update documentation automatically

### Verification

Verify guardrails are active by asking Copilot:

```
@workspace What are your testing requirements?
```

Expected response should mention "80% minimum coverage" and "zero-tolerance for bugs".

## Current Status

### Completed Features

- ✅ Core instruction file system - 2025-10-10
- ✅ Zero-tolerance bug policy - 2025-10-10
- ✅ Testing requirements and standards - 2025-10-10
- ✅ Research-first mandate - 2025-10-10
- ✅ Documentation requirements - 2025-10-10
- ✅ README with examples and FAQ - 2025-10-10
- ✅ MCP setup guide - 2025-10-10
- ✅ Manifest template and this file - 2025-10-10

### In Progress

- 🚧 CONTRIBUTING.md - Planned
- 🚧 Language-specific instruction templates - Planned
- 🚧 VS Code extension for easy setup - Planned

### Planned

- 📅 Video tutorials - Target: Q4 2025
- 📅 Pre-commit hooks for validation - Target: Q4 2025
- 📅 Compliance dashboard - Target: Q1 2026
- 📅 More MCP server configurations - Ongoing

## Known Issues

### None Currently

No known issues at this time.

## Performance Metrics

Not applicable - this is a documentation/configuration project.

## Security

### Security Measures

- ✅ No code execution - purely instruction files
- ✅ No secrets stored - uses environment variables
- ✅ Open source and auditable
- ✅ MIT licensed

### Security Best Practices

- MCP tokens should be stored in environment variables, never committed
- Review MCP server source code before using
- Use minimal GitHub token scopes
- Rotate tokens regularly

## Architecture Decisions

No formal ADRs yet as this is a documentation project.

### Key Design Decisions

1. **Markdown Format** - Universal, version-controllable, human-readable
2. **Modular Instructions** - Separate files for different concerns
3. **Applies To Pattern** - Each instruction specifies file patterns it applies to
4. **Template-Based** - Provides reusable templates for manifests, docs, etc.
5. **MCP Integration** - Leverages newest Copilot capabilities

## Recent Changes

### 2025-10-10 - v1.0.0

- Initial release
- Created all core instruction files
- Added comprehensive README
- Added MCP setup guide
- Created manifest template
- Added MIT license

## Contributing

See CONTRIBUTING.md (coming soon) for contribution guidelines.

### Quick Start for Contributors

1. Fork repository
2. Create feature branch
3. Make changes
4. Test with actual Copilot usage
5. Update documentation
6. Submit pull request

## Resources

### Internal Documentation

- [README](./README.md) - Main documentation
- [MCP Setup Guide](./MCP-SETUP.md) - MCP configuration
- [Copilot Instructions](./.github/copilot-instructions.md) - What Copilot sees

### External Resources

- [GitHub Copilot Documentation](https://docs.github.com/copilot)
- [Model Context Protocol](https://modelcontextprotocol.io)
- [VS Code MCP Guide](https://code.visualstudio.com/docs/copilot/mcp-servers)
- [OWASP Guidelines](https://owasp.org)

## Contacts

- **Project Lead**: dstorey87
- **Repository**: https://github.com/dstorey87/copilot-guardrails
- **Issues**: https://github.com/dstorey87/copilot-guardrails/issues
- **Discussions**: https://github.com/dstorey87/copilot-guardrails/discussions

---

**Next Review**: 2025-10-17 (weekly)  
**Maintained By**: GitHub Copilot + dstorey87  
**Status**: Production Ready ✓
