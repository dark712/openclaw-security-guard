# Security Policy

## 🛡️ OpenClaw Security Guard - Security Policy

**Author:** Miloud Belarebia  
**Website:** [2pidata.com](https://2pidata.com)

---

## Our Commitment

As a security tool, we hold ourselves to the highest standards. This tool:

- ✅ Contains **no telemetry or tracking**
- ✅ Makes **no external network requests**
- ✅ Stores **no data** outside your machine
- ✅ Is **fully auditable** as open source

---

## Supported Versions

| Version | Supported |
|---------|-----------|
| 1.x.x   | ✅ Yes    |
| < 1.0   | ❌ No     |

---

## Reporting a Vulnerability

If you discover a security vulnerability, please report it responsibly.

### 📧 Contact

**Preferred:** Open a [GitHub Security Advisory](https://github.com/2pidata/openclaw-security-guard/security/advisories/new)

**Alternative:** Email security concerns to the maintainer via GitHub

### 📝 What to Include

1. **Description** of the vulnerability
2. **Steps to reproduce**
3. **Potential impact**
4. **Suggested fix** (if any)

### ⏱️ Response Time

| Severity | Acknowledgment | Fix Timeline |
|----------|----------------|--------------|
| Critical | 24 hours | 48-72 hours |
| High | 48 hours | 7 days |
| Medium | 7 days | 30 days |
| Low | 14 days | 60 days |

### 🏆 Recognition

We acknowledge all valid security reports in our CHANGELOG and README.

---

## Security Measures

### Code Security

| Measure | Status | Description |
|---------|--------|-------------|
| No `eval()` | ✅ | No dynamic code execution |
| No `Function()` | ✅ | No function constructor |
| No shell injection | ✅ | Commands are parameterized |
| Input validation | ✅ | All inputs validated with Zod |
| Path sanitization | ✅ | Protection against traversal |
| XSS prevention | ✅ | HTML output is escaped |

### Authentication Security

| Measure | Status | Description |
|---------|--------|-------------|
| Password hashing | ✅ | PBKDF2 with 100,000 iterations |
| Salt per password | ✅ | Unique 16-byte salt |
| Timing-safe compare | ✅ | Prevents timing attacks |
| Secure sessions | ✅ | 32-byte random tokens |
| Session expiry | ✅ | 24-hour automatic expiry |

### Network Security

| Measure | Status | Description |
|---------|--------|-------------|
| Localhost binding | ✅ | Dashboard binds to 127.0.0.1 |
| No external calls | ✅ | Zero telemetry or phone-home |
| No data collection | ✅ | 100% private |

### Dependency Security

| Measure | Status | Description |
|---------|--------|-------------|
| Minimal dependencies | ✅ | Only essential packages |
| Regular audits | ✅ | `npm audit` in CI |
| Version pinning | ✅ | Exact versions in lockfile |

---

## Secure Development Practices

### For Contributors

Before submitting code, ensure:

- [ ] No hardcoded secrets or credentials
- [ ] No use of `eval()`, `Function()`, or `vm.runInContext()`
- [ ] All user inputs are validated
- [ ] File paths are sanitized
- [ ] External commands are parameterized (never concatenated)
- [ ] Tests cover security-sensitive code
- [ ] `npm audit` passes

### Code Review Checklist

Security reviewers check for:

- [ ] Input validation on all entry points
- [ ] Output encoding/escaping
- [ ] Authentication and authorization
- [ ] Cryptographic implementations
- [ ] Error handling (no sensitive info in errors)
- [ ] Logging (no secrets logged)
- [ ] Dependencies (no known vulnerabilities)

---

## Threat Model

### Assets Protected

1. **User's OpenClaw configuration**
2. **User's API keys and secrets**
3. **Dashboard access**
4. **Local file system**

### Threats Considered

| Threat | Mitigation |
|--------|------------|
| Malicious input | Input validation, sanitization |
| Path traversal | Path normalization, containment |
| XSS in reports | HTML escaping |
| Brute force login | Rate limiting, secure hashing |
| Session hijacking | Secure random tokens, expiry |
| Dependency attacks | Minimal deps, regular audits |

### Out of Scope

- Physical access to user's machine
- Compromised Node.js runtime
- Compromised npm registry

---

## Known Limitations

1. **Pattern-based detection** - Secrets scanner uses regex, may have false positives/negatives
2. **Point-in-time** - Scans show current state only
3. **Local execution** - Cannot detect remote threats
4. **User trust** - User must protect their dashboard password

---

## Security Checklist for Users

### When Using This Tool

- ✅ Keep the tool updated
- ✅ Protect your dashboard password
- ✅ Review security reports before sharing
- ✅ Don't run as root unless necessary

### When Deploying OpenClaw

Based on our recommendations:

1. Set sandbox mode: `always`
2. Set DM policy: `pairing`
3. Bind gateway to: `loopback`
4. Enable rate limiting
5. Disable elevated mode
6. Use environment variables for secrets (not config files)

---

## Audit Log

| Date | Auditor | Scope | Result |
|------|---------|-------|--------|
| 2026-02-13 | Self-audit | Full codebase | Pass |

---

## Contact

**Maintainer:** Miloud Belarebia

**Website:** [2pidata.com](https://2pidata.com)

**For security consulting:** [Contact 2pidata](https://2pidata.com)

---

*This security policy is reviewed and updated with each major release.*
