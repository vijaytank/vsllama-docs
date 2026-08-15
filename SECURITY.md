# VSLLama Security Policy & Hardening Guidelines

> **Last Security Audit:** 2026-08-13  
> **Production Dependencies Status:** 0 Critical / 0 High / 0 Moderate / 0 Low (Production dependencies are 100% clean)

VSLLama is designed from the ground up as a **privacy-first and security-hardened** AI coding companion for VS Code.

---

## 🛡️ Supported Versions

Security updates and patches are actively released for the following versions:

| Version | Supported |
| ------- | --------- |
| 2.2.x   | :white_check_mark: |
| 2.1.x   | :white_check_mark: |
| 2.0.x   | :x: |
| < 2.0   | :x: |

---

## 🔐 Production Hardening & Security Architecture

1. **Native OS Credential Storage (`SecretStorage`)**
   - All AI Provider API Keys (OpenAI, Anthropic, Gemini, NVIDIA NIM, Perplexity, Ollama Cloud) are stored using VS Code's native `SecretStorage` API.
   - Credentials are backed by OS-level keychains (DPAPI on Windows, Keychain on macOS, libsecret on Linux) and never written to plain-text settings files or disk logs.

2. **Command Injection Prevention (`shell: false`)**
   - Tool execution (`run_command`) passes arguments via tokenized argv arrays with `shell: false`.
   - Command string concatenation and shell metacharacter evaluation (such as `;`, `&&`, `|`, `` ` ``) are explicitly prevented.

3. **Workspace Bounds & Path Confinement**
   - File system tool operations (reading, writing, deleting) undergo path normalization and boundary verification (`getAbsolutePath()`) to ensure operations cannot escape the active workspace root directory.

4. **Error Log Sanitization (`sanitizeErrorMessage`)**
   - All outgoing error tracebacks and user-facing notifications are passed through a centralized error sanitizer.
   - Bearer tokens, provider API keys (`sk-`, `nvapi-`, `AIzaSy`, `pplx-`), and local OS file paths are automatically redacted prior to rendering or logging.

5. **Structured Audit Logging**
   - High-privilege actions and system events produce structured JSON audit records in `system_events/audit.log` within the workspace root.
   - Audit logs feature automatic 10 MB log rotation to prevent unbounded disk usage.

---

## 📩 Reporting a Vulnerability

If you discover a potential security vulnerability within VSLLama, please report it privately:

- **Email**: Security reports can be sent directly to the repository maintainer.
- **GitHub**: Submit a confidential advisory via [GitHub Security Advisories](https://github.com/vijaytank/vsllama-docs/security/advisories).

Please include:
- A description of the issue and potential impact.
- Steps to reproduce or proof-of-concept code.

We aim to acknowledge receipt of vulnerability reports within 24–48 hours and provide updates until resolution.
