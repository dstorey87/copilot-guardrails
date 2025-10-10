# Testing Standards and Requirements

**Applies To**: `**/*`

## The Testing Mandate

**ALL CODE MUST BE TESTED. NO EXCEPTIONS.**

If you write it, you test it. If it's not tested, it's not done.

### Playwright E2E Testing (MANDATORY)

**FOR ALL FRONTEND AND BACKEND CHANGES:**

1. **EVERY feature addition requires Playwright E2E tests** - No exceptions
2. **Services must be verified as running** before tests execute
3. **ALL functionality must be tested** - Partial testing = incomplete work
4. **Nothing is considered tested without Playwright E2E coverage**

**Use Playwright MCP Tools:**
- `mcp_playwright_playwright_navigate` - Navigate to URLs
- `mcp_playwright_playwright_click` - Click elements
- `mcp_playwright_playwright_fill` - Fill form fields
- `mcp_playwright_playwright_screenshot` - Capture test evidence
- `mcp_playwright_playwright_get_visible_text` - Verify content
- `mcp_playwright_playwright_console_logs` - Check for errors
- `mcp_playwright_start_codegen_session` - Generate test code
- `mcp_playwright_end_codegen_session` - Save generated tests

**Before ANY frontend/backend code is considered complete:**
- [ ] Playwright E2E tests written for ALL new functionality
- [ ] All services verified as running (health checks)
- [ ] Complete user workflows tested end-to-end
- [ ] Screenshots captured for visual verification
- [ ] Console logs checked for errors
- [ ] Tests pass in headless and headed modes

## Test Coverage Requirements

### Minimum Coverage Levels

- **Unit Tests**: 80% minimum coverage
- **Integration Tests**: All critical paths
- **E2E Tests**: All user-facing workflows

### Coverage by Component Type

#### Business Logic: 90%+
```typescript
// These MUST be heavily tested
export function calculateTotal(items: Item[]): number {
  // Business critical - needs comprehensive tests
}
```

#### UI Components: 80%+
```typescript
// Test rendering, interactions, edge cases
export function ProductCard({ product }: Props) {
  // User-facing - needs thorough testing
}
```

#### Utilities: 95%+
```typescript
// Pure functions should be easy to test
export function formatCurrency(amount: number): string {
  // Utility - should be near 100% coverage
}
```

#### Infrastructure: 70%+
```typescript
// Config, setup, etc.
export function initializeApp() {
  // Harder to test, but still required
}
```

## Test Types

### 1. Unit Tests

**Purpose**: Test individual functions/methods in isolation

```typescript
// Example: Jest/Vitest
import { describe, it, expect } from 'vitest';
import { calculateDiscount } from './pricing';

describe('calculateDiscount', () => {
  it('calculates 10% discount correctly', () => {
    expect(calculateDiscount(100, 10)).toBe(90);
  });

  it('handles zero discount', () => {
    expect(calculateDiscount(100, 0)).toBe(100);
  });

  it('handles 100% discount', () => {
    expect(calculateDiscount(100, 100)).toBe(0);
  });

  it('throws on negative prices', () => {
    expect(() => calculateDiscount(-100, 10)).toThrow();
  });

  it('throws on invalid discount percentage', () => {
    expect(() => calculateDiscount(100, 150)).toThrow();
  });
});
```

```python
# Example: pytest
import pytest
from pricing import calculate_discount

def test_calculate_discount_basic():
    assert calculate_discount(100, 10) == 90

def test_calculate_discount_zero():
    assert calculate_discount(100, 0) == 100

def test_calculate_discount_full():
    assert calculate_discount(100, 100) == 0

def test_calculate_discount_negative_price():
    with pytest.raises(ValueError):
        calculate_discount(-100, 10)

def test_calculate_discount_invalid_percentage():
    with pytest.raises(ValueError):
        calculate_discount(100, 150)
```

### 2. Integration Tests

**Purpose**: Test multiple components working together

```typescript
// Example: Testing service layer with database
import { describe, it, expect, beforeEach } from 'vitest';
import { UserService } from './user-service';
import { TestDatabase } from '../test-utils/database';

describe('UserService Integration', () => {
  let service: UserService;
  let db: TestDatabase;

  beforeEach(async () => {
    db = await TestDatabase.create();
    service = new UserService(db);
  });

  it('creates user and retrieves by id', async () => {
    const user = await service.createUser({
      name: 'John Doe',
      email: 'john@example.com'
    });

    const retrieved = await service.getUserById(user.id);
    expect(retrieved).toEqual(user);
  });

  it('prevents duplicate emails', async () => {
    await service.createUser({
      name: 'John Doe',
      email: 'john@example.com'
    });

    await expect(service.createUser({
      name: 'Jane Doe',
      email: 'john@example.com'
    })).rejects.toThrow('Email already exists');
  });
});
```

### 3. End-to-End Tests (MANDATORY WITH PLAYWRIGHT MCP)

**Purpose**: Test complete user workflows using Playwright MCP

**CRITICAL**: Use Playwright MCP tools for ALL E2E testing. Traditional Playwright test files are supplementary.

```typescript
// Example: Using Playwright MCP Tools
// Step 1: Navigate to application
await mcp_playwright_playwright_navigate({
  url: 'http://localhost:3000/products/123',
  browserType: 'chromium',
  headless: false
});

// Step 2: Verify service is running
const pageText = await mcp_playwright_playwright_get_visible_text();
if (pageText.includes('Error') || pageText.includes('Cannot connect')) {
  throw new Error('Service is not running - tests cannot proceed');
}

// Step 3: Test user workflow
await mcp_playwright_playwright_click({ selector: 'button:text("Add to Cart")' });
await mcp_playwright_playwright_screenshot({ name: 'cart-added', savePng: true });

await mcp_playwright_playwright_click({ selector: 'a:text("Checkout")' });
await mcp_playwright_playwright_fill({ selector: '#name', value: 'John Doe' });
await mcp_playwright_playwright_fill({ selector: '#address', value: '123 Main St' });

await mcp_playwright_playwright_screenshot({ name: 'checkout-form', savePng: true });
await mcp_playwright_playwright_click({ selector: 'button:text("Place Order")' });

// Step 4: Verify results
const confirmationText = await mcp_playwright_playwright_get_visible_text();
if (!confirmationText.includes('Order confirmed')) {
  throw new Error('Order confirmation not displayed');
}

// Step 5: Check for console errors
const logs = await mcp_playwright_playwright_console_logs({ type: 'error' });
if (logs.length > 0) {
  throw new Error(`Console errors detected: ${logs}`);
}

await mcp_playwright_playwright_screenshot({ name: 'order-complete', savePng: true });
await mcp_playwright_playwright_close();
```

**Traditional Playwright Test (Supplementary)**:

```typescript
// Example: Playwright Test Framework (use alongside MCP)
import { test, expect } from '@playwright/test';

test('user can complete purchase', async ({ page }) => {
  // Navigate to product page
  await page.goto('/products/123');
  
  // Add to cart
  await page.click('button:text("Add to Cart")');
  await expect(page.locator('.cart-count')).toHaveText('1');
  
  // Proceed to checkout
  await page.click('a:text("Checkout")');
  
  // Fill shipping info
  await page.fill('#name', 'John Doe');
  await page.fill('#address', '123 Main St');
  
  // Complete purchase
  await page.click('button:text("Place Order")');
  
  // Verify confirmation
  await expect(page.locator('.order-confirmation')).toBeVisible();
  expect(await page.locator('.order-number').textContent()).toMatch(/^ORD-/);
});
```

## Test Organization

### File Structure

```
src/
├── components/
│   ├── Button.tsx
│   └── Button.test.tsx          # Co-located with component
├── services/
│   ├── user-service.ts
│   └── user-service.test.ts     # Co-located with service
└── utils/
    ├── formatting.ts
    └── formatting.test.ts       # Co-located with utility

tests/
├── integration/                 # Integration tests
│   ├── auth.test.ts
│   └── checkout.test.ts
└── e2e/                         # End-to-end tests
    ├── user-flows.spec.ts
    └── admin-flows.spec.ts
```

### Naming Conventions

#### Test Files
- Unit: `*.test.ts` or `*.spec.ts`
- Integration: `*.integration.test.ts`
- E2E: `*.e2e.test.ts` or `*.spec.ts`

#### Test Cases
```typescript
// Good: Descriptive and specific
it('throws error when email is invalid', () => {});
it('returns empty array when no results found', () => {});
it('calls onSubmit with form data when valid', () => {});

// Bad: Vague or unclear
it('works', () => {});
it('test email', () => {});
it('handles data', () => {});
```

## Test Quality Standards

### The AAA Pattern (Arrange-Act-Assert)

```typescript
it('calculates total price with tax', () => {
  // Arrange
  const items = [
    { price: 10, quantity: 2 },
    { price: 5, quantity: 1 }
  ];
  const taxRate = 0.1;

  // Act
  const total = calculateTotal(items, taxRate);

  // Assert
  expect(total).toBe(27.5); // (10*2 + 5*1) * 1.1
});
```

### Test Independence

```typescript
// Good: Each test is independent
describe('UserService', () => {
  let service: UserService;

  beforeEach(() => {
    service = new UserService();
  });

  it('creates user', async () => {
    const user = await service.create({ name: 'John' });
    expect(user.name).toBe('John');
  });

  it('deletes user', async () => {
    const user = await service.create({ name: 'Jane' });
    await service.delete(user.id);
    expect(await service.findById(user.id)).toBeNull();
  });
});

// Bad: Tests depend on each other
describe('UserService', () => {
  let userId: string;

  it('creates user', async () => {
    const user = await service.create({ name: 'John' });
    userId = user.id; // Side effect
  });

  it('deletes user', async () => {
    await service.delete(userId); // Depends on previous test
  });
});
```

### Edge Cases and Error Handling

```typescript
describe('parseDate', () => {
  // Happy path
  it('parses valid date string', () => {
    expect(parseDate('2025-10-10')).toEqual(new Date(2025, 9, 10));
  });

  // Edge cases
  it('handles leap year', () => {
    expect(parseDate('2024-02-29')).toEqual(new Date(2024, 1, 29));
  });

  it('handles end of year', () => {
    expect(parseDate('2025-12-31')).toEqual(new Date(2025, 11, 31));
  });

  // Error cases
  it('throws on invalid format', () => {
    expect(() => parseDate('not-a-date')).toThrow('Invalid date format');
  });

  it('throws on invalid date', () => {
    expect(() => parseDate('2025-02-30')).toThrow('Invalid date');
  });

  // Boundary conditions
  it('handles null input', () => {
    expect(() => parseDate(null as any)).toThrow();
  });

  it('handles empty string', () => {
    expect(() => parseDate('')).toThrow();
  });
});
```

## Mocking and Test Doubles

### When to Mock

✅ **Mock These**:
- External APIs
- Database calls (in unit tests)
- File system operations
- Time/Date functions
- Random number generators
- Third-party services

❌ **Don't Mock These**:
- Simple utility functions
- Pure functions
- Your own business logic
- Trivial dependencies

### Mocking Examples

```typescript
// Mock external API
import { vi } from 'vitest';
import { fetchUserData } from './api';

vi.mock('./api', () => ({
  fetchUserData: vi.fn()
}));

it('handles API error', async () => {
  vi.mocked(fetchUserData).mockRejectedValue(
    new Error('Network error')
  );

  await expect(loadUser('123')).rejects.toThrow('Failed to load user');
});
```

```python
# Mock external service
from unittest.mock import Mock, patch
import pytest
from user_service import UserService

@patch('user_service.email_service')
def test_sends_welcome_email(mock_email):
    service = UserService()
    user = service.create_user('john@example.com')
    
    mock_email.send.assert_called_once_with(
        to='john@example.com',
        subject='Welcome!'
    )
```

## Test Data Management

### Fixtures and Factories

```typescript
// test-utils/fixtures.ts
export const createUser = (overrides = {}) => ({
  id: '123',
  name: 'John Doe',
  email: 'john@example.com',
  role: 'user',
  ...overrides
});

export const createProduct = (overrides = {}) => ({
  id: '456',
  name: 'Test Product',
  price: 99.99,
  stock: 10,
  ...overrides
});

// Usage in tests
import { createUser, createProduct } from '../test-utils/fixtures';

it('applies discount to premium users', () => {
  const user = createUser({ role: 'premium' });
  const product = createProduct({ price: 100 });
  
  expect(calculatePrice(user, product)).toBe(90);
});
```

```python
# tests/fixtures.py
import pytest
from models import User, Product

@pytest.fixture
def user():
    return User(
        id='123',
        name='John Doe',
        email='john@example.com',
        role='user'
    )

@pytest.fixture
def premium_user():
    return User(
        id='124',
        name='Jane Doe',
        email='jane@example.com',
        role='premium'
    )

# Usage
def test_discount(premium_user):
    price = calculate_price(premium_user, product=100)
    assert price == 90
```

## Performance Testing

```typescript
import { test, expect } from 'vitest';

test('processes large dataset efficiently', () => {
  const largeDataset = Array.from({ length: 10000 }, (_, i) => ({
    id: i,
    value: Math.random()
  }));

  const start = performance.now();
  const result = processData(largeDataset);
  const duration = performance.now() - start;

  expect(duration).toBeLessThan(100); // Must complete in < 100ms
  expect(result.length).toBe(10000);
});
```

## Snapshot Testing

```typescript
// For UI components
import { render } from '@testing-library/react';
import { Button } from './Button';

it('renders correctly', () => {
  const { container } = render(
    <Button variant="primary">Click me</Button>
  );
  
  expect(container.firstChild).toMatchSnapshot();
});

// For data structures
it('generates correct report', () => {
  const report = generateMonthlyReport({
    year: 2025,
    month: 10
  });
  
  expect(report).toMatchSnapshot();
});
```

## Test Configuration

### TypeScript/JavaScript (Vitest)

```typescript
// vitest.config.ts
import { defineConfig } from 'vitest/config';

export default defineConfig({
  test: {
    globals: true,
    environment: 'jsdom',
    coverage: {
      provider: 'v8',
      reporter: ['text', 'json', 'html'],
      exclude: [
        'node_modules/',
        'tests/',
        '**/*.test.ts',
        '**/*.spec.ts'
      ],
      thresholds: {
        lines: 80,
        functions: 80,
        branches: 80,
        statements: 80
      }
    }
  }
});
```

### Python (pytest)

```ini
# pytest.ini
[pytest]
testpaths = tests
python_files = test_*.py *_test.py
python_classes = Test*
python_functions = test_*
addopts = 
    --cov=src
    --cov-report=html
    --cov-report=term
    --cov-fail-under=80
    --strict-markers
    --verbose
```

## Continuous Integration

```yaml
# .github/workflows/test.yml
name: Tests

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    
    steps:
      - uses: actions/checkout@v4
      
      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'
          cache: 'npm'
      
      - name: Install dependencies
        run: npm ci
      
      - name: Run unit tests
        run: npm test
      
      - name: Run integration tests
        run: npm run test:integration
      
      - name: Check coverage
        run: npm run test:coverage
      
      - name: Upload coverage
        uses: codecov/codecov-action@v4
        with:
          file: ./coverage/coverage-final.json
```

## Testing Checklist

Before marking code as complete:

- [ ] All new code has unit tests
- [ ] Coverage meets minimum threshold (80%)
- [ ] Edge cases are tested
- [ ] Error cases are tested
- [ ] Integration points are tested
- [ ] **Playwright MCP E2E tests written for ALL new features**
- [ ] **All services verified as running before E2E tests**
- [ ] **Complete user workflows tested with Playwright MCP**
- [ ] **Screenshots captured at key steps for verification**
- [ ] **Console logs checked for errors**
- [ ] E2E tests cover user workflows
- [ ] All tests pass locally
- [ ] All tests pass in CI
- [ ] No flaky tests
- [ ] Tests are fast (< 5 seconds for unit tests)
- [ ] Mocks are appropriate and minimal
- [ ] Test data is clear and realistic

## Common Anti-Patterns

### ❌ Testing Implementation Details

```typescript
// Bad
it('calls helper function', () => {
  const spy = vi.spyOn(component, 'helperMethod');
  component.doSomething();
  expect(spy).toHaveBeenCalled();
});

// Good
it('produces correct output', () => {
  const result = component.doSomething();
  expect(result).toBe(expectedValue);
});
```

### ❌ Brittle Tests

```typescript
// Bad: Breaks if implementation changes
expect(element.className).toBe('btn btn-primary');

// Good: Tests behavior, not implementation
expect(element).toHaveClass('btn-primary');
```

### ❌ Incomplete Coverage

```typescript
// Bad: Only happy path
it('creates user', () => {
  expect(createUser({ name: 'John' })).toBeDefined();
});

// Good: Happy path + error cases
describe('createUser', () => {
  it('creates user with valid data', () => {});
  it('throws on missing name', () => {});
  it('throws on invalid email', () => {});
  it('throws on duplicate email', () => {});
});
```

## Remember

> Tests are the specification of your code. They define what it does and doesn't do.

Good tests:
- ✅ Are fast
- ✅ Are isolated
- ✅ Are repeatable
- ✅ Are thorough
- ✅ Are maintainable

**If you can't test it, you can't trust it.**

---

**Minimum Coverage**: 80%  
**No Excuses**: "Hard to test" means "poorly designed"  
**Test First**: Write tests before or alongside code, never after
