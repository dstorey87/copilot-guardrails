# Research and Best Practices Instructions

**Applies To**: `**/*`

## The Research-First Mandate

**NEVER IMPLEMENT WITHOUT RESEARCH. PERIOD.**

Your knowledge cutoff means you may not have the latest information. The web does. Use it.

## When to Research

### ALWAYS Research Before:

1. **Implementing a New Feature**
   - "What's the best way to implement [feature] in [language/framework]?"
   - "[Framework] [feature] best practices October 2025"
   - "Common pitfalls when implementing [feature]"

2. **Choosing a Library/Framework**
   - "Best [type] library for [use case] 2025"
   - "[Library A] vs [Library B] comparison"
   - "Is [library] still maintained October 2025"

3. **Solving a Problem**
   - "How to [problem] in [technology] 2025"
   - "[Error message] solution"
   - "[Technology] security best practices"

4. **Architecture Decisions**
   - "[Pattern] architecture pros and cons"
   - "When to use [approach] vs [alternative]"
   - "Scalability considerations for [system]"

5. **Security Implementation**
   - "[Technology] security vulnerabilities 2025"
   - "How to securely [action]"
   - "OWASP [topic] guidelines"

## Search Query Patterns

### Effective Search Queries

```plaintext
✅ GOOD:
- "TypeScript async error handling best practices 2025"
- "React Server Components security considerations October 2025"
- "PostgreSQL connection pooling node.js best practices"
- "GitHub Actions workflow optimization 2025"

❌ BAD:
- "typescript async" (too vague)
- "how to code" (too broad)
- "best practices" (no context)
- "error" (useless)
```

### Query Template

```
[Technology] [Specific Topic] [best practices|security|performance|tutorial] [October 2025|2025]
```

## Research Protocol

### Step 1: Identify Knowledge Gaps

```markdown
## Before Implementation Checklist

- [ ] Do I know the current best practice?
- [ ] Do I know the security implications?
- [ ] Do I know common pitfalls?
- [ ] Do I know performance considerations?
- [ ] Is there a newer/better approach?
```

### Step 2: Conduct Research

```typescript
// WRONG: Implement based on assumptions
function implementFeature() {
  // I think this is how it works...
}

// RIGHT: Research first, then implement
/*
 * RESEARCH CONDUCTED:
 * 1. Searched: "Node.js worker threads best practices 2025"
 * 2. Found: Official Node.js docs recommend using worker_threads for CPU-intensive tasks
 * 3. Security: Validated input before passing to worker
 * 4. Performance: Use pool of workers, not one-per-task
 * 
 * IMPLEMENTATION BASED ON:
 * - https://nodejs.org/api/worker_threads.html
 * - https://blog.logrocket.com/node-js-worker-threads-tutorial/
 */
function implementFeature() {
  // Implementation based on research
}
```

### Step 3: Validate Findings

Check multiple sources:

1. **Official Documentation** (highest authority)
2. **Reputable Tech Blogs** (Vercel, LogRocket, etc.)
3. **GitHub Discussions/Issues** (real-world experiences)
4. **Stack Overflow** (with recent dates)
5. **Security Advisories** (CVE databases)

⚠️ **Red Flags**:
- Article from 2020 or earlier (likely outdated)
- No code examples
- Contradicts official docs
- No mention of security
- Too good to be true

## Research Documentation

### In Code Comments

```python
"""
Calculate user subscription tier based on usage.

RESEARCH NOTES:
- Researched: "SaaS pricing tier calculation best practices"
- Sources:
  * https://stripe.com/docs/billing/subscriptions/usage-based
  * https://www.priceintelligently.com/blog/saas-pricing-models
  
DECISIONS:
- Using usage-based with tiered pricing
- Calculating at end of billing cycle (not real-time)
- Grace period for tier changes (as recommended by Stripe)

SECURITY:
- Validated against gaming/manipulation
- Logging all tier changes for audit
"""
def calculate_subscription_tier(user_id: str, usage: dict) -> str:
    # Implementation
    pass
```

### In ADRs (Architecture Decision Records)

```markdown
# ADR 001: Use PostgreSQL for Main Database

## Status
Accepted

## Context
Need to choose database for user data, transactions, and relationships.

## Research Conducted

### Searches Performed
1. "PostgreSQL vs MySQL 2025 comparison"
2. "Best relational database for SaaS October 2025"
3. "PostgreSQL JSON performance 2025"

### Key Findings
- PostgreSQL has better JSON support (JSONB)
- Superior handling of concurrent writes
- Better full-text search capabilities
- Stronger consistency guarantees
- Active development community

### Sources
- [PostgreSQL Docs](https://www.postgresql.org/docs/)
- [AWS Database Blog](https://aws.amazon.com/blogs/database/)
- [Hacker News Discussion](https://news.ycombinator.com/item?id=xxxxx)

## Decision
Use PostgreSQL 16+ for all relational data needs.

## Consequences

### Positive
- JSONB for flexible schemas
- Strong ACID guarantees
- Excellent tooling ecosystem

### Negative
- Slightly more complex setup than MySQL
- Requires understanding of advanced features

## Validation
- Performance tested with 1M records: ✅
- Security review completed: ✅
- Team has PostgreSQL experience: ✅
```

## Specific Research Areas

### Security Research

**ALWAYS search for security implications:**

```plaintext
Before implementing authentication:
➡️ Search: "[auth method] security vulnerabilities 2025"
➡️ Search: "OWASP authentication best practices"
➡️ Search: "[framework] auth security checklist"

Before handling user input:
➡️ Search: "[framework] input validation best practices"
➡️ Search: "SQL injection prevention [language] 2025"
➡️ Search: "XSS prevention [framework]"

Before using a library:
➡️ Search: "[library] security vulnerabilities"
➡️ Search: "[library] CVE" 
➡️ Check: npm audit / pip-audit results
```

### Performance Research

```plaintext
Before implementing data processing:
➡️ Search: "[operation] performance optimization [language]"
➡️ Search: "[framework] performance best practices 2025"
➡️ Search: "[algorithm] time complexity"

Before choosing architecture:
➡️ Search: "[pattern] scalability considerations"
➡️ Search: "[service] rate limits and quotas"
➡️ Search: "[technology] benchmark comparison"
```

### Framework/Library Research

```plaintext
Before adopting a dependency:
➡️ Search: "is [library] still maintained 2025"
➡️ Search: "[library] alternatives comparison"
➡️ Search: "[library] breaking changes recent"
➡️ Check: GitHub stars, issues, last commit
➡️ Check: npm/pypi download trends
```

## MCP Server Usage for Research

### Use Web Search MCP

```typescript
// Before implementing, search for best practices
const research = await mcpWebSearch(
  "Next.js 15 app router data fetching best practices October 2025"
);

// Review findings
console.log('Research findings:', research);

// Then implement based on research
function implementDataFetching() {
  // Implementation follows researched best practices
}
```

### Use Context7 MCP for Library Docs

```typescript
// Get up-to-date library documentation
const docs = await mcpContext7(
  'react',
  'server components'
);

// Use official docs as implementation guide
import { ServerComponent } from 'react';

// Implement according to official docs
export default function MyServerComponent() {
  // Following official documentation
}
```

### Use GitHub MCP for Real Examples

```typescript
// Search for real-world implementations
const examples = await mcpGitHub.searchCode(
  'language:typescript useEffect cleanup pattern'
);

// Learn from production code
// Then implement your version
```

## Research Quality Criteria

### High-Quality Sources

✅ **Tier 1: Official Documentation**
- Language/framework official docs
- Official GitHub repositories
- Official blog posts
- RFCs and specifications

✅ **Tier 2: Reputable Tech Companies**
- Vercel, Netlify (for web)
- AWS, Google Cloud, Azure (for cloud)
- Auth0, Okta (for auth)
- Stripe (for payments)

✅ **Tier 3: Established Tech Blogs**
- LogRocket
- CSS-Tricks
- Smashing Magazine
- Dev.to (from known authors)

⚠️ **Use With Caution**
- Medium articles (verify author)
- Personal blogs (cross-reference)
- Stack Overflow (check votes and date)
- Reddit (good for discussions, not sole source)

❌ **Avoid**
- Content farms
- AI-generated articles (without verification)
- Outdated tutorials (pre-2024)
- Anonymous sources

## Research Validation Process

### The Three-Source Rule

Before implementing anything significant:

1. **Find THREE independent sources**
2. **All three should agree on the approach**
3. **At least one should be official documentation**

If sources contradict:
- Research deeper
- Understand why they differ
- Choose based on:
  - Most recent information
  - Most authoritative source
  - Best security/performance profile

### Code Example Validation

```markdown
## Before Using Code From Web

- [ ] Code is from a reputable source
- [ ] Code is recent (2024-2025)
- [ ] Code includes error handling
- [ ] Code follows security best practices
- [ ] Code has no obvious bugs
- [ ] Code fits your use case
- [ ] You understand what the code does
- [ ] You can explain why it works
```

## Integration with Development Workflow

### Phase 1: Planning
```
1. Receive requirement
2. RESEARCH similar implementations
3. RESEARCH best practices
4. RESEARCH security considerations
5. Document findings
6. Propose approach
```

### Phase 2: Implementation
```
1. Review research notes
2. Follow researched patterns
3. Reference documentation links in comments
4. Implement with confidence
```

### Phase 3: Validation
```
1. Test against researched edge cases
2. Verify security measures
3. Check performance expectations
4. Validate against best practices
```

## Common Research Scenarios

### Scenario 1: New API Integration

```markdown
## Research Checklist

- [ ] Official API documentation reviewed
- [ ] Authentication method researched
- [ ] Rate limits identified
- [ ] Error handling patterns found
- [ ] Security best practices reviewed
- [ ] SDK availability checked
- [ ] Code examples studied
- [ ] Common issues researched (GitHub issues)
```

### Scenario 2: Performance Optimization

```markdown
## Research Checklist

- [ ] Profiling techniques researched
- [ ] Common bottlenecks identified
- [ ] Optimization strategies reviewed
- [ ] Benchmarking methods found
- [ ] Trade-offs understood
- [ ] Real-world examples studied
```

### Scenario 3: Security Implementation

```markdown
## Research Checklist

- [ ] OWASP guidelines reviewed
- [ ] CVE database checked
- [ ] Security advisories read
- [ ] Attack vectors identified
- [ ] Mitigation strategies researched
- [ ] Security testing methods found
- [ ] Compliance requirements verified
```

## Anti-Patterns

### ❌ Assuming You Know Best

```typescript
// WRONG
function hashPassword(password: string) {
  // I think SHA-256 is good enough
  return crypto.createHash('sha256').update(password).digest('hex');
}

// RIGHT: Research first
/*
 * RESEARCHED: "password hashing best practices 2025"
 * FINDING: Use bcrypt or argon2, never plain SHA-256
 * REASON: SHA-256 is too fast, vulnerable to brute force
 * SOURCE: https://owasp.org/www-community/Password_Storage_Cheat_Sheet
 */
import bcrypt from 'bcrypt';

function hashPassword(password: string) {
  const saltRounds = 10; // OWASP recommended
  return bcrypt.hash(password, saltRounds);
}
```

### ❌ Using Outdated Information

```python
# WRONG: Using old approach without checking
def fetch_data():
    # This is how I did it in 2020...
    response = urllib.request.urlopen(url)
    return response.read()

# RIGHT: Research current best practice
"""
RESEARCHED: "Python HTTP requests best practices 2025"
FINDING: Use httpx for modern async/await support
SOURCE: https://www.python-httpx.org/
"""
import httpx

async def fetch_data():
    async with httpx.AsyncClient() as client:
        response = await client.get(url)
        response.raise_for_status()
        return response.json()
```

### ❌ Copying Code Without Understanding

```javascript
// WRONG: Copy-paste without understanding
// Copied from Stack Overflow
function debounce(func, wait) {
  let timeout;
  return function executedFunction(...args) {
    const later = () => {
      clearTimeout(timeout);
      func(...args);
    };
    clearTimeout(timeout);
    timeout = setTimeout(later, wait);
  };
}
// ^^^ Has bugs, but you wouldn't know because you didn't understand it

// RIGHT: Understand, then implement
/**
 * RESEARCHED: "JavaScript debounce implementation explained"
 * UNDERSTOOD: 
 * - Debounce delays function execution
 * - Resets timer on each call
 * - Only executes after quiet period
 * 
 * SOURCES:
 * - https://davidwalsh.name/javascript-debounce-function
 * - https://lodash.com/docs/#debounce
 * 
 * IMPLEMENTATION NOTES:
 * - Using lodash.debounce (battle-tested)
 * - Configured with leading/trailing options
 * - Added TypeScript types for safety
 */
import { debounce } from 'lodash';

const debouncedSearch = debounce(
  (query: string) => searchAPI(query),
  300,
  { leading: false, trailing: true }
);
```

## Documentation Requirements

### Research Log Format

```markdown
# Research Log: [Feature/Problem]

**Date**: 2025-10-10
**Researcher**: GitHub Copilot
**Context**: [Why this research was needed]

## Questions
1. [Primary question]
2. [Secondary question]
3. [Security question]

## Searches Conducted
1. "[Search query 1]" - [Key finding]
2. "[Search query 2]" - [Key finding]
3. "[Search query 3]" - [Key finding]

## Key Findings

### Best Practices
- [Finding 1]
- [Finding 2]

### Security Considerations
- [Consideration 1]
- [Consideration 2]

### Performance Notes
- [Note 1]
- [Note 2]

## Sources
1. [Title](URL) - Official docs
2. [Title](URL) - Blog post
3. [Title](URL) - GitHub discussion

## Decision
[What approach was chosen and why]

## Implementation Notes
[How the research influenced the implementation]
```

## Remember

> The only thing worse than not knowing is not knowing that you don't know.

**Research isn't optional. It's professional responsibility.**

- ✅ Research before implementing
- ✅ Verify from multiple sources
- ✅ Document your findings
- ✅ Update when standards change
- ✅ Share knowledge with team

**You are only as good as the information you act on. Make it current. Make it correct.**

---

**Enforcement Level**: MANDATORY  
**Search First**: Before every significant implementation  
**This Prevents**: Outdated code, security vulnerabilities, reinventing wheels
