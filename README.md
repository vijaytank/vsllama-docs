# VSLLama

A privacy-first VS Code extension that connects to local Ollama and cloud AI providers (OpenAI, Anthropic, Gemini, NVIDIA NIM, Perplexity, Ollama Cloud) for chat and coding help.  
MCP integration is optional (can be enabled/disabled).

## Features (v2.0.1)
- **Agentic Mode**: Autonomous task execution with tool-use (MCP) support. The AI creates implementation plans for complex tasks and asks for your approval before using tools.
- **Planning Mode**: Generate and manage detailed implementation plans for architectural decisions.
- **Smart Model Routing**: Automatically switch between reasoning models (for planning) and coding models (for execution).
- **Expanded AI Providers**: Stream responses from Ollama, OpenAI, Anthropic, Gemini, NVIDIA NIM, Perplexity, Ollama Cloud, and llama.cpp.
- **AI-Driven Critique Loop**: Optional post-change self-verification using your project's own build system/test tooling to auto-detect and resolve errors.
- **Configurable Rate Limiting**: Global and per-provider sliding-window rate limiting settings to prevent API rate limits from interrupting operations.
- **Streaming Retry Resilience**: Initial connection retry resilience for all streaming providers against network blips and cold-starts.
- **JSON Parsing Repair**: Automatic correction of malformed JSON outputs from LLM providers.
- **UI/UX & Debugging Enhancements**: Collapsible reasoning blocks (`<think>`), tool calls, and long user messages; pulsing generation indicator; and enhanced error details.
- **MCP Tool Integration**: Full support with connection pooling and idle timeouts for Model Context Protocol servers.
- **Code Autocomplete**: AI-powered inline ghost text suggestions as you type.
- **Interactive Onboarding**: Guided setup for first-time users.
- **Actionable Error Recovery**: One-click retry and settings shortcuts.
- **Smart Git Commits**: Context-aware commit message generation from staged/unstaged changes.
- **Performance Optimized**: Built-in sliding-window rate limiting and response caching.

## Requirements
- VS Code (v1.109.0 or higher)
- An active AI provider:
  - **Local**: Ollama running at `http://localhost:11434`
  - **Cloud**: API Key for OpenAI, Anthropic, Gemini, NVIDIA NIM, Perplexity, or Ollama Cloud

## Quick Start
1. **Install**: Install from [VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=VijayTank.vsllama)
2. **Open Chat**: Click the VSLLama icon (Llama silhouette) in the Activity Bar
3. **Choose Provider**: Click the **Environment** tab to select your AI provider
4. **Start Chatting**: Type your message and press Enter

For detailed instructions, see the [User Guide](USER_GUIDE.md).

## Usage

### Chat Modes
- **Agent Mode** (default): AI autonomously executes tasks with MCP tool integration. You approve before tools are used.
- **Chat Mode**: Traditional conversational interaction without tool execution.
- **Plan Mode**: Generate structured architectural plans and implementation strategies.

Switch modes in the **Environment** tab of the VSLLama chat sidebar.

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
1. Stage changes in the **Source Control** view
2. Click the **Sparkle icon** in the Source Control header
3. Review the generated message in the Chat Sidebar
4. Click **Apply** to populate your commit message

## Configuration

Access settings with `Ctrl+,` and search for `VSLLama`:

### Provider & Model Selection
- `provider`: AI Provider (`ollama`, `openai`, `anthropic`, `gemini`, `nvidianim`, `perplexity`, `ollamacloud`, `llamacpp`)
- `model`: Default LLM (defaults to `auto`)
- `defaultMode`: Default chat mode (`agent`, `chat`, `plan`)
- `planningModel`: Optional specific model for planning phase
- `executionModel`: Optional specific model for execution phase

### Autocomplete Settings
- `autocompleteEnabled`: Toggle inline ghost text completions
- `autocompleteDelay`: Milliseconds before triggering autocomplete (default: 800ms)

### Rate Limiting
- `rateLimiting.enabled`: Enable sliding-window rate limiting (default: `true`)
- `rateLimiting.<provider>.maxRequests`: Max requests in window (e.g., `50` for OpenAI)
- `rateLimiting.<provider>.windowMs`: Rate limit window in milliseconds (e.g., `60000` for 1 minute)

### AI Critique Loop
- `critiqueLoop.enabled`: Enable self-verification using local build tools (default: `true`)
- `critiqueLoop.maxRetries`: Maximum auto-correction attempts (default: `2`)

### MCP Configuration
- `mcpServers`: Definitions for MCP tool servers (stdio-based connections)

**💡 Tip**: You can easily switch providers and set API Keys directly from the **Environment** tab in the VSLLama chat view without editing config files.

## Troubleshooting

### Common Issues
1. **Extension won't connect to Ollama**
   - Verify Ollama is running: `http://localhost:11434`
   - Check firewall/networking settings
   - Try reloading VS Code (`Ctrl+R`)

2. **API Rate Limits (HTTP 429)**
   - Adjust `vsllama.rateLimiting` settings to reduce request frequency
   - Increase `windowMs` or decrease `maxRequests` for affected providers

3. **MCP Server Issues**
   - Check the **MCP Tools** section in the chat sidebar for connection status
   - Verify MCP server configuration in settings

4. **Streaming Errors**
   - Extension automatically retries failed connections
   - Check your internet connection and API endpoint URLs
   - Review error details in the **Environment** tab

### Getting Help
- Use the **Retry** button in error cards
- Check API keys in the **Environment** tab
- Run `VSLLama: Reset Onboarding` from the command palette if needed
- Enable debug logging in settings for detailed error information

## Roadmap
- Add "Use selection" and "Apply edits" features
- Interactive MCP Tool confirmation UI
- Enhanced local context with RAG integration
- Support for additional AI providers

## Privacy
VSLLama is **privacy-first**:
- Local Ollama mode keeps all code and conversations on your machine
- API keys are securely stored in VS Code's built-in SecretStorage
- No telemetry or data collection
- All processing respects your workspace boundaries

## License
MIT License - See [LICENSE](LICENSE) for details

---

**Need help?** Visit the [User Guide](USER_GUIDE.md) for detailed documentation and advanced configuration.
