# Getting Started with LibreChat MCP

Follow these steps to set up LibreChat with MCP support.

## 1. Basic Setup

```bash
# Install NVM (Node Version Manager)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
source ~/.bashrc  # or ~/.zshrc

# Install Node.js
nvm install --lts
nvm use --lts

# Install UV (Python Package Manager)
curl -LsSf https://astral.sh/uv/install.sh | sh
```

## 2. Install LibreChat

```bash
# Clone and install
git clone https://github.com/danny-avila/LibreChat.git
cd LibreChat
npm install
cp .env.example .env
```

## 3. Set Up MongoDB

Choose one:

### Local MongoDB
```bash
# macOS
brew tap mongodb/brew
brew install mongodb-community
brew services start mongodb-community

# Add to .env:
MONGO_URI=mongodb://localhost:27017/librechat
```

### Cloud MongoDB (Atlas)
1. Create account at [MongoDB Atlas](https://account.mongodb.com/account/register)
2. Create free cluster
3. Add connection string to `.env`

## 4. Install MCP Tools

```bash
# WCGW for terminal access
uv pip install wcgw

# uvx for web access (Fetch)
uv pip install uvx

# Brave Search (optional)
npm install -g @modelcontextprotocol/server-brave-search
```

## 5. Configure LibreChat

Create/edit `librechat.yaml`:

```yaml
# Enable Agent Builder and MCP
endpoints:
  agents:
    disableBuilder: false
  anthropic:
    models:
      default: ["claude-3-5-sonnet-20241022"]
    modelDisplayLabel: "Claude"
    capabilities: ["tools", "actions"]
    agentMode: true

# Configure MCP servers
mcpServers:
  wcgw:
    type: "stdio"
    command: "/opt/homebrew/bin/uv"
    args: ["tool", "run", "--from", "wcgw@latest", "--python", "3.12", "wcgw_mcp"]
    iconPath: "/assets/tools/terminal.svg"
  
  fetch:
    type: "stdio"
    command: "/opt/homebrew/bin/uvx"
    args: ["mcp-server-fetch"]
    iconPath: "/assets/tools/globe.svg"
```

## 6. Start LibreChat

```bash
npm run start
```

Visit http://localhost:3080 and create your first MCP agent!

## Next Steps

- [Create Your First Agent](creating-mcp-agents.md)
- [Detailed Configuration Options](mcp-configuration.md)
- [Tool Installation Details](tool-installation.md)

## Common Issues

1. **NVM not found**: Restart terminal or source profile
2. **MongoDB connection failed**: Check service is running
3. **Tool not found**: Verify installations in PATH
4. **Agent Builder not showing**: Check `disableBuilder: false` in config