# Changelog

All notable changes to OpenClaw Security Guard will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [Unreleased]

### Planned
- Email alert integration
- Slack/Discord notifications
- PDF report export
- Additional prompt injection patterns
- Docker support
- Prometheus metrics export

---

## [1.0.0] - 2026-02-13

### 🎉 Initial Release

**Author:** Miloud Belarebia ([@miloudbelarebia](https://github.com/miloudbelarebia))

#### Added

**CLI Scanner**
- 🔍 **Secrets Scanner** - Detects 15+ types of secrets (OpenAI, Anthropic, AWS, etc.)
- 🔧 **Config Auditor** - Validates OpenClaw configuration against 15+ security rules
- 💉 **Prompt Injection Detector** - Detects 50+ injection patterns across 10 categories
- 📦 **Dependency Scanner** - Checks for vulnerable npm packages
- 🔌 **MCP Server Auditor** - Validates installed MCP servers

**Live Dashboard**
- 📊 Real-time security score (0-100)
- 📈 Request monitoring
- 💰 Cost tracking
- 🚨 Live alerts
- 🔐 Password protection

**Auto-Fix**
- Automatic backup before changes
- Interactive or automatic mode
- Detailed change logging

**Security**
- Input validation with Zod
- Path traversal protection
- XSS prevention in reports
- Timing-safe password comparison
- Secure session tokens

**Developer Experience**
- GitHub Actions CI/CD
- Pre-commit hooks support
- Comprehensive test suite
- Multi-language support (EN, FR, AR)

#### Security

- ✅ No telemetry or tracking
- ✅ No external network requests
- ✅ No `eval()` or dynamic code execution
- ✅ All inputs validated
- ✅ Secrets masked in output
- ✅ Localhost-only dashboard

---

## Version History

| Version | Date | Highlights |
|---------|------|------------|
| 1.0.0 | 2026-02-13 | Initial release |

---

## Contributors

- **Miloud Belarebia** - Creator & Maintainer

---

## Links

- [GitHub Repository](https://github.com/2pidata/openclaw-security-guard)
- [npm Package](https://www.npmjs.com/package/openclaw-security-guard)
- [Documentation](https://github.com/2pidata/openclaw-security-guard#readme)
- [2pidata.com](https://2pidata.com)
