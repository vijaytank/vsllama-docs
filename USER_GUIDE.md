# VSLLama User Guide

Welcome to **VSLLama**, your privacy-first AI coding companion powered by local LLMs and MCP (Model Context Protocol).

## 🚀 Getting Started

### 1. Prerequisites
- **VS Code**: Version 1.109.0 or higher.
- **AI Provider**: You can use a local LLM via [Ollama](https://ollama.ai/), or connect to cloud providers (OpenAI, Anthropic, Gemini) using your API keys.

### 2. Setting Up the AI Provider
1. Open the **VSLLama Chat Sidebar**.
2. Click the **Environment** tab.
3. Select your desired AI Provider from the dropdown (Ollama, OpenAI, Anthropic, or Gemini).
4. If using a cloud provider, enter your **API Key** and click **Save**. The key is securely stored in VS Code's `SecretStorage`.
5. You can also specify custom Base URLs directly in your VS Code settings (e.g., `vsllama.openaiUrl`).

---

## 🛠️ Usage

### Sidebar Chat
1. Click the **VSLLama icon** (Llama silhouette) in the Activity Bar.
2. Type your message in the chat box.
3. Use the **Environment** tab to switch models or manage API keys.

### Code Actions
Right-click on any selected code in the editor to access the VSLLama submenu:
- **Explain This Code**: Get a step-by-step breakdown of the selection.
- **Fix This Code**: Let the AI identify and propose fixes for bugs.
- **Generate Unit Tests**: Automatically create tests for the selected function.
- **Add Documentation**: Generate Javadoc/JSDoc style comments.
- **Generate Code**: Describe what you need, and the AI will write the code.

**Keyboard Shortcuts:**
- `Ctrl+Shift+L`: Explain Code
- `Ctrl+Shift+F`: Fix Code
- `Ctrl+Shift+T`: Generate Tests
- `Ctrl+Shift+D`: Add Docs
- `Ctrl+Shift+G`: Generate Code

### Code Autocomplete (Inline Suggestions)
VSLLama can provide predictive, ghost-text completions as you type. To use this:
1. Open your VS Code Settings (`Ctrl+,`).
2. Search for `VSLLama` and check the **Autocomplete Enabled** box.
3. Start typing in your editor. VSLLama will wait for a short pause (default: 800ms) and present ghost text. You can also manually trigger completion at any time using `Alt+\`.
4. Press `Tab` to accept the suggestion.

---

## 🧬 MCP Integration (Advanced)

VSLLama supports **MCP (Model Context Protocol)** to provide the LLM with deeper context about your environment.

### Configuring MCP Servers
You can add MCP servers in your `settings.json`:

```json
"vsllama.mcpServers": {
  "my-local-server": {
    "command": "python",
    "args": ["path/to/server.py"]
  }
}
```

### Using Tools
If a connected MCP server provides tools, the LLM will automatically attempt to use them when relevant to your request. You can see the status of connected MCP servers in the **MCP Tools** section of the sidebar.

---

## 📋 Git Integration
VSLLama can help you write better commit messages based on your local changes.
1. Stage your changes in the Source Control view (or leave them unstaged if you prefer evaluating working tree changes).
2. Click the **Sparkle icon** in the Source Control header.
3. Review the generated message in the Chat Sidebar. 
4. Click **Apply** to automatically populate your VS Code Git message input box!
