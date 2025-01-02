# Tool Installation Guide for LibreChat MCP

This guide covers the installation of required tools for LibreChat's MCP functionality.

## UV Package Manager

UV is a fast Python package manager written in Rust, required for various MCP tools.

### Installing UV

#### Method 1: Using curl (Recommended)
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

#### Method 2: Using pip
```bash
pip install uv
```

#### Method 3: Using Homebrew (macOS)
```bash
brew install uv
```

Verify the installation:
```bash
uv --version
```

### Installing uvx

uvx is typically used for the fetch MCP server. Install it using uv:

```bash
uv pip install uvx
```

## MCP Server Components

### 1. WCGW (Terminal Tools)

WCGW requires Python 3.12 and can be installed using uv:

```bash
# Create a new virtual environment with Python 3.12
uv venv -p python3.12 .venv

# Activate the virtual environment
source .venv/bin/activate  # On Unix/macOS
# or
.venv\Scripts\activate  # On Windows

# Install wcgw
uv pip install wcgw
```

### 2. Fetch Server

The fetch server is installed using npx:

```bash
# Ensure you have Node.js installed (see installation.md for nvm setup)
npm install -g @modelcontextprotocol/server-fetch
```

### 3. Brave Search

1. First, obtain a Brave Search API key:
   - Go to [Brave Search API Dashboard](https://brave.com/search/api/)
   - Create an account or sign in
   - Generate an API key

2. Install the Brave Search server:
```bash
npm install -g @modelcontextprotocol/server-brave-search
```

## Configuration After Installation

After installing the tools, update your `librechat.yaml` configuration:

```yaml
mcpServers:
  wcgw:
    type: "stdio"
    command: "uv"
    args: ["tool", "run", "--from", "wcgw@latest", "--python", "3.12", "wcgw_mcp"]
    iconPath: "/assets/tools/terminal.svg"
  
  fetch:
    type: "stdio"
    command: "npx"
    args: ["@modelcontextprotocol/server-fetch"]
    iconPath: "/assets/tools/globe.svg"
  
  brave-search:
    type: "stdio"
    command: "npx"
    args: ["@modelcontextprotocol/server-brave-search"]
    env:
      BRAVE_API_KEY: "your-api-key-here"
```

## Troubleshooting

### UV Issues
1. **Permission Denied**
   ```bash
   sudo chown -R $USER ~/.cargo
   curl -LsSf https://astral.sh/uv/install.sh | sh
   ```

2. **Python Version Issues**
   - Ensure Python 3.12 is installed
   - Use `uv venv -p python3.12` to create environment

### Node.js Tool Issues
1. **Global Install Permission Errors**
   ```bash
   # Fix npm permissions
   mkdir ~/.npm-global
   npm config set prefix '~/.npm-global'
   # Add to ~/.profile or ~/.zshrc:
   export PATH=~/.npm-global/bin:$PATH
   ```

2. **Brave Search API Connection Issues**
   - Verify API key in configuration
   - Check network connectivity
   - Ensure no firewall blocking

### General Tips
- Always use the latest versions of tools
- Keep Python and Node.js up to date
- Check tool-specific logs for errors
- Use virtual environments to avoid conflicts