# VSLLama

A privacy-first VS Code extension that connects to local Ollama and cloud AI providers (OpenAI, Anthropic, Gemini, NVIDIA NIM, Perplexity, Ollama Cloud, llama.cpp) for chat and coding help.  
MCP integration is optional (can be enabled/disabled).

## Features (v2.2.0)
- **Agentic Mode**: Autonomous task execution with tool-use (MCP) support.
- **Planning Mode**: Generate and manage detailed architectural implementation plans.
- **Smart Model Routing**: Automatically switch between reasoning models (planning) and coding models (execution).
- **Expanded AI Providers**: Stream responses from Ollama, OpenAI, Anthropic, Gemini, NVIDIA NIM, Perplexity, Ollama Cloud, and llama.cpp.
- **Dark / Light Theme System**: Dynamic theme toggle button (`🌓`) with persistent local preference storage.
- **WCAG Accessibility & ARIA Support**: Full `aria-label` coverage on all interactive controls, high-contrast focus outlines, and an `aria-live` polite status announcer for screen readers.
- **Interactive Error Recovery**: One-click error card dismissal and `↩️ Undo Last Message` to quickly step back conversation turns.
- **Streaming Progress Bar**: Visual indeterminate progress indicator displaying real-time generation and tool execution states.
- **Visual Tool Call Classification**: Type-specific icons and colored borders for tool calls (📖 Read, ✏️ Write, 🚀 Exec, 🗑️ Delete) with syntax highlighting for code output.
- **Real BPE Token Estimation**: Precise Byte-Pair Encoding token counts powered by `gpt-tokenizer`.
- **MCP Resilience & Auto-Reconnect**: Automatic disconnect detection with exponential backoff reconnects (up to 5 retries).
- **Security Hardened**: Shell injection prevention using argv array execution (`shell: false`), path traversal bounds checking, centralized error sanitizer (`sanitizeErrorMessage`), and workspace-bound audit logging (`system_events/audit.log`).
- **Dynamic Model Search & Lock Badges**: Live model search filtering for provider dropdowns (>10 models) and background `ModelProber` accessibility checks that dynamically display `🔒` lock badges.
- **AI-Driven Critique Loop**: Optional post-change self-verification using the project's own build system/test tooling to auto-detect and resolve errors.
- **Configurable Rate Limiting & Response Caching**: Global and per-provider sliding-window rate limiting with SHA-256 cache keys and dedicated model-list caching (15-min TTL).
- **Code Autocomplete**: AI-powered inline ghost text suggestions.
- **Interactive Onboarding**: Guided setup for first-time users.
- **Smart Git Commits**: Context-aware commit message generation.
- **CI / CD Pipeline**: GitHub Actions CI workflow covering type checks, linting, builds, and security audits.

## Requirements
- VS Code `^1.107.0`
- Node `>=18.0.0`
- An active AI provider (e.g. Ollama running locally at http://localhost:11434, or an API Key for OpenAI, Anthropic, Gemini, NVIDIA NIM, Perplexity, or Ollama Cloud)

## Quick Start
1. **Install**: Install from [VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=VijayTank.vsllama)
2. **Open Chat**: Click the VSLLama icon (Llama silhouette) in the Activity Bar
3. **Choose Provider & Model**: Select your provider and model from the header dropdowns
4. **Theme Preference**: Click `🌓` in the header bar to switch between Dark and Light themes
5. **Start Chatting**: Type your message and press Enter

For detailed instructions, see the [User Guide](USER_GUIDE.md).

## Usage

### Chat Modes
- **Agent Mode** (default): AI autonomously executes tasks with MCP tool integration. You approve before tools are used.
- **Chat Mode**: Traditional conversational interaction without tool execution.
- **Plan Mode**: Generate structured architectural plans and implementation strategies.

### Code Actions
Right-click on any selected code in the editor to access VSLLama tools:
- **Explain This Code**: Step-by-step code breakdown
- **Fix This Code**: Bug identification and fixes
- **Generate Unit Tests**: Automatic test generation
- **Add Documentation**: Javadoc/JSDoc comments
- **Generate Code**: Write code from descriptions

**Keyboard Shortcuts:**
- `Ctrl+Shift+L` (or `Cmd+Shift+L`): Explain Code
- `Ctrl+Shift+F` (or `Cmd+Shift+F`): Fix Code
- `Ctrl+Shift+T` (or `Cmd+Shift+T`): Generate Tests
- `Ctrl+Shift+D` (or `Cmd+Shift+D`): Add Docs
- `Ctrl+Shift+G` (or `Cmd+Shift+G`): Generate Code

### Code Autocomplete
Enable AI-powered inline ghost text suggestions:
1. Open VS Code Settings (`Ctrl+,`)
2. Search for `VSLLama`
3. Enable **Autocomplete Enabled**
4. Code suggestions appear after a short pause (default: 800ms)
5. Manual trigger: Press `Alt+\`
6. Accept suggestion: Press `Tab`

### Git Integration
Generate commit messages based on your changes:
1. Stage changes in the **Source Control** view (or leave unstaged)
2. Click the **Sparkle icon** ✨ in the Source Control header
3. Review the generated message in the Chat Sidebar
4. Click **Apply** to populate your commit message

## Configuration

Access settings with `Ctrl+,` and search for `VSLLama`:

### Provider & Model Selection
- `provider`: AI Provider (`ollama`, `openai`, `anthropic`, `gemini`, `nvidianim`, `perplexity`, `ollamacloud`, `llamacpp`)
- `ollamaUrl`: Local Ollama instance URL (default: `http://127.0.0.1:11434`)
- `openaiUrl`: Base URL for OpenAI API (default: `https://api.openai.com/v1`)
- `anthropicUrl`: Base URL for Anthropic API (default: `https://api.anthropic.com/v1`)
- `geminiUrl`: Base URL for Gemini API (default: `https://generativelanguage.googleapis.com/v1beta`)
- `nvidianimUrl`: Base URL for NVIDIA NIM API (default: `https://integrate.api.nvidia.com/v1`)
- `perplexityUrl`: Base URL for Perplexity API (default: `https://api.perplexity.ai`)
- `ollamacloudUrl`: Base URL for Ollama Cloud API (default: `https://ollama.com`)
- `llamacppUrl`: Base URL for llama.cpp server (default: `http://localhost:8080/v1`)
- `model`: Default LLM (defaults to `auto`)
- `defaultMode`: Default chat mode (`agent`, `chat`, `plan`)
- `planningModel`: Optional specific model for planning phase
- `executionModel`: Optional specific model for execution phase

### Autocomplete Settings
- `autocompleteEnabled`: Toggle inline ghost text completions
- `autocompleteDelay`: Milliseconds before triggering autocomplete (default: 800ms)

### Rate Limiting
- `rateLimiting.enabled`: Enable sliding-window rate limiting globally (default: `true`)
- `rateLimiting.<provider>.maxRequests`: Max requests allowed in window for a provider
- `rateLimiting.<provider>.windowMs`: Rate limit window in milliseconds for a provider

### AI Critique Loop
- `critiqueLoop.enabled`: Enable self-verification using local build tools (default: `true`)
- `critiqueLoop.maxRetries`: Maximum auto-correction attempts (default: `2`)

### MCP Configuration
- `mcpServers`: Definitions for MCP tool servers (stdio, sse, streamable HTTP, WebSocket)

**💡 Tip**: You can easily switch providers, set API Keys, toggle themes (`🌓`), and check MCP server status (`🔌 MCP`) directly from the header controls in the VSLLama chat view.

## Troubleshooting

### Common Issues
1. **Extension won't connect to Ollama**
   - Verify Ollama is running: `http://127.0.0.1:11434`
   - Check firewall/networking settings
   - Try reloading VS Code (`Ctrl+R`)

2. **API Rate Limits (HTTP 429) & Forbidden Access (HTTP 403 / 402)**
   - Adjust `vsllama.rateLimiting` settings to reduce request frequency
   - Inspect model `🔒` lock badges (indicated by the `ModelProber` background service)

3. **MCP Server Issues**
   - Check the `🔌 MCP` section in the chat header for connection status
   - VSLLama automatically attempts reconnection (up to 5 retries with exponential backoff) if an MCP server disconnects

4. **Interactive Session Recovery**
   - Use `↩️ Undo Last Message` on error cards to revert conversation turns cleanly
   - Dismiss error notifications via the `✕` button

### Getting Help
- Use the **Retry** or **Undo** buttons in error cards
- Check API keys in the Settings overlay (`⚙️`)
- Run `VSLLama: Reset Onboarding` from the command palette if needed

## Privacy & Security
VSLLama is **privacy-first**:
- Local Ollama & llama.cpp modes keep code and conversations on your machine
- API keys are securely stored in VS Code's native `SecretStorage` (OS Keychain API)
- Sensitive Bearer tokens, API keys, and local file paths are redacted via `sanitizeErrorMessage`
- Command tool executions are run via argv array tokens (`shell: false`) to prevent command injection
- All filesystem tool operations are verified against workspace boundaries with log auditing in `system_events/audit.log`

## License
MIT License - See [LICENSE](LICENSE) for details

---

**Need help?** Visit the [User Guide](USER_GUIDE.md) for detailed documentation and advanced configuration.
