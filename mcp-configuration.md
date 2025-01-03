# LibreChat MCP Configuration Guide

This guide explains how to configure LibreChat to work with Anthropic's MCP (Mission Control Protocol) and additional MCP servers.

## Configuration Files

LibreChat's MCP configuration is split across two main files:
- `librechat.yaml`: Main configuration file
- `.env`: Environment variables

## MCP Servers Configuration

The MCP servers are configured in `librechat.yaml` under the `mcpServers` section. Here's how to set up different MCP servers:

### Example Configuration

Here's a complete example of the MCP servers configuration:

```yaml
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
  
  brave-search:
    type: "stdio"
    command: "sh"
    args: ["-c", "export BRAVE_API_KEY=\"your-api-key\" && npx @modelcontextprotocol/server-brave-search"]
```

Notes:
1. Replace paths like `/opt/homebrew/bin/` with your system's paths
2. Install required tools:
   - `uv pip install wcgw`
   - `uv pip install uvx`
   - `npm install -g @modelcontextprotocol/server-brave-search`
3. Get a Brave Search API key from their [API dashboard](https://brave.com/search/api/)

## Required Configuration

Your `librechat.yaml` needs these essential configurations:

```yaml
# Enable Agent Builder
endpoints:
  agents:
    disableBuilder: false

# Anthropic Configuration
endpoints:
  anthropic:
    models:
      default: ["claude-3-5-sonnet-20241022"]
    modelDisplayLabel: "Claude"
    capabilities: ["tools", "actions"]
    agentMode: true
```

And in `.env`:

```env
ENDPOINTS=anthropic,agents

# Enable agent toolbar in interface
interface:
  agentToolbar: true
```

## Important Notes

1. **API Keys**: Never commit API keys to version control. Use environment variables or secure key management.
2. **Paths**: Adjust paths (`command` and `args`) according to your system setup.
3. **Permissions**: Ensure proper permissions for executing the MCP server commands.
4. **Dependencies**: Install required packages (uv, uvx) before configuring MCP servers.

## Security Considerations

1. Keep your `.env` file secure and never commit it to version control
2. Use environment-specific configuration for different deployments
3. Regularly rotate API keys and access tokens
4. Limit permissions to only what's necessary for each MCP server

## Troubleshooting

1. Check command paths using `which [command]`
2. Verify API keys are correctly set
3. Check server logs for execution errors
4. Ensure all required dependencies are installed