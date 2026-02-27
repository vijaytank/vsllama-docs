# VSLLama

A privacy-first VS Code extension that connects to local Ollama and cloud AI providers (OpenAI, Anthropic, Gemini) for chat and coding help.  
MCP integration is optional (can be enabled/disabled).

## Features (current)
- Sidebar chat view
- Stream responses from Ollama
- Extension ↔ webview messaging (ping/pong)
- MCP Tool Integration (Phase 1 complete)
- Code Autocomplete (Inline Ghost Text)
- Smart Git Commit Message Generation

## Requirements
- VS Code
- An active AI provider (e.g. Ollama running locally at http://localhost:11434, or an API Key for OpenAI, Anthropic, or Gemini)

## Usage
- **Chat**: Open the VSLLama view in the Activity Bar to start chatting with your local models.
- **Code Actions**: Highlight code and right-click to access "Explain", "Fix", and "Generate" tools.
- **Git Commits**: Generate context-aware commit messages from the Source Control view (evaluates both staged and unstaged changes).
- **Code Autocomplete**: Get AI-powered inline code suggestions as you type (requires enabling in settings).

For detailed instructions, see the [User Guide](USER_GUIDE.md).

## Install (VSIX)
1. Download the `.vsix` from the [Latest Release](https://github.com/vijaytank/vsllama/releases).
2. In VS Code: Extensions → `...` → **Install from VSIX...**

## Configuration
Access settings (`Ctrl+,`) and search for `VSLLama` to configure:
- `provider`: AI Provider to use (`ollama`, `openai`, `anthropic`, `gemini`).
- `ollamaUrl`, `openaiUrl`, `anthropicUrl`, `geminiUrl`: Provider API Base URLs.
- `model`: Default LLM to use.
- `mcpServers`: Definitions for MCP tool servers.
- `autocompleteEnabled`: Toggle inline ghost text code completions.
- `autocompleteDelay`: Milliseconds to wait before triggering autocomplete (default: 800ms).

*Note: You can easily switch providers and set API Keys directly from the Environment tab in the VSLLama chat view.*

## Development
- `npm install`
- Press `F5` to start the Extension Development Host


## Roadmap
- Add “Use selection” and “Apply edits”
- Interactive MCP Tool confirmation UI
- Enhanced local context with RAG integration

