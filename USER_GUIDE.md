# VSLLama User Guide

Welcome to **VSLLama**, your privacy-first AI coding companion powered by local LLMs and MCP (Model Context Protocol).

## 🚀 Getting Started

### 1. Prerequisites
- **VS Code**: Version 1.109.0 or higher
- **AI Provider**: You can use:
  - **Local**: [Ollama](https://ollama.ai/) running at `http://localhost:11434`
  - **Cloud**: API keys for OpenAI, Anthropic, Gemini, NVIDIA NIM, Perplexity, or Ollama Cloud

### 2. Setting Up the AI Provider

1. Open the **VSLLama Chat Sidebar** (Llama icon in the Activity Bar)
2. Click the **Environment** tab
3. Select your desired AI Provider from the dropdown:
   - `ollama` (local)
   - `openai`
   - `anthropic`
   - `gemini`
   - `nvidianim`
   - `perplexity`
   - `ollamacloud`
   - `llamacpp`
4. If using a cloud provider, enter your **API Key** and click **Save**
   - Keys are securely stored in VS Code's `SecretStorage`
5. (Optional) Specify custom Base URLs in your VS Code settings (e.g., `vsllama.openaiUrl`)

### 3. Selecting Your Default Mode

Choose your preferred chat mode in the **Environment** tab:

- **Agent Mode** (default): Autonomous task execution with MCP tool support. The AI creates implementation plans and requests approval before executing tools.
- **Chat Mode**: Traditional conversational interaction without tool execution.
- **Plan Mode**: Generate structured architectural plans and implementation strategies.

---

## 🛠️ Usage

### Sidebar Chat

1. Click the **VSLLama icon** (Llama silhouette) in the Activity Bar
2. Type your message in the chat box
3. Use the **Environment** tab to:
   - Switch AI providers or models
   - Change chat modes (Agent, Chat, Plan)
   - Manage API keys
   - Configure model selection (Smart Routing)

### Understanding the Chat Interface

The chat view includes visual enhancements for better interaction:

**Collapsible Sections**:
- **AI Reasoning**: When the AI shows `<think>` tags (reasoning process), they appear in collapsible details blocks. Click to expand/collapse.
- **Tool Calls**: System tool calls and their results are grouped in expandable sections. This helps you debug and understand what the AI did.
- **Long Messages**: Messages exceeding 5 lines are collapsed by default to save screen space. Click to expand.

**Status Indicators**:
- **Pulsing Dot**: Shows the AI's current status: "starting", "thinking", "generating", "executing tools", or "resuming"
- Real-time feedback on what the extension is doing

**Layout Optimizations**:
- Word-wrap enabled for better code block readability
- High-contrast scrollbars optimized for dark/light themes
- Responsive design for all VS Code window sizes

### Code Actions

Right-click on any selected code in the editor to access the VSLLama submenu:

#### Available Actions
- **Explain This Code**: Get a step-by-step breakdown of the selection
- **Fix This Code**: Let the AI identify and propose fixes for bugs
- **Generate Unit Tests**: Automatically create tests for the selected function
- **Add Documentation**: Generate Javadoc/JSDoc style comments
- **Generate Code**: Describe what you need, and the AI will write the code

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

1. Open VS Code Settings (`Ctrl+,`)
2. Search for `VSLLama`
3. Check the **Autocomplete Enabled** checkbox
4. Start typing in your editor
   - VSLLama waits for a short pause (default: 800ms) before showing suggestions
   - Ghost text appears in a lighter color
5. Press `Tab` to accept the suggestion
6. (Optional) Manually trigger with `Alt+\`

**Configuration**:
- `vsllama.autocompleteEnabled`: Toggle on/off
- `vsllama.autocompleteDelay`: Milliseconds to wait before showing suggestions (default: 800ms)

---

## 🧠 Chat Modes Explained

### Agent Mode
The default mode for most use cases. The AI:
1. Analyzes your request
2. Creates an implementation plan (if complex)
3. Asks for your approval before executing tools or making changes
4. Uses MCP tools to read files, search code, or execute commands
5. Applies the agreed-upon changes with verification

**Best for**: Complex tasks, code generation, refactoring, debugging.

### Chat Mode
Traditional conversational interaction:
1. Exchange messages with the AI
2. No automatic tool execution
3. No implementation plans
4. Direct responses without approval steps

**Best for**: Quick questions, learning, brainstorming, explanations.

### Plan Mode
Specialized for architectural planning:
1. Generate structured implementation plans
2. Outline technical strategies
3. Create roadmaps and design documents

**Best for**: Architecture decisions, project planning, high-level design discussions.

---

## 🧬 MCP Integration (Advanced)

VSLLama supports **MCP (Model Context Protocol)** to provide the LLM with deeper context about your environment.

### What is MCP?

MCP is a protocol that allows the LLM to interact with tools and data sources:
- Read and understand your codebase
- Run commands or custom scripts
- Access external data sources
- Execute complex tasks autonomously

### Configuring MCP Servers

You can add MCP servers in your VS Code `settings.json`:

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

**Example MCP Server**: [NakshAstraMCP](https://github.com/vijaytank/NakshAstraMCP-Docs)
- Provides deep code analysis and context
- Available for installation as a standalone package

### Using MCP Tools

Once an MCP server is connected:
1. The LLM automatically detects available tools
2. When relevant to your request, tools are used automatically (in Agent Mode)
3. You'll see tool calls and results in collapsible sections in the chat
4. Check the **MCP Tools** tab to see connection status

**Server Status**:
- Open the **MCP Tools** section in the chat sidebar
- Green dot = Connected and ready
- Red dot = Connection failed
- Check your MCP server configuration if issues occur

---

## 📋 Git Integration

### Generate Commit Messages

VSLLama helps you write better, context-aware commit messages:

1. Stage your changes in the **Source Control** view (or leave them unstaged to analyze working tree changes)
2. Click the **Sparkle icon** ✨ in the Source Control header
3. VSLLama generates a commit message based on your changes
4. Review the message in the Chat Sidebar
5. Click **Apply** to populate your VS Code Git message input box
6. (Optional) Edit and refine the message
7. Commit as usual with `Ctrl+Enter` or the commit button

---

## ⚙️ Advanced Configuration

### Smart Model Routing

Enable automatic model selection for optimal performance:

1. In Settings, set `vsllama.model` to `auto`
2. Optionally specify separate models:
   - `vsllama.planningModel`: For planning/reasoning (e.g., Claude 3 Opus)
   - `vsllama.executionModel`: For execution/coding (e.g., Claude 3 Sonnet)

The extension automatically switches models based on the task phase.

### Rate Limiting

Prevent API rate limits from interrupting your workflow:

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

- `enabled`: Global toggle (default: `true`)
- `maxRequests`: Maximum requests allowed in the window
- `windowMs`: Time window in milliseconds (e.g., `60000` = 1 minute)

### AI Critique Loop

Optional self-verification of code changes using your project's build system:

```json
{
  "vsllama.critiqueLoop": {
    "enabled": true,
    "maxRetries": 2
  }
}
```

- `enabled`: Enable post-change verification (default: `true`)
- `maxRetries`: Auto-correction attempts (default: `2`)

When enabled, VSLLama:
1. Makes the proposed changes
2. Runs your project's build/test system
3. Detects any errors
4. Automatically corrects issues if possible
5. Verifies the fix

---

## 🛠️ Troubleshooting

### Extension Won't Connect to Ollama

**Problem**: "Unable to connect to Ollama"

**Solutions**:
1. Verify Ollama is running:
   ```bash
   curl http://localhost:11434/api/tags
   ```
2. Check your firewall/networking settings
3. Verify the correct Ollama URL in `vsllama.ollamaUrl`
4. Try reloading VS Code: `Ctrl+R` (Windows/Linux) or `Cmd+R` (macOS)

### API Rate Limits (HTTP 429)

**Problem**: "Rate limit exceeded" errors from OpenAI, Anthropic, etc.

**Solutions**:
1. Enable and adjust `vsllama.rateLimiting` settings
2. Increase `windowMs` (e.g., from `60000` to `120000`)
3. Decrease `maxRequests` to reduce frequency
4. Wait for the window to reset before retrying

### MCP Server Connection Failed

**Problem**: "Failed to connect to MCP server"

**Solutions**:
1. Verify the MCP server is installed and executable
2. Check the command and args in your settings
3. Review the **MCP Tools** section for status details
4. Try manually running the MCP command to test it
5. Check your workspace path is correct

### Streaming Connection Errors

**Problem**: "Connection lost", "Network timeout"

**Solutions**:
1. Extension automatically retries failed connections
2. Check your internet connection stability
3. Verify API endpoint URLs are correct in settings
4. Review detailed error messages in the **Environment** tab

### Long Response Times

**Problem**: Responses are slow or seem stuck

**Solutions**:
1. Check the pulsing indicator status:
   - "thinking" = AI is processing
   - "generating" = AI is streaming response
   - "executing tools" = AI is running MCP tools
2. Verify your network connection
3. Try a simpler, more focused request
4. Check if API is down (visit provider's status page)

### Reset the Extension

If you encounter persistent issues:

1. Press `Ctrl+Shift+P` (or `Cmd+Shift+P` on macOS)
2. Search for and run: **VSLLama: Reset Onboarding**
3. This clears cache and resets settings to defaults

### Get Better Error Details

Enable more verbose error information:

1. Open VS Code Settings
2. Search for `VSLLama` debug or logging options
3. Review the Output panel: View → Output → Select "VSLLama" from dropdown

---

## 📞 Support & Feedback

- **Issues**: Report bugs on [GitHub Issues](https://github.com/vijaytank/vsllama/issues)
- **Discussions**: Join the community on [GitHub Discussions](https://github.com/vijaytank/vsllama/discussions)
- **Documentation**: Check the [main repository](https://github.com/vijaytank/vsllama)

---

**Happy coding with VSLLama! 🦙**
