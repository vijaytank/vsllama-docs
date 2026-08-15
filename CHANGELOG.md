# VSLLama Changelog

All notable changes to this project will be documented in this file.

Check [Keep a Changelog](http://keepachangelog.com/) for recommendations on how to structure this file.

## [2.2.0] - 2026-08-15

### Added
- **Dynamic Model Search & Natural Sorting**: Real-time live model search filtering in the Settings panel when provider model list length > 10, with natural alphanumeric sorting across Settings cards and toolbar dropdowns.
- **Staggered Background Model Prober (`ModelProber`)**: Staggered background accessibility checks for cloud providers returning > 5 models to dynamically render `🔒` lock badges in the UI and populate `lockedModelsCache`.
- **Centralized Error Redaction (`sanitizeErrorMessage`)**: Centralized utility in `src/utils/errorSanitizer.ts` to redact Bearer tokens, API keys (`sk-`, `nvapi-`, `AIzaSy`, `pplx-`), and local OS file paths across all 8 AI clients.
- **MCP Transport Adapters (`normalizeTransport`)**: Safe, explicit transport normalization for stdio, SSE, StreamableHTTP, and WebSocket transports.
- **Abortable RetryWrapper & Timeout Helper (`createTimeoutSignal`)**: Added `signal?: AbortSignal` support and `abortableSleep` to guarantee instant prompt cancellations during backoff delays.

### Refactored & Cleaned
- **ESLint Compliance**: Enforced strict `curly` brace formatting across `chatService.ts` and `sessionManager.ts`, resolving all lint warnings (0 errors, 0 warnings).
- **Robust Tool Call Extraction**: Upgraded `extractToolCalls` to parse `[TOOL: ...]` blocks anywhere in model text output with support for string escaping, missing parentheses, and relaxed JSON format healing.
- **Webview Message Handling & XSS Safety**: Enforced strict `escapeHtml` sanitization across dynamic DOM elements in webview media and async routing for `approvePlan`, `continueChat`, `testApiKey`, and `refreshMcp`.
- **Node Engine Specifications**: Specified `"engines": { "vscode": "^1.107.0", "node": ">=18.0.0" }`.

### Fixed
- **Cloud Provider Streaming Errors**: Fixed silent hangs, empty response errors, and infinite loops across NVIDIA NIM, OpenAI, Perplexity, Anthropic, Gemini, and Ollama Cloud by inspecting SSE line frames for `data.error` / `data.detail` payloads and throwing descriptive error messages immediately.
- **HTTP 403 & 402 Error Handling**: Added dedicated status code handlers for `403 Forbidden` (subscription/plan required) and `402 Payment Required` (credits required).
- **Auto Mode Selection**: Automatically excluded dynamically locked (`🔒`) models from `Auto` mode heuristic selectors (`heuristicallySelectFastModel` and `heuristicallySelectHeavyModel`).

## [2.1.0] - 2026-08-13

### Added
- **Theme & Visual System**: Dark/light theme toggle button (`🌓`) in chat header with persistent user preference storage.
- **Accessibility & ARIA Compliance**: Full WCAG compliance with `aria-label` coverage across all controls and an `aria-live` screen reader status announcer (`polite`).
- **Interactive Error Recovery**: Structured error card UI featuring error dismissal (`✕`) and a one-click `↩️ Undo Last Message` button to revert context turns.
- **Streaming Progress Bar**: Visual indeterminate progress animation during model streaming and tool execution.
- **Tool Call Visual Classification**: Distinct color-coded borders and type icons for tool calls (📖 Read, ✏️ Write, 🚀 Exec, 🗑️ Delete) with syntax highlighting for code output.
- **Byte-Pair Encoding Tokenization**: Real BPE token count estimation using `gpt-tokenizer`.
- **MCP Auto-Reconnect**: Automatic transport disconnect detection and exponential backoff auto-reconnect (up to 5 retries).
- **Audit Logging**: Workspace-bound structured audit logging in `system_events/audit.log` with 10 MB log rotation.
- **CI Pipeline**: Automated GitHub Actions workflow covering type-checking, linting, pretest builds, and security audits.

### Changed
- **Security Hardening**: Refactored command execution to use argv arrays with `shell: false`, eliminating shell injection risks.
- **Cache Optimizations**: Created dedicated `modelListCache` with a 15-minute TTL to reduce redundant provider model queries.
- **Session Manager Persistence**: Directly backed by VS Code global state.

## [2.0.0] - 2026-05-04

### Added
- **Major Architectural Overhaul**: Transitioned to a service-oriented architecture with dedicated `ChatService`, `MessageHandler`, `SessionManager`, and `PlanManager`.
- **Agentic Mode**: Autonomous task execution with tool-use (MCP) support.
- **Planning Mode**: Generate and manage detailed architectural implementation plans.
- **Expanded AI Providers**: Added support for NVIDIA NIM, Perplexity, Ollama Cloud, and llama.cpp.
- **Smart Model Routing**: Automatic selection of reasoning vs. coding models based on task context.
- **Comprehensive Test Suite**: Test coverage across core services, AI clients, and utilities.

## [1.0.0] - 2026-02-24

### Added
- Sidebar chat view with streaming responses from Ollama, OpenAI, Anthropic, and Gemini.
- MCP Tool Integration (Phase 1).
- Code Autocomplete (Inline Ghost Text).
- Smart Git Commit Message Generation.
- Code Actions: Explain, Fix, Generate Tests, Add Docs, Generate Code.
- Secure API key storage via VS Code SecretStorage.

---

## Version History

| Version | Release Date | Major Changes |
|---------|--------------|---------------|
| 2.2.0 | 2026-08-15 | Dynamic model search, ModelProber, error sanitizer, timeout signals |
| 2.1.0 | 2026-08-13 | Theme toggle (`🌓`), WCAG ARIA compliance, Undo Last Message, BPE tokenization, MCP auto-reconnect, audit logging |
| 2.0.0 | 2026-05-04 | Service architecture, Agentic & Plan modes, expanded cloud AI providers |
| 1.0.0 | 2026-02-24 | Initial release with core features |

---

**For upgrade guidance**, visit the [User Guide](USER_GUIDE.md).
