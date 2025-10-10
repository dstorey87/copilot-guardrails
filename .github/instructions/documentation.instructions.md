# Manifest and Documentation Requirements

**Applies To**: `**/*`

## The Manifest System

**EVERY REPOSITORY MUST HAVE A `manifest.md` FILE.**

This is not optional. This is how you maintain context across sessions and help humans understand your codebase.

## manifest.md Template

```markdown
# Project Manifest

> **Last Updated**: [ISO Date]
> **Version**: [Semantic Version]
> **Status**: [Development|Staging|Production]

## Project Overview

### Purpose
[One paragraph describing what this project does and why it exists]

### Key Features
- [Feature 1]
- [Feature 2]
- [Feature 3]

### Tech Stack
- **Language**: [Primary language and version]
- **Framework**: [Main framework and version]
- **Database**: [Database and version]
- **Key Dependencies**: [Critical libraries]

## Directory Structure

```
project-root/
├── .github/                     # GitHub configuration
│   ├── workflows/              # CI/CD pipelines
│   ├── copilot-instructions.md # Global Copilot guidelines
│   └── instructions/           # Specific instruction files
├── src/                        # Source code
│   ├── components/             # [Description]
│   ├── services/               # [Description]
│   └── utils/                  # [Description]
├── tests/                      # Test files
│   ├── unit/                   # Unit tests
│   ├── integration/            # Integration tests
│   └── e2e/                    # End-to-end tests
├── docs/                       # Documentation
├── config/                     # Configuration files
├── manifest.md                 # This file
├── package.json                # Dependencies (if Node.js)
├── requirements.txt            # Dependencies (if Python)
└── README.md                   # Public-facing docs
```

## Component Inventory

### Core Components

#### [Component Name]
- **Location**: `path/to/component`
- **Purpose**: [What it does]
- **Dependencies**: [What it depends on]
- **Tests**: `path/to/tests`
- **Coverage**: [X%]
- **Status**: [✅ Complete | 🚧 In Progress | ⚠️ Issues]

#### [Component Name 2]
- **Location**: `path/to/component2`
- **Purpose**: [What it does]
- **Dependencies**: [What it depends on]
- **Tests**: `path/to/tests`
- **Coverage**: [X%]
- **Status**: [✅ Complete | 🚧 In Progress | ⚠️ Issues]

### Services

#### [Service Name]
- **Location**: `path/to/service`
- **Purpose**: [What it does]
- **External Dependencies**: [APIs, databases, etc.]
- **Configuration**: `path/to/config`
- **Status**: [✅ Complete | 🚧 In Progress | ⚠️ Issues]

## Dependencies

### Production Dependencies

| Package | Version | Purpose | Documentation |
|---------|---------|---------|---------------|
| [name] | [version] | [why we use it] | [link] |
| [name] | [version] | [why we use it] | [link] |

### Development Dependencies

| Package | Version | Purpose | Documentation |
|---------|---------|---------|---------------|
| [name] | [version] | [why we use it] | [link] |
| [name] | [version] | [why we use it] | [link] |

## Setup Instructions

### Prerequisites
- [Prerequisite 1 with version]
- [Prerequisite 2 with version]

### Installation

```bash
# Step 1: Clone repository
git clone [repo-url]
cd [repo-name]

# Step 2: Install dependencies
[install command]

# Step 3: Configure environment
cp .env.example .env
# Edit .env with your values

# Step 4: Initialize database (if applicable)
[db setup commands]

# Step 5: Run tests
[test command]

# Step 6: Start development server
[start command]
```

### Environment Variables

| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `VAR_NAME` | Yes/No | value | [what it does] |
| `VAR_NAME` | Yes/No | value | [what it does] |

## Development Workflow

### Running Tests

```bash
# Unit tests
[unit test command]

# Integration tests
[integration test command]

# E2E tests
[e2e test command]

# Coverage report
[coverage command]
```

### Building

```bash
# Development build
[dev build command]

# Production build
[prod build command]
```

### Deployment

```bash
# Deploy to staging
[staging deploy command]

# Deploy to production
[production deploy command]
```

## Current Status

### Completed Features
- ✅ [Feature 1] - [Date completed]
- ✅ [Feature 2] - [Date completed]

### In Progress
- 🚧 [Feature 3] - [Current status/blocker]
- 🚧 [Feature 4] - [Current status/blocker]

### Planned
- 📅 [Feature 5] - [Target date]
- 📅 [Feature 6] - [Target date]

## Known Issues

### Critical
- ❌ **[Issue Description]**
  - **Impact**: [What it affects]
  - **Workaround**: [Temporary solution]
  - **Status**: [Being investigated/In progress/Blocked]

### Non-Critical
- ⚠️ **[Issue Description]**
  - **Impact**: [What it affects]
  - **Priority**: [Low/Medium/High]

## Performance Metrics

| Metric | Target | Current | Status |
|--------|--------|---------|--------|
| Test Coverage | 80% | [X%] | [✅/❌] |
| Build Time | < 60s | [Xs] | [✅/❌] |
| Bundle Size | < 500KB | [XKB] | [✅/❌] |

## Security

### Security Measures
- [Measure 1: e.g., "Input validation on all endpoints"]
- [Measure 2: e.g., "Rate limiting configured"]
- [Measure 3: e.g., "Secrets in environment variables"]

### Security Audits
- **Last Audit**: [Date]
- **Findings**: [Number of issues]
- **Status**: [All resolved/X remaining]

### Dependency Vulnerabilities
- **Last Check**: [Date]
- **High/Critical**: [Number]
- **Medium/Low**: [Number]

## Architecture Decisions

See `docs/adr/` for detailed Architecture Decision Records.

### Key Decisions
1. **[Decision Title]** - [Brief summary] - [Date]
2. **[Decision Title]** - [Brief summary] - [Date]

## Recent Changes

### [Date] - [Version]
- [Change description]
- [Change description]

### [Date] - [Version]
- [Change description]
- [Change description]

## Contributing

See `CONTRIBUTING.md` for detailed contribution guidelines.

### Quick Start for Contributors
1. Fork repository
2. Create feature branch
3. Make changes with tests
4. Ensure all tests pass
5. Update documentation
6. Submit pull request

## Resources

### Internal Documentation
- [Doc 1](path/to/doc)
- [Doc 2](path/to/doc)

### External Resources
- [Resource 1](URL)
- [Resource 2](URL)

## Contacts

- **Project Lead**: [Name] - [Contact]
- **Tech Lead**: [Name] - [Contact]
- **DevOps**: [Name] - [Contact]

---

**Next Review**: [Date]  
**Maintained By**: GitHub Copilot + [Team Name]
```

## Update Requirements

### When to Update manifest.md

✅ **MUST Update**:
- Added new component/service
- Changed directory structure
- Added/removed dependency
- Changed tech stack
- Identified new issue
- Resolved existing issue
- Completed feature
- Changed deployment process
- Updated environment variables

⚠️ **Should Update**:
- Performance metrics changed significantly
- Documentation links changed
- Team contacts changed

### Update Frequency

- **Minimum**: Weekly
- **Recommended**: After each significant change
- **Mandatory**: Before each release

## Component Documentation Requirements

### For Each Major Component

Create `README.md` in component directory:

```markdown
# [Component Name]

## Purpose
[What this component does]

## API

### Functions/Methods

#### `functionName(param1, param2)`
- **Description**: [What it does]
- **Parameters**:
  - `param1` (type): [Description]
  - `param2` (type): [Description]
- **Returns**: [Return type and description]
- **Throws**: [Errors it might throw]
- **Example**:
  ```typescript
  const result = functionName('value1', 'value2');
  ```

## Usage Examples

```typescript
// Example 1: Basic usage
import { Component } from './component';

const instance = new Component();
instance.doSomething();

// Example 2: Advanced usage
const result = instance.complexOperation({
  option1: true,
  option2: 'value'
});
```

## Configuration

[How to configure this component]

## Testing

```bash
# Run component tests
npm test -- components/ComponentName
```

## Dependencies

- [Dependency 1]: [Why needed]
- [Dependency 2]: [Why needed]

## Known Issues

- [Issue 1]
- [Issue 2]

## Future Enhancements

- [Enhancement 1]
- [Enhancement 2]
```

## README.md Requirements

Every repository must have a `README.md` that serves as public-facing documentation:

```markdown
# [Project Name]

[Project description - what it does and why it exists]

## Features

- ✨ [Feature 1]
- ✨ [Feature 2]
- ✨ [Feature 3]

## Quick Start

```bash
# Install
[install command]

# Run
[run command]
```

## Documentation

Full documentation available at [docs/](./docs/) or [link to hosted docs].

## Installation

### Prerequisites
- [Requirement 1]
- [Requirement 2]

### Steps

```bash
# Step 1
[command]

# Step 2
[command]
```

## Usage

### Basic Example

```typescript
// Code example
```

### Advanced Example

```typescript
// More complex example
```

## API Reference

See [API.md](./docs/API.md) for detailed API documentation.

## Contributing

Contributions welcome! Please read [CONTRIBUTING.md](./CONTRIBUTING.md) first.

## Testing

```bash
# Run tests
[test command]

# Run with coverage
[coverage command]
```

## License

[License type] - See [LICENSE](./LICENSE) for details.

## Support

- 🐛 [Report bugs](issues-link)
- 💡 [Request features](discussions-link)
- 📚 [Read docs](docs-link)

## Acknowledgments

- [Credit 1]
- [Credit 2]
```

## Code Documentation Standards

### Function/Method Documentation

```typescript
/**
 * Calculate the total price including tax and discounts.
 * 
 * This function applies discounts first, then calculates tax on the
 * discounted amount. This matches the business requirement that tax
 * should not be applied to discounted portions.
 * 
 * @param items - Array of cart items with price and quantity
 * @param taxRate - Tax rate as decimal (e.g., 0.1 for 10%)
 * @param discountCode - Optional discount code to apply
 * @returns Total price including tax, rounded to 2 decimal places
 * 
 * @throws {Error} If taxRate is negative or > 1
 * @throws {Error} If any item has negative price or quantity
 * 
 * @example
 * ```typescript
 * const items = [
 *   { price: 10.00, quantity: 2 },
 *   { price: 5.00, quantity: 1 }
 * ];
 * const total = calculateTotal(items, 0.1, 'SAVE10');
 * console.log(total); // 24.75
 * ```
 * 
 * @see {@link applyDiscount} for discount calculation logic
 * @see {@link calculateTax} for tax calculation logic
 */
export function calculateTotal(
  items: CartItem[],
  taxRate: number,
  discountCode?: string
): number {
  // Implementation
}
```

```python
def calculate_total(items: list[CartItem], tax_rate: float, discount_code: str | None = None) -> float:
    """
    Calculate the total price including tax and discounts.
    
    This function applies discounts first, then calculates tax on the
    discounted amount. This matches the business requirement that tax
    should not be applied to discounted portions.
    
    Args:
        items: Array of cart items with price and quantity
        tax_rate: Tax rate as decimal (e.g., 0.1 for 10%)
        discount_code: Optional discount code to apply
    
    Returns:
        Total price including tax, rounded to 2 decimal places
    
    Raises:
        ValueError: If taxRate is negative or > 1
        ValueError: If any item has negative price or quantity
    
    Example:
        >>> items = [
        ...     CartItem(price=10.00, quantity=2),
        ...     CartItem(price=5.00, quantity=1)
        ... ]
        >>> calculate_total(items, 0.1, 'SAVE10')
        24.75
    
    See Also:
        apply_discount: Discount calculation logic
        calculate_tax: Tax calculation logic
    """
    # Implementation
    pass
```

### Complex Logic Documentation

```typescript
// ALGORITHM: Boyer-Moore string search
// REFERENCE: https://en.wikipedia.org/wiki/Boyer%E2%80%93Moore_string-search_algorithm
// WHY: O(n/m) average case, faster than naive O(n*m)
// RESEARCHED: "fast string search algorithm JavaScript 2025"
function boyerMooreSearch(text: string, pattern: string): number {
  // 1. Build bad character table
  const badChar = buildBadCharTable(pattern);
  
  // 2. Search with skip optimization
  let shift = 0;
  while (shift <= text.length - pattern.length) {
    // ... implementation
  }
  
  return -1;
}
```

## Architecture Documentation

### Create ADR (Architecture Decision Record) for Significant Decisions

Location: `docs/adr/NNNN-decision-title.md`

```markdown
# ADR NNNN: [Decision Title]

## Status

[Proposed | Accepted | Deprecated | Superseded by ADR-XXXX]

## Context

[Describe the problem or opportunity]

## Decision Drivers

* [Driver 1]
* [Driver 2]
* [Driver 3]

## Considered Options

* [Option 1]
* [Option 2]
* [Option 3]

## Decision Outcome

Chosen option: "[Option X]", because [justification].

### Positive Consequences

* [Benefit 1]
* [Benefit 2]

### Negative Consequences

* [Tradeoff 1]
* [Tradeoff 2]

## Pros and Cons of the Options

### [Option 1]

* Good, because [argument a]
* Good, because [argument b]
* Bad, because [argument c]

### [Option 2]

* Good, because [argument a]
* Bad, because [argument b]

## Links

* [Link to related decision]
* [Link to external resource]
```

## Documentation Maintenance

### Review Schedule

- **Weekly**: Update manifest.md with changes
- **Monthly**: Review all README files for accuracy
- **Quarterly**: Review ADRs for relevance
- **Before Release**: Complete documentation audit

### Documentation Checklist

Before marking work complete:

- [ ] `manifest.md` updated
- [ ] Component README updated (if applicable)
- [ ] API documentation updated
- [ ] Code comments added for complex logic
- [ ] Examples provided
- [ ] Known issues documented
- [ ] ADR created (if architectural change)
- [ ] Dependencies documented

## Remember

> Code is temporary. Documentation is forever.

Well-documented code:
- ✅ Can be maintained by anyone
- ✅ Preserves context across time
- ✅ Prevents duplicate work
- ✅ Enables effective collaboration
- ✅ Reduces cognitive load

**Your future self (and every other developer) will thank you.**

---

**Update Frequency**: After every significant change  
**Minimum Standard**: All public APIs documented  
**Best Practice**: Document why, not just what
