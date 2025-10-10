# Zero-Tolerance Bug Policy

**Applies To**: `**/*`

## The Iron Rule

**NO CODE SHIPS WITH KNOWN BUGS. PERIOD.**

This is not negotiable. This is not flexible. This is the foundation of professional software development.

## What Counts as a Bug

### Severity Levels

#### Critical (P0) - IMMEDIATE HALT
- System crashes or hangs
- Data corruption or loss
- Security vulnerabilities
- Complete feature failure

**Action**: Drop everything. Fix immediately. No exceptions.

#### High (P1) - MUST FIX BEFORE NEXT COMMIT
- Feature partially works
- Error messages are unclear
- Performance degradation
- Failing tests
- Type errors
- Linter failures

**Action**: Fix before proceeding with any new work.

#### Medium (P2) - MUST FIX BEFORE PR
- UI/UX issues
- Missing edge case handling
- Incomplete documentation
- Code style violations
- Missing tests

**Action**: Include fix in current work iteration.

#### Low (P3) - TRACK BUT CAN DEFER
- Minor UI polish
- Optimization opportunities
- Nice-to-have features

**Action**: Create an issue, but can be addressed later.

## The Bug Loop Protocol

```
┌─────────────────────────────────────┐
│  Bug Detected                       │
└───────────┬─────────────────────────┘
            ↓
┌─────────────────────────────────────┐
│  STOP ALL OTHER WORK                │
└───────────┬─────────────────────────┘
            ↓
┌─────────────────────────────────────┐
│  Categorize Bug (P0/P1/P2/P3)       │
└───────────┬─────────────────────────┘
            ↓
┌─────────────────────────────────────┐
│  Document Bug                        │
│  - What went wrong                   │
│  - Expected vs actual behavior       │
│  - Steps to reproduce                │
└───────────┬─────────────────────────┘
            ↓
┌─────────────────────────────────────┐
│  Root Cause Analysis                │
│  - Why did this happen?              │
│  - What assumptions were wrong?      │
│  - What was overlooked?              │
└───────────┬─────────────────────────┘
            ↓
┌─────────────────────────────────────┐
│  Implement Fix                       │
│  - Address root cause                │
│  - Don't just patch symptoms         │
└───────────┬─────────────────────────┘
            ↓
┌─────────────────────────────────────┐
│  Write/Update Tests                  │
│  - Test the bug scenario             │
│  - Test the fix                      │
│  - Test regressions                  │
└───────────┬─────────────────────────┘
            ↓
┌─────────────────────────────────────┐
│  Run Full Test Suite                │
└───────────┬─────────────────────────┘
            ↓
        ┌───┴───┐
        │ Pass? │
        └───┬───┘
            │
     No ────┼──── Yes
     │      │      │
     │      ↓      ↓
     │  ┌──────┐  ┌──────────────────────┐
     │  │ Loop │  │ Verify Fix Complete  │
     │  │ Back │  └──────────┬───────────┘
     │  └──────┘             ↓
     │                   ┌──────┐
     └───────────────────│ Done │
                         └──────┘
```

## Detection Methods

### Automated Detection

1. **Test Failures**
   ```bash
   # All tests must pass
   npm test
   pytest
   ```

2. **Type Checking**
   ```bash
   # TypeScript
   tsc --noEmit
   
   # Python
   mypy .
   ```

3. **Linting**
   ```bash
   # JavaScript/TypeScript
   eslint .
   
   # Python
   ruff check .
   ```

4. **Security Scanning**
   ```bash
   npm audit
   safety check
   ```

### Manual Detection

- Code review findings
- User reports
- Integration testing
- Edge case analysis

## Fix Validation

### Required Evidence

Before declaring a bug fixed:

1. ✅ **Test Coverage**
   - Bug scenario is covered by test
   - Test fails without fix
   - Test passes with fix

2. ✅ **No Regressions**
   - All existing tests still pass
   - No new warnings or errors
   - Performance not degraded

3. ✅ **Root Cause Addressed**
   - Not just a symptom patch
   - Underlying issue resolved
   - Similar bugs prevented

4. ✅ **Documentation Updated**
   - Change log entry
   - Comments explain the fix
   - Known issues list updated

## Communication Protocol

### When Reporting a Bug

```markdown
## Bug Report

**Severity**: [P0/P1/P2/P3]
**Component**: [affected module/file]
**Detected**: [how was it found]

### Description
[Clear description of what went wrong]

### Expected Behavior
[What should happen]

### Actual Behavior
[What actually happened]

### Steps to Reproduce
1. [First step]
2. [Second step]
3. [etc.]

### Root Cause
[Analysis of why this happened]

### Proposed Fix
[How you plan to fix it]
```

### When Reporting a Fix

```markdown
## Bug Fix Complete

**Bug ID**: [reference to bug report]
**Fix Commit**: [commit hash]

### Changes Made
- [File/module changed]
- [What was changed]

### Tests Added
- [Test file]
- [Test scenarios covered]

### Validation
- [x] All tests pass
- [x] No regressions
- [x] Root cause addressed
- [x] Documentation updated

### Risk Assessment
**Low** | **Medium** | **High**

[Explanation of potential impacts]
```

## Anti-Patterns to Avoid

### ❌ The "I'll Fix It Later" Trap

```javascript
// TODO: This sometimes fails, fix later
function processData(data) {
  // bug-prone code
}
```

**WHY IT'S BAD**: "Later" never comes. Fix it NOW.

### ❌ The "Works on My Machine"

```python
# It works when I test it manually...
def feature():
    pass  # but has no automated tests
```

**WHY IT'S BAD**: Manual testing is not reproducible. Write tests.

### ❌ The "Quick Patch"

```typescript
// Quick fix to make it work
if (data === undefined) return;  // band-aid
```

**WHY IT'S BAD**: Treats symptoms, not causes. Find why `data` is undefined.

### ❌ The "Silent Failure"

```python
try:
    risky_operation()
except Exception:
    pass  # ignore errors
```

**WHY IT'S BAD**: Bugs must be visible. Log, report, fix.

## Enforcement Mechanisms

### Pre-Commit Hooks

```bash
#!/bin/bash
# .git/hooks/pre-commit

# Run tests
npm test || exit 1

# Run linter
npm run lint || exit 1

# Type check
npx tsc --noEmit || exit 1
```

### CI/CD Pipeline

```yaml
# .github/workflows/ci.yml
name: CI
on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Run tests
        run: npm test
      - name: Check coverage
        run: npm run test:coverage
        # Fail if coverage < 80%
```

### Code Review Checklist

- [ ] No known bugs
- [ ] All tests pass
- [ ] No linter errors
- [ ] No type errors
- [ ] No security warnings
- [ ] Code review approved

## Metrics to Track

### Bug Metrics

- **Bugs Found**: Total bugs detected
- **Bugs Fixed**: Bugs resolved
- **Time to Fix**: Average fix time by severity
- **Bug Escape Rate**: Bugs found in production
- **Reopened Bugs**: Fixes that didn't work

### Quality Metrics

- **Test Coverage**: Should be ≥ 80%
- **Code Quality Score**: From linters
- **Technical Debt**: Time to fix all P2/P3 bugs

## Success Criteria

A successful implementation means:

✅ **Zero P0/P1 bugs in main branch**  
✅ **All tests passing at all times**  
✅ **No compiler/linter errors**  
✅ **Test coverage ≥ 80%**  
✅ **All bugs documented and tracked**  
✅ **Fast feedback loops (bugs found early)**

## Remember

> Quality is not an act, it is a habit. - Aristotle

Every bug you ignore makes the next bug easier to ignore. Every bug you fix makes the codebase stronger.

**Be ruthless with bugs. Your users will thank you.**

---

**Enforcement Level**: ABSOLUTE ZERO TOLERANCE  
**No Exceptions**: Not for deadlines, not for demos, not for "quick fixes"  
**This Is Non-Negotiable**: Professional developers don't ship bugs
