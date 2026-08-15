# VSLLama User Guide (v2.2.0)

Welcome to **VSLLama**, your privacy-first AI coding companion powered by local LLMs and MCP (Model Context Protocol).

## 🚀 Getting Started

### 1. Prerequisites
- **VS Code**: Version `1.107.0` or higher
- **Node.js**: Version `18.0.0` or higher
- **AI Provider**: You can use:
  - **Local**: [Ollama](https://ollama.ai/) running at `http://127.0.0.1:11434` or [llama.cpp](https://github.com/ggerganov/llama.cpp) server at `http://localhost:8080/v1`
  - **Cloud**: API keys for OpenAI, Anthropic, Gemini, NVIDIA NIM, Perplexity, or Ollama Cloud

### 2. Setting Up the AI Provider

1. Open the **VSLLama Chat Sidebar** (Llama icon in the Activity Bar).
2. Use the header controls and dropdowns:
   - **Theme Toggle (`🌓`)**: Instantly switch between Dark and Light UI themes. Your choice is automatically saved.
   - **Mode Selector**: Choose between **Agent**, **Chat**, and **Plan** modes.
   - **Model Selector**: Select your preferred provider and model (or select "Auto (Smart Routing)").
   - **Settings Overlay (`⚙️`)**: Manage API Keys and custom Base URLs.
3. If using a cloud provider, enter your **API Key** in the settings overlay:
   - Keys are securely stored in VS Code's native `SecretStorage` (OS Keychain API).
4. (Optional) Specify custom Base URLs in settings (e.g., `vsllama.openaiUrl`, `vsllama.llamacppUrl`).

### 3. Selecting Your Default Mode

Choose your preferred chat mode from the top header:

- **Agent Mode** (default): Autonomous task execution with MCP tool support. The AI creates implementation plans and requests approval before executing tools.
- **Chat Mode**: Traditional conversational interaction without tool execution.
- **Plan Mode**: Generate structured architectural plans and implementation strategies.

---

## 🛠️ Usage

### Sidebar Chat

1. Click the **VSLLama icon** in the Activity Bar.
2. Type your message in the chat box.
3. Use the header controls:
   - Toggle theme (`🌓`)
   - Select modes and models
   - Check `🔌 MCP` status badge
   - Access `⚙️ Settings` overlay

### UI/UX & Accessibility Features

The chat view includes rich visual, interactive, and accessibility enhancements:

- **Dark / Light Theme**: Click `🌓` in the header bar to flip between dark glassmorphism and light themes.
- **Accessibility & Screen Readers**:
  - Full WCAG 2.1 compliance with explicit `aria-label` attributes across all interactive buttons, inputs, and selectors.
  - Visible keyboard focus outlines (`:focus-visible`).
  - Screen reader status announcer (`aria-live="polite"`) announcing text generation status, theme switches, and errors.
- **Interactive Error Cards**:
  - Error occurrences render actionable cards displaying the error summary.
  - Includes a `✕` dismiss button and a `↩️ Undo Last Message` button to cleanly revert the last conversation turn.
- **Streaming Progress Bar**: Visual progress indicator (`.chat-progress`) displaying real-time text generation and tool execution.
- **Tool Call Visuals & Syntax Highlighting**:
  - Tool calls feature distinct color-coded borders and type icons: 📖 Read (`read_file`, `list_files`), ✏️ Write (`write_file`, `edit_file`, `create_file`), 🚀 Exec (`run_command`), and 🗑️ Delete (`delete_file`).
  - Code outputs are syntax-highlighted (JSON, Python, JavaScript, TypeScript).
- **Dynamic Model Search & Lock Badges**:
  - Provider model lists with >10 models render a live model search bar in Settings cards.
  - Background `ModelProber` service checks model accessibility and renders `🔒` lock badges for locked or restricted models.
- **Collapsible Sections**:
  - **AI Reasoning**: Thinking processes (e.g. from `<think>` tags) render in collapsible details blocks.
  - **Long Messages**: Messages exceeding 5 lines are collapsed by default to optimize vertical screen space.

### Code Actions

Right-click on any selected code in the editor to access the VSLLama submenu:

#### Available Actions
- **Explain This Code**: Get a step-by-step breakdown of the selection.
- **Fix This Code**: Let the AI identify and propose fixes for bugs.
- **Generate Unit Tests**: Automatically create tests for the selected function.
- **Add Documentation**: Generate Javadoc/JSDoc style comments.
- **Generate Code**: Describe what you need, and the AI will write the code.

#### Keyboard Shortcuts

| Action | Windows/Linux | macOS |
|--------|--------------|-------|
| Explain Code | `Ctrl+Shift+L` | `Cmd+Shift+L` |
| Fix Code | `Ctrl+Shift+F` | `Cmd+Shift+F` |
| Generate Tests | `Ctrl+Shift+T` | `Cmd+Shift+T` |
| Add Docs | `Ctrl+Shift+D` | `Cmd+Shift+D` |
| Generate Code | `Ctrl+Shift+G` | `Cmd+Shift+G` |

### Code Autocomplete (Inline Suggestions)

VSLLama can provide predictive, ghost-text completions as you type:

1. Open VS Code Settings (`Ctrl+,`).
2. Search for `VSLLama`.
3. Check the **Autocomplete Enabled** checkbox.
4. Start typing in your editor:
   - VSLLama waits for a short pause (default: 800ms) before showing suggestions.
   - Ghost text appears inline.
5. Press `Tab` to accept the suggestion.
6. (Optional) Manually trigger with `Alt+\`.

**Configuration**:
- `vsllama.autocompleteEnabled`: Toggle on/off
- `vsllama.autocompleteDelay`: Milliseconds to wait before showing suggestions (default: 800ms)

---

## 🧠 Chat Modes Explained

### Agent Mode
The default mode for complex tasks:
1. Analyzes your request.
2. Creates an implementation plan (if required).
3. Asks for approval before running tools or making changes.
4. Uses MCP tools to read files, search code, or run commands.
5. Applies changes with optional critique-loop verification.

### Chat Mode
Conversational assistance:
1. Direct message exchange with the AI.
2. No automated tool execution.
3. Fast answers for quick questions and brainstorming.

### Plan Mode
Architectural design and planning:
1. Generates structured implementation plans.
2. Outlines technical strategies and roadmaps.

---

## 🧬 MCP Integration (Advanced)

VSLLama supports **MCP (Model Context Protocol)** to provide the LLM with deeper context about your environment.

### Auto-Reconnect & Connection Resilience
- Connected MCP servers are monitored for transport disconnects.
- If an MCP server disconnects, VSLLama automatically attempts reconnection with exponential backoff (1s → 2s → 4s up to 5 retries).

### Configuring MCP Servers

Add MCP servers to your `settings.json`:

```json
{
  "vsllama.mcpServers": {
    "nakshastramcp": {
      "command": "nakshastramcp",
      "args": ["start", "--transport", "stdio"],
      "type": "stdio",
      "disabled": false
    }
  }
}
```

### Using MCP Tools

1. Connected tools are automatically recognized by the LLM.
2. In Agent Mode, tools are called when needed (with user approval).
3. Tool operations are categorized by type icons (📖 Read, ✏️ Write, 🚀 Exec, 🗑️ Delete).
4. Click `🔌 MCP` in the chat header to check connection status.

---

## 📋 Git Integration

### Generate Commit Messages

VSLLama generates context-aware git commit messages:

1. Stage your changes in the **Source Control** view (or leave unstaged).
2. Click the **Sparkle icon** ✨ in the Source Control header.
3. Review the generated message in the Chat Sidebar.
4. Click **Apply** to populate the VS Code Git message input box!

---

## ⚙️ Advanced Configuration

### Smart Model Routing

Set `vsllama.model` to `auto` in settings for automated model selection based on task phase:
- `vsllama.planningModel`: Model used for reasoning/planning.
- `vsllama.executionModel`: Model used for code generation/execution.

### Sliding-Window Rate Limiting

Prevent API rate limits across cloud providers:

```json
{
  "vsllama.rateLimiting": {
    "enabled": true,
    "openai": {
      "maxRequests": 50,
      "windowMs": 60000
    },
    "anthropic": {
      "maxRequests": 50,
      "windowMs": 60000
    }
  }
}
```

### AI Critique Loop

Optional post-change self-verification using your project's build and test tooling:

```json
{
  "vsllama.critiqueLoop": {
    "enabled": true,
    "maxRetries": 2
  }
}
```

---

## 🔒 Security & Audit Logging

- **Command Execution Guard**: `run_command` executes tool arguments via tokenized argv arrays (`shell: false`), preventing shell injection.
- **Error Redaction**: Sensitive Bearer tokens, API keys, and local OS paths are automatically redacted from error messages by `sanitizeErrorMessage`.
- **Workspace Confinement**: All file read/write operations strictly check path boundaries against the workspace root.
- **Audit Logging**: Structured JSON forensic logs are written to `system_events/audit.log` inside your workspace root with automated 10 MB log rotation.

---

## 🛠️ Troubleshooting

### Connection & Rate Limit Issues
1. **Ollama connection error**: Ensure Ollama is listening on `http://127.0.0.1:11434`.
2. **API Rate Limits (HTTP 429)**: Adjust `vsllama.rateLimiting` in settings.
3. **Locked Models (`🔒`)**: Models flagged with `🔒` are restricted by provider plan limits or API key permissions.
4. **Session Recovery**: Click `↩️ Undo Last Message` on error cards to revert conversation state.

### Reset Extension State
Run **VSLLama: Reset Onboarding** from the Command Palette (`Ctrl+Shift+P`) to reset onboarding and clear local state.

---

## 📞 Support & Feedback

- **Issues**: Report bugs on [GitHub Issues](https://github.com/vijaytank/vsllama-docs/issues)
- **Documentation**: [Main Repository](https://github.com/vijaytank/vsllama-docs)

---

**Happy coding with VSLLama! 🦙**
