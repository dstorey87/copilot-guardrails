# Contributing to Copilot Guardrails

Thank you for your interest in contributing to the Copilot Guardrails project! This document provides guidelines for contributing.

## Code of Conduct

By participating in this project, you agree to maintain a respectful and inclusive environment for all contributors.

## How to Contribute

### Reporting Issues

If you find a bug or have a suggestion:

1. Check if the issue already exists in [Issues](https://github.com/dstorey87/copilot-guardrails/issues)
2. If not, create a new issue with:
   - Clear, descriptive title
   - Detailed description of the issue/suggestion
   - Steps to reproduce (for bugs)
   - Expected vs actual behavior
   - Your environment (VS Code version, Copilot version, OS)

### Submitting Changes

1. **Fork the Repository**
   ```bash
   git clone https://github.com/YOUR_USERNAME/copilot-guardrails.git
   cd copilot-guardrails
   ```

2. **Create a Branch**
   ```bash
   git checkout -b feature/your-feature-name
   # or
   git checkout -b fix/bug-description
   ```

3. **Make Your Changes**
   - Follow the existing file structure and formatting
   - Update documentation to reflect your changes
   - Test your changes with actual GitHub Copilot usage

4. **Commit Your Changes**
   ```bash
   git add .
   git commit -m "feat: add new instruction for X"
   # or
   git commit -m "fix: correct Y in Z instruction file"
   ```

   Use conventional commit messages:
   - `feat:` for new features
   - `fix:` for bug fixes
   - `docs:` for documentation changes
   - `refactor:` for code refactoring
   - `test:` for test changes

5. **Push and Create Pull Request**
   ```bash
   git push origin feature/your-feature-name
   ```
   Then create a PR on GitHub.

## Contribution Guidelines

### For Instruction Files

When modifying `.github/copilot-instructions.md` or `.github/instructions/*.instructions.md`:

- \u2705 **Be Explicit**: Use "MUST", "NEVER", "ALWAYS" for mandatory rules
- \u2705 **Be Specific**: Provide concrete examples, not vague descriptions
- \u2705 **Be Consistent**: Follow the existing tone and structure
- \u2705 **Be Tested**: Verify your changes work with Copilot
- \u2705 **Be Documented**: Add examples showing the instruction in action

### For Documentation

When modifying README.md, MCP-SETUP.md, or other docs:

- \u2705 Keep language clear and concise
- \u2705 Add code examples where helpful
- \u2705 Update table of contents if adding sections
- \u2705 Verify all links work
- \u2705 Use proper markdown formatting

### For Templates

When modifying templates (like manifest.md):

- \u2705 Keep placeholders clearly marked (e.g., `[Your Project Name]`)
- \u2705 Provide explanatory comments
- \u2705 Include realistic examples
- \u2705 Make optional sections clearly marked

## What We're Looking For

### High Priority

- \u2b50 Language-specific instruction templates (Python, TypeScript, Java, Go, etc.)
- \u2b50 Industry-specific patterns (web dev, data science, DevOps, etc.)
- \u2b50 Additional MCP server configurations
- \u2b50 Real-world usage examples
- \u2b50 Video tutorials or screencasts

### Medium Priority

- \ud83d\udd38 Improvements to existing instructions
- \ud83d\udd38 Better examples and explanations
- \ud83d\udd38 Translations to other languages
- \ud83d\udd38 Pre-commit hook templates
- \ud83d\udd38 CI/CD workflow examples

### Also Welcome

- Bug fixes
- Typo corrections
- Documentation improvements
- Feature suggestions

## Style Guide

### Markdown Formatting

```markdown
# Top Level Heading (only one per file)

## Second Level

### Third Level

**Bold for emphasis**
*Italic for subtle emphasis*
`code` for inline code
\u2705 for checkmarks (completed/good)
\u274c for X marks (incomplete/bad)
\u26a0\ufe0f for warnings
```

### Code Examples

Always include:
- Language identifier in code blocks
- Comments explaining key parts
- Both "good" and "bad" examples where relevant

```markdown
\u274c **Bad Example**:
\`\`\`typescript
// Don't do this
function foo() { }
\`\`\`

\u2705 **Good Example**:
\`\`\`typescript
// Do this instead
function processData(data: Data[]): Result {
  // Clear, documented, typed
}
\`\`\`
```

## Testing Your Changes

Before submitting a PR:

1. **Test with Copilot**
   - Install your changes in a test repository
   - Ask Copilot to perform tasks related to your changes
   - Verify Copilot follows the new instructions

2. **Check Markdown**
   - Ensure all markdown renders correctly
   - Verify links work
   - Check for typos

3. **Update Documentation**
   - Update manifest.md if you changed file structure
   - Update README.md if you added major features
   - Add examples to demonstrate your changes

## Pull Request Process

1. **PR Description**
   - Clearly describe what your PR does
   - Reference any related issues
   - Include before/after examples if applicable

2. **Review Process**
   - Maintainers will review your PR
   - Address any feedback or requested changes
   - Be patient - reviews may take a few days

3. **After Approval**
   - Your PR will be merged
   - You'll be credited in the release notes
   - Thank you for contributing!

## Questions?

If you have questions about contributing:

1. Check existing [Discussions](https://github.com/dstorey87/copilot-guardrails/discussions)
2. Create a new discussion
3. Tag it appropriately

## License

By contributing, you agree that your contributions will be licensed under the MIT License.

---

**Thank you for helping make Copilot a better development tool!**
