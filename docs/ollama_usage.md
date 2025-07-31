# Using Ollama with Trae Agent

Trae Agent supports Ollama out of the box through its OpenAI-compatible API integration. This guide explains how to configure and use Ollama with Trae Agent.

## Prerequisites

1. Python 3.12+
2. Ollama server running locally or accessible via network
3. Trae Agent installed (follow instructions in [README.md](README.md))

## Configuration Options

### Option 1: Environment Variables (Recommended)

Set the following environment variables:

```bash
# Ollama API key (can be any string, typically "ollama")
export OLLAMA_API_KEY="your_api_key"

# Ollama/LM Studio base URL (default is http://localhost:1234/v1 for LM Studio, http://localhost:11434/v1 for standard Ollama)
export OLLAMA_BASE_URL="http://your_ollama_server:port/v1"
```

### Option 2: Configuration File

Edit `trae_config.json` and configure the Ollama provider:

```json
{
  "default_provider": "ollama",
  "model_providers": {
    "ollama": {
      "api_key": "your_api_key",
      "base_url": "http://localhost:11434/v1",
      "model": "qwen3",  // or your preferred Ollama model
      "max_tokens": 4096,
      "temperature": 0.5,
      "top_p": 1,
      "top_k": 0,
      "max_retries": 10
    }
  }
}
```

## Usage Examples

### Basic Task Execution

```bash
# Using environment variables
export OLLAMA_API_KEY="ollama"
export OLLAMA_BASE_URL="http://localhost:11434/v1"

trae-cli run "Create a Python script to calculate Fibonacci numbers" --provider ollama --model qwen3
```

### Interactive Mode

```bash
# Using configuration file
trae-cli interactive --provider ollama --model qwen3
```

## Supported Models

Trae Agent supports tool calling with the following Ollama models:
- deepseek-r1
- qwen3
- llama3.1, llama3.2
- mistral
- qwen2.5, qwen2.5-coder
- mistral-nemo
- llama3.3
- qwq
- mistral-small
- mixtral
- smollm2
- llama4
- command-r
- hermes3
- phi4-mini
- granite3.3
- devstral
- mistral-small3.1

## Troubleshooting

1. **Connection Issues**: Ensure your Ollama server is running and accessible at the specified base URL.
2. **Model Not Found**: Verify that the model name matches what's available in your Ollama installation.
3. **API Key Errors**: The API key for Ollama can be any string (typically "ollama"), but it must match between configuration and environment variables.

## Advanced Usage

For advanced configurations, you can combine multiple providers and switch between them:

```bash
# Run with different providers
trae-cli run "Optimize this code" --provider openrouter --model "openai/gpt-4o"
trae-cli run "Generate documentation" --provider ollama --model qwen3
```

This guide provides everything you need to start using Ollama with Trae Agent effectively.