# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

App-gpty is a Python command-line wrapper for the OpenAI GPT API. It provides a simple interface to interact with GPT models from the command line, with features like system messages, itemized prompts, and various response controls.

## Development Commands

### Installation and Setup
```bash
# Install dependencies using Poetry
poetry install

# Install the package in development mode
pip install -e .
```

### Build and Distribution
```bash
# Build the package
poetry build

# Install from source
pip install git+https://github.com/tecolicom/App-gpty.git
```

### Documentation Generation
```bash
# Generate multilingual README files (requires xlate tool)
make all
# This creates README.EN-US.md, README.KO.md, README.ZH.md from README.md
```

## Architecture

### Core Structure
- `gpty/gpty.py` - Main CLI application using Typer framework
- `gpty/__init__.py` - Package initialization (minimal)
- `pyproject.toml` - Poetry configuration and dependencies

### Key Components
- **CLI Interface**: Built with Typer for type-safe command-line parsing
- **OpenAI Integration**: Uses official OpenAI Python client (v1.12.0+)
- **Message Processing**: Supports system messages, itemized prompts, and stdin input
- **Engine Aliases**: Shortcuts for common models ("3" → gpt-3.5-turbo, "4" → gpt-4o-mini)

### Dependencies
- `openai`: Official OpenAI API client
- `typer`: Modern CLI framework
- `click` & `click-spinner`: UI enhancements
- Python 3.9+ required

## Usage Patterns

The tool processes prompts in sequence:
1. System messages are added first (can be multiple)
2. Itemize option transforms subsequent prompts into bullet points
3. Stdin input supported via "-" argument
4. All prompts joined with newlines before API call

## Configuration

- API key via `OPENAI_API_KEY` environment variable or `--key` option
- Default model: gpt-4o-mini
- Default temperature: 0.5
- Default max tokens: 2000

## Release Process

1. Update `version` in `pyproject.toml`
2. Update `Changes` file
3. Update copyright year if needed (README.md → `make all` for translations)
4. Commit all changes
5. Tag and push:
   ```bash
   git push origin main
   git tag X.Y.Z
   git push origin X.Y.Z
   ```

Not published to PyPI. Installed via `pip install git+https://github.com/tecolicom/App-gpty.git`.

## Code Style Requirements

- **CRITICAL**: All text files (including source code, documentation, configuration files, etc.) MUST end with a newline character
- This applies to Python files, Markdown files, TOML files, and any other text-based files
- Files ending without a newline will cause issues with many Unix tools and should be avoided
