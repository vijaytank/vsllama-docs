# VSLLama Changelog

All notable changes to this project will be documented in this file.

## [2.0.1] - 2026-06-16

### Added
- **Agentic Mode**: Autonomous task execution with MCP tool integration and user approval for tool execution
- **Planning Mode**: Generate structured implementation plans for architectural decisions
- **Smart Model Routing**: Automatically switch between reasoning models (planning) and coding models (execution)
- **Expanded AI Providers**: Added support for NVIDIA NIM, Perplexity, Ollama Cloud, and llama.cpp
- **AI-Driven Critique Loop**: Optional post-change self-verification using project's build system/test tooling
- **Streaming Retry Resilience**: Automatic retry handling for network blips and cold-starts on all streaming providers
- **JSON Parsing Repair**: Automatic correction of malformed JSON outputs from LLM providers
- **Collapsible Reasoning Blocks**: AI thinking processes (`<think>` tags) now render in expandable details sections
- **Enhanced Tool Call Visualization**: System tool calls and results grouped in expandable sections for debugging
- **Pulsing Status Indicator**: Real-time feedback showing AI status (starting, thinking, generating, executing tools, resuming)
- **Interactive Onboarding**: Guided setup for first-time users with provider selection

### Improved
- **UI/UX Enhancements**: Long messages (5+ lines) collapse by default to save screen space
- **Rate Limiting**: Global and per-provider sliding-window configuration for API rate limit management
- **Error Recovery**: One-click retry buttons and settings shortcuts for actionable error handling
- **MCP Tool Integration**: Full support with connection pooling and idle timeout management
- **Response Caching**: Performance optimized with built-in caching mechanisms
- **Git Commit Generation**: Enhanced context-awareness for staged and unstaged changes

### Configuration
- Added `planningModel` and `executionModel` settings for smart routing
- Added `critiqueLoop.enabled` and `critiqueLoop.maxRetries` for self-verification
- Added per-provider rate limiting configuration
- All settings accessible from Environment tab without file editing

## [1.0.0] - 2026-02-24

### Added
- Sidebar chat view with streaming responses from Ollama
- MCP Tool Integration (Phase 1)
- Code Autocomplete (Inline Ghost Text)
- Smart Git Commit Message Generation
- Code Actions: Explain, Fix, Generate Tests, Add Docs, Generate Code
- Support for Ollama, OpenAI, Anthropic, and Gemini providers
- Secure API key storage via VS Code SecretStorage
- Interactive webview with collapsible sections
- Full MCP server support with stdio connections

---

## Version History

| Version | Release Date | Major Changes |
|---------|--------------|---------------|
| 2.0.1 | 2026-06-16 | Agentic mode, planning, smart routing, expanded providers |
| 1.0.0 | 2026-02-24 | Initial release with core features |

---

**For upgrade guidance**, visit the [User Guide](USER_GUIDE.md).
