# LibreChat MCP Protocol Documentation

This repository contains comprehensive documentation for setting up and using LibreChat with Anthropic's MCP (Mission Control Protocol). The MCP protocol enables enhanced functionality and better control over Claude interactions through LibreChat.

## Quick Links

- [Installation Guide](installation.md) - Complete guide for installing LibreChat with npm and nvm
- [Tool Installation Guide](tool-installation.md) - Instructions for installing all required MCP tools
- [MCP Configuration Guide](mcp-configuration.md) - How to configure LibreChat for MCP functionality

## Table of Contents

### 1. Getting Started
- [System Requirements](#system-requirements)
- [Quick Start Guide](#quick-start-guide)

### 2. Installation
- [Node.js Setup with NVM](installation.md#node-js-setup-with-nvm)
- [LibreChat Installation](installation.md#installation-steps)
- [MongoDB Setup Options](installation.md#mongodb-setup-options)
  - [Local Installation](installation.md#option-1-local-mongodb-installation)
  - [Cloud Hosted (MongoDB Atlas)](installation.md#option-2-mongodb-atlas-cloud-hosted)

### 3. MCP Tools Setup
- [UV Package Manager](tool-installation.md#uv-package-manager)
- [WCGW Terminal Tools](tool-installation.md#1-wcgw-terminal-tools)
- [Fetch Server](tool-installation.md#2-fetch-server)
- [Brave Search](tool-installation.md#3-brave-search)

### 4. Configuration
- [MCP Server Configuration](mcp-configuration.md#mcp-servers-configuration)
- [Anthropic Setup](mcp-configuration.md#anthropic-configuration)
- [Security Settings](mcp-configuration.md#security-considerations)

### 5. Creating MCP Agents
- [Agent Builder Guide](creating-mcp-agents.md)
- [Best Practices](creating-mcp-agents.md#best-practices)
- [Example Instructions](creating-mcp-agents.md#example-instructions)
- [Testing and Maintenance](creating-mcp-agents.md#testing-your-agent)

### 6. Troubleshooting
- [MongoDB Issues](installation.md#mongodb-issues)
- [Node.js and NVM Issues](installation.md#nodejs-and-nvm-issues)
- [Tool-Specific Issues](tool-installation.md#troubleshooting)

## Quick Start Guide

1. **Install Prerequisites**
   ```bash
   # Install NVM
   curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
   # Install Node.js
   nvm install --lts
   # Install UV
   curl -LsSf https://astral.sh/uv/install.sh | sh
   ```

2. **Clone and Install LibreChat**
   ```bash
   git clone https://github.com/danny-avila/LibreChat.git
   cd LibreChat
   npm install
   ```

3. **Install MCP Tools**
   ```bash
   # Install WCGW
   uv pip install wcgw
   # Install Fetch Server
   npm install -g @modelcontextprotocol/server-fetch
   # Install Brave Search
   npm install -g @modelcontextprotocol/server-brave-search
   ```

4. **Configure LibreChat**
   - Set up MongoDB ([local](installation.md#option-1-local-mongodb-installation) or [cloud](installation.md#option-2-mongodb-atlas-cloud-hosted))
   - Configure [MCP servers](mcp-configuration.md#mcp-servers-configuration)
   - Set up [Anthropic integration](mcp-configuration.md#anthropic-configuration)

5. **Start LibreChat**
   ```bash
   npm run start
   ```

## System Requirements

- Operating System: Linux, macOS, or Windows
- Node.js: LTS version (via nvm)
- Python: 3.12 (for WCGW)
- MongoDB: 4.4 or higher
- Storage: 1GB minimum for base installation
- Memory: 2GB RAM minimum recommended

## Security Notes

- Never commit API keys or sensitive credentials
- Use environment variables for secrets
- Keep all tools and dependencies updated
- Follow security best practices for MongoDB setup
- Regularly backup your configuration and data

## Contributing

Feel free to submit issues and enhancement requests. We welcome your contributions to improve the documentation.

## License

This documentation is released under the MIT License. See the LICENSE file for details.