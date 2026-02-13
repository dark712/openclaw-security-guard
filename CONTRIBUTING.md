# Contributing to OpenClaw Security Guard

First off, thank you for considering contributing! 🎉

This document provides guidelines for contributing to OpenClaw Security Guard.

---

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [Development Setup](#development-setup)
- [Project Structure](#project-structure)
- [How to Contribute](#how-to-contribute)
- [Coding Standards](#coding-standards)
- [Security Guidelines](#security-guidelines)
- [Testing](#testing)
- [Pull Request Process](#pull-request-process)
- [Release Process](#release-process)

---

## Code of Conduct

This project follows the [Contributor Covenant](https://www.contributor-covenant.org/version/2/1/code_of_conduct/). By participating, you agree to uphold this code.

**In short:** Be respectful, inclusive, and professional.

---

## Getting Started

### Prerequisites

- Node.js 22 or higher
- npm 10 or higher
- Git

### Fork and Clone

```bash
# Fork the repo on GitHub, then:
git clone https://github.com/YOUR_USERNAME/openclaw-security-guard.git
cd openclaw-security-guard

# Add upstream remote
git remote add upstream https://github.com/2pidata/openclaw-security-guard.git
```

---

## Development Setup

```bash
# Install dependencies
npm install

# Run tests to verify setup
npm test

# Run in development mode (auto-reload)
npm run dev

# Run linting
npm run lint

# Run specific scanner for testing
node src/cli/index.js scan secrets
```

### IDE Setup

**VS Code** (recommended):

```json
// .vscode/settings.json
{
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "eslint.validate": ["javascript"]
}
```

**Recommended extensions:**
- ESLint
- Prettier
- GitLens

---

## Project Structure

```
openclaw-security-guard/
├── src/
│   ├── cli/
│   │   └── index.js          # CLI entry point & commands
│   ├── dashboard/
│   │   └── server.js         # Web dashboard server
│   ├── scanners/
│   │   ├── secrets-scanner.js
│   │   ├── config-auditor.js
│   │   ├── prompt-injection-detector.js
│   │   ├── dependency-scanner.js
│   │   └── mcp-server-auditor.js
│   ├── hardening/
│   │   └── auto-hardener.js  # Auto-fix functionality
│   ├── monitors/
│   │   ├── realtime-monitor.js
│   │   └── cost-monitor.js
│   ├── utils/
│   │   ├── helpers.js        # Utility functions
│   │   ├── i18n.js           # Internationalization
│   │   └── validation.js     # Input validation
│   └── index.js              # Main exports
├── tests/
│   ├── unit/                 # Unit tests
│   ├── integration/          # Integration tests
│   └── e2e/                  # End-to-end tests
├── docs/
│   ├── en/                   # English docs
│   ├── fr/                   # French docs
│   └── ar/                   # Arabic docs
└── examples/                 # Example configurations
```

---

## How to Contribute

### 🐛 Reporting Bugs

1. Check [existing issues](https://github.com/2pidata/openclaw-security-guard/issues)
2. Create a new issue with:
   - Clear title
   - Steps to reproduce
   - Expected vs actual behavior
   - Environment (OS, Node version)
   - Relevant logs/screenshots

### 💡 Suggesting Features

1. Check [existing feature requests](https://github.com/2pidata/openclaw-security-guard/issues?q=is%3Aissue+label%3Aenhancement)
2. Create a new issue with:
   - Clear description of the feature
   - Use case / why it's needed
   - Proposed implementation (optional)

### 📝 Improving Documentation

- Fix typos, clarify explanations
- Add examples
- Translate to other languages

### 🔧 Submitting Code

See [Pull Request Process](#pull-request-process) below.

---

## Coding Standards

### JavaScript Style

We use ESLint and Prettier. Key rules:

```javascript
// ✅ Good
const myFunction = async (param) => {
  if (!param) {
    throw new Error('Parameter required');
  }
  return await doSomething(param);
};

// ❌ Bad
function myFunction(param) {
  if(!param) throw new Error('Parameter required')
  return doSomething(param)
}
```

### Naming Conventions

| Type | Convention | Example |
|------|------------|---------|
| Files | kebab-case | `secrets-scanner.js` |
| Classes | PascalCase | `SecretsScanner` |
| Functions | camelCase | `scanForSecrets` |
| Constants | UPPER_SNAKE | `MAX_FILE_SIZE` |
| Variables | camelCase | `fileContent` |

### File Structure

```javascript
/**
 * 🛡️ Module Name
 * 
 * Description of what this module does.
 * 
 * @author Miloud Belarebia
 */

// 1. Imports (external first, then internal)
import fs from 'fs';
import path from 'path';
import { helper } from '../utils/helpers.js';

// 2. Constants
const DEFAULT_CONFIG = {};

// 3. Classes/Functions
export class MyClass {
  constructor(config) {
    this.config = config;
  }
  
  async myMethod() {
    // Implementation
  }
}

// 4. Default export (if applicable)
export default MyClass;
```

### Comments

```javascript
// ✅ Good - explains WHY
// Skip binary files to avoid false positives in entropy calculation
if (isBinaryFile(filePath)) continue;

// ❌ Bad - explains WHAT (obvious from code)
// Loop through files
for (const file of files) {
```

---

## Security Guidelines

**CRITICAL:** This is a security tool. Code must be secure.

### Must Follow

- [ ] **No `eval()` or `Function()`** - Never execute dynamic code
- [ ] **No shell injection** - Always parameterize commands
- [ ] **Validate all inputs** - Use Zod schemas
- [ ] **Sanitize paths** - Prevent directory traversal
- [ ] **Escape outputs** - Prevent XSS in HTML reports
- [ ] **No secrets in code** - Use environment variables
- [ ] **Minimal dependencies** - Each dep is an attack surface

### Security Review Checklist

Before submitting:

```bash
# Check for security issues
npm run audit:deps
npm run test:security

# Verify no secrets in code
git diff --cached | grep -i "password\|secret\|key\|token"
```

### Forbidden Patterns

```javascript
// ❌ NEVER DO THIS
eval(userInput);
new Function(userInput);
child_process.exec(userInput);
fs.readFile(userInput);  // Without validation
require(userInput);

// ✅ DO THIS INSTEAD
// Use parameterized functions
// Validate and sanitize inputs
// Use allowlists, not blocklists
```

---

## Testing

### Running Tests

```bash
# All tests
npm test

# Watch mode
npm run test:watch

# With coverage
npm run test:coverage

# Specific suite
npm run test:unit
npm run test:integration
npm run test:security
```

### Writing Tests

```javascript
// tests/unit/my-feature.test.js
import { describe, it, expect, beforeEach } from 'vitest';
import { MyFeature } from '../../src/my-feature.js';

describe('MyFeature', () => {
  let feature;
  
  beforeEach(() => {
    feature = new MyFeature({});
  });
  
  describe('myMethod', () => {
    it('should handle valid input', () => {
      const result = feature.myMethod('valid');
      expect(result).toBe(true);
    });
    
    it('should reject invalid input', () => {
      expect(() => feature.myMethod(null)).toThrow();
    });
    
    it('should handle edge cases', () => {
      // Test edge cases
    });
  });
});
```

### Test Requirements

- All new features must have tests
- All bug fixes must have regression tests
- Security-sensitive code requires security tests
- Maintain >80% code coverage

---

## Pull Request Process

### 1. Create a Branch

```bash
git checkout -b feature/my-feature
# or
git checkout -b fix/bug-description
```

### 2. Make Changes

- Follow coding standards
- Add/update tests
- Update documentation

### 3. Commit

Use [Conventional Commits](https://www.conventionalcommits.org/):

```bash
# Format: type(scope): description

git commit -m "feat(scanner): add AWS key detection"
git commit -m "fix(dashboard): resolve login redirect issue"
git commit -m "docs(readme): add installation instructions"
git commit -m "test(secrets): add unit tests for masking"
git commit -m "security(auth): use timing-safe comparison"
```

Types: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`, `security`

### 4. Push and Create PR

```bash
git push origin feature/my-feature
```

Then create a Pull Request on GitHub.

### 5. PR Requirements

- [ ] Tests pass (`npm test`)
- [ ] Linting passes (`npm run lint`)
- [ ] Security audit passes (`npm run audit:deps`)
- [ ] Documentation updated (if needed)
- [ ] Follows coding standards
- [ ] No merge conflicts

### 6. Review Process

1. Automated checks run
2. Maintainer reviews code
3. Address feedback
4. Approval and merge

---

## Release Process

*(For maintainers)*

1. Update version in `package.json`
2. Update `CHANGELOG.md`
3. Create git tag: `git tag v1.0.0`
4. Push tag: `git push --tags`
5. CI publishes to npm

---

## Recognition

Contributors are recognized in:

- `CHANGELOG.md` (per release)
- `README.md` (significant contributions)
- GitHub contributors page

---

## Questions?

- 💬 [Open an issue](https://github.com/2pidata/openclaw-security-guard/issues)
- 📧 Contact maintainer via GitHub

---

## Thank You!

Every contribution, no matter how small, helps make this tool better for everyone. 🙏

**Happy coding!** 🦞🛡️
