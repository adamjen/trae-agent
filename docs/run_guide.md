# Running Trae Agent

## Prerequisites

1. Python 3.12+
2. Project installed (follow instructions in README.md)
3. trae_config.json configured with your preferred LLM provider settings

## Basic Usage

### Run a Simple Task

```bash
trae-cli run "Create a hello world Python script"
```

### With Specific Provider and Model

```bash
# Using OpenAI
trae-cli run "Fix the bug in main.py" --provider openai --model gpt-4o

# Using Ollama
trae-cli run "Optimize this code" --provider ollama --model qwen3
```

## Interactive Mode

Start an interactive session where you can run multiple tasks:

```bash
# Basic interactive mode
trae-cli interactive

# With custom configuration
trae-cli interactive --provider ollama --model qwen3 --max-steps 30
```

In interactive mode, you can:
- Type any task description to execute it
- Use `status` to see agent information
- Use `help` for available commands
- Use `clear` to clear the screen
- Use `exit` or `quit` to end the session

## Environment Variables

You can set environment variables for API keys and base URLs:

```bash
# For OpenAI
export OPENAI_API_KEY="your-openai-api-key"

# For Ollama
export OLLAMA_API_KEY="ollama"
export OLLAMA_BASE_URL="http://your-ollama-server:port/v1"

# For other providers (see README for full list)
```

## Common Commands

### Show Configuration

```bash
trae-cli show-config
```

### Run with Custom Working Directory

```bash
trae-cli run "Add unit tests for the utils module" --working-dir /path/to/project
```

### Save Trajectory for Debugging

```bash
trae-cli run "Refactor the database module" --trajectory-file debug_session.json
```

## Troubleshooting

1. **Import Errors**: Try setting PYTHONPATH
   ```bash
   PYTHONPATH=. trae-cli run "your task"
   ```

2. **API Key Issues**: Verify your API keys are set
   ```bash
   echo $OPENAI_API_KEY
   echo $OLLAMA_API_KEY
   trae-cli show-config
   ```

3. **Permission Errors**: Ensure proper permissions for file operations
   ```bash
   chmod +x /path/to/your/project
   ```

4. **Command not found**: Try using uv if needed
   ```bash
   uv run trae-cli "your task"