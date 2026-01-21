# Cerebras AI Code Assistant

An intelligent AI-powered development environment that combines conversational AI with powerful development tools, Git integration, and file operations featuring advanced fuzzy matching capabilities.

## Overview

Cerebras AI Code Assistant is an enhanced command-line interface built on top of the Cerebras AI API that serves as your intelligent coding companion. It provides seamless integration between natural language conversations and practical development tasks, making coding more intuitive and productive.

## Key Features

### 🤖 **AI-Powered Development**
- **Conversational Interface**: Interactive chat with advanced Cerebras AI models
- **Dual Model Support**: Toggle between chat model (`gpt-oss-120b`) and reasoning model (`Z.ai GLM 4.7`) (Adjust config.json to change models)
- **Function Calling**: AI can automatically execute tools and operations
- **Streaming Responses**: Real-time AI response with rich formatting

### 📁 **Intelligent File Operations**
- **Fuzzy File Matching**: Find files even with typos or partial paths
- **Smart Code Editing**: Precise code modifications with fuzzy matching for snippet replacement
- **Batch Operations**: Read and create multiple files efficiently
- **Context-Aware**: Maintains file context across conversations

### 🔧 **Shell Command Integration**
- **Cross-Platform Support**: Execute bash (Linux/macOS/WSL) and PowerShell commands
- **Git Operations**: Full Git workflow through shell commands (init, add, commit, branch, status, etc.)
- **Security Confirmation**: Prompts for approval before executing potentially dangerous commands
- **Flexible Execution**: AI can run any shell command with user oversight

### 💬 **Advanced Context Management**
- **Token-Based Estimation**: Intelligent conversation history management
- **Smart Truncation**: Preserves important context while staying within limits
- **File Context Tracking**: Manages multiple files in conversation context
- **Usage Monitoring**: Real-time context usage statistics and warnings

### 🛡️ **Security & Safety**
- **Shell Command Confirmation**: Security prompts for bash and PowerShell commands
- **Path Validation**: Robust file path sanitization and validation
- **Size Limits**: Configurable limits for file operations and content
- **Exclusion Patterns**: Smart filtering of system and temporary files

## Installation

### Prerequisites
- Python 3.8+
- Cerebras AI API key

### Setup

1. **Clone the repository**:
   ```bash
   git clone https://github.com/fabiopauli/cerebras-assistant.git
   cd cerebras
   ```

2. **Install required dependencies**:
   Using uv (recommended - faster)
   ```bash
   uv venv
   uv pip install -r requirements.txt
   uv run main.py
   ```
   
   ```bash
   pip install -r requirements.txt
   ```

3. **Install optional dependencies for enhanced fuzzy matching**:
   ```bash
   pip install thefuzz python-levenshtein
   ```

4. **Set up environment variables**:
   Create a `.env` file or set the environment variable:
   
   ```bash
   # Create .env file
   echo "CEREBRAS_API_KEY=your-cerebras-api-key-here" > .env
   ```
   Or
   ```bash
   export CEREBRAS_API_KEY="your-cerebras-api-key-here"
   ```

5. **Run the assistant**:
   ```bash
   python main.py
   ```
   

## Usage

### Command-Line Interface

The assistant supports both natural language conversation and special commands:

#### **Special Commands**

**General Commands:**
- `/help` - Show all available commands and their descriptions
- `/r` - Call Reasoner model for one-off reasoning tasks
- `/reasoner` - Toggle between chat and reasoner models
- `/markdown` - Toggle markdown rendering for AI responses
- `/clear` - Clear the console screen
- `/clear-context` - Reset conversation context
- `/context` - Show current context usage statistics
- `/os` - Show operating system information
- `/exit` or `/quit` - Exit the application

**Directory & File Management:**
- `/folder` - Show current base directory
- `/folder <path>` - Set base directory for file operations
- `/folder reset` - Reset base directory to current working directory
- `/add <path>` - Add file/dir to conversation context (supports fuzzy matching)

#### **Example Workflows**

**Adding files to context:**
```bash
/add src/main.py
/add src/  # Add entire directory
/add mai.py  # Fuzzy matching will find main.py
```

**Git workflow:**
```bash
# Use bash commands through the AI assistant
git init
git add .
git commit "Initial commit with source files"
git branch feature/new-feature
git status
```

**File operations through conversation:**
```
User: "Create a new Python function that calculates Fibonacci numbers"
Assistant: [Creates the file with the function]

User: "Now modify the function to use memoization"
Assistant: [Edits the existing function using fuzzy matching]
```

### AI Tool Integration

The assistant can automatically execute these operations through function calls:

1. **File Operations**: `read_file`, `create_file`, `edit_file`, `read_multiple_files`, `create_multiple_files`
2. **System Operations**: `run_bash`, `run_powershell` (with security confirmation for shell commands)

**Note:** Git operations are performed through bash/PowerShell commands (e.g., `git add .`, `git commit`, `git status`) rather than dedicated Git functions.

## Configuration

### AI Models

The assistant supports dual-model architecture:

- **Chat Model (`gpt-oss-120b`)**: Optimized for conversational interactions and general coding tasks
- **Reasoning Model (`Z.ai GLM 4.7`)**: Enhanced reasoning capabilities for complex problem-solving

You can toggle between models using `/reasoner` command or make a one-off reasoning call with `/r`.

**Model Configuration** (in `config.json`):
```json
{
  "models": {
    "default_model": "gpt-oss-120b",
    "reasoner_model": "zai-glm-4.7"
  }
}
```

### Fuzzy Matching Thresholds
- **File Path Matching**: 80% similarity minimum
- **Code Edit Matching**: 85% similarity minimum

### Context Limits
- **Maximum History**: 50 messages
- **Context Files**: 5 files maximum
- **Token Estimation**: ~60,000 tokens context window (Z.ai GLM 4.7)

## Project Structure

```bash
cerebras/
├── main.py             # Main application script
├── config.py           # Configuration and constants
├── utils.py            # Utility functions
├── system_prompt.txt   # System prompt configuration
├── README.md           # This documentation
├── pyproject.toml      # Project configuration
├── uv.lock             # UV lock file
└── .env                # Environment variables (create this)
```

## Advanced Features

### Fuzzy Matching
The assistant uses advanced fuzzy matching for:
- **File Path Resolution**: Find files even with typos (`mai.py` → `main.py`)
- **Code Snippet Matching**: Edit code even if the exact snippet has minor differences
- **Directory Navigation**: Smart directory and file discovery

### Context Management
- **Intelligent Truncation**: Automatically manages conversation history
- **File Priority**: Keeps most recently accessed files in context
- **Token Estimation**: Provides real-time context usage feedback
- **Memory Optimization**: Efficient handling of large codebases

### Security Features
- **Command Validation**: Confirms potentially dangerous operations
- **Path Sanitization**: Prevents directory traversal attacks
- **File Type Filtering**: Excludes binary and system files automatically
- **Size Limitations**: Prevents memory exhaustion from large files

## Dependencies

### Required
- `cerebras-cloud-sdk` - Cerebras AI API client
- `rich` - Enhanced console output and formatting
- `prompt_toolkit` - Interactive command-line interface
- `pydantic` - Data validation and settings management
- `python-dotenv` - Environment variable management

### Optional
- `thefuzz` - Fuzzy string matching capabilities
- `python-levenshtein` - Performance optimization for fuzzy matching

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Support

If you encounter any issues or have questions, please:
1. Check the `/help` command within the application
2. Review this documentation
3. Open an issue on the project repository

---

**Powered by Cerebras AI Models, including Z.ai GLM 4.7**