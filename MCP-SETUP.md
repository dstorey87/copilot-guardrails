# MCP Server Setup Guide

> **Complete guide to configuring Model Context Protocol (MCP) servers for GitHub Copilot**

**Last Updated**: October 2025  
**Copilot Version**: VS Code with MCP support (Generally Available)

## What is MCP?

Model Context Protocol (MCP) is a standardized way for AI applications to interact with external data sources and tools. For GitHub Copilot, MCP servers provide:

- 🌐 **Web search** - Current best practices and documentation
- 📚 **Library docs** - Up-to-date official documentation
- 🐞 **GitHub integration** - Repository management and code search
- 🎭 **Browser automation** - E2E testing with Playwright
- ☁️ **Cloud services** - Azure, AWS, GCP integration

## Prerequisites

### Required

- ✅ VS Code version 1.85 or later
- ✅ GitHub Copilot extension (latest version)
- ✅ GitHub Copilot subscription (Individual, Business, or Enterprise)
- ✅ Node.js 18+ or Python 3.10+ (depending on servers)

### Optional but Recommended

- GitHub account with appropriate permissions
- npm or pip for installing MCP servers

## Quick Setup

### Step 1: Enable MCP in Copilot

1. Open VS Code
2. Open Settings (Ctrl+, or Cmd+,)
3. Search for "Copilot MCP"
4. Enable "GitHub Copilot > MCP: Enabled"

### Step 2: Configure MCP Servers

MCP servers are configured in your VS Code `settings.json` file.

Open settings.json:

- Press `Ctrl+Shift+P` (Cmd+Shift+P on Mac)
- Type "Preferences: Open User Settings (JSON)"
- Press Enter

## Essential MCP Servers

### 1. GitHub MCP Server (HIGHEST PRIORITY)

**What it does**: Official GitHub integration for repo management, code search, PR operations.

**Why you need it**: Core functionality for the guardrails system.

#### Installation

```bash
# Using npm
npm install -g @modelcontextprotocol/server-github

# Or using npx (no installation needed)
npx @modelcontextprotocol/server-github
```

#### Configuration

Add to `settings.json`:

```json
{
  "github.copilot.chat.mcp.enabled": true,
  "github.copilot.chat.mcp.servers": {
    "github": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-github"
      ],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "${env:GITHUB_TOKEN}"
      }
    }
  }
}
```

#### Get GitHub Token

1. Go to <https://github.com/settings/tokens>
2. Click "Generate new token (classic)"
3. Select scopes:
   - `repo` (full control of private repositories)
   - `read:org` (read org data)
   - `workflow` (update GitHub Actions)
4. Generate and copy token
5. Set environment variable:

**Windows (PowerShell)**:

```powershell
[System.Environment]::SetEnvironmentVariable('GITHUB_TOKEN', 'your-token-here', 'User')
```

**macOS/Linux**:

```bash
echo 'export GITHUB_TOKEN="your-token-here"' >> ~/.zshrc
# or ~/.bashrc depending on your shell
source ~/.zshrc
```

### 2. Web Search MCP

**What it does**: Enables Copilot to search the web for current information.

**Why you need it**: Research-first mandate requires current best practices.

**Note**: This is built into GitHub Copilot by default when enabled via workspace settings.

#### Enable Web Search

In your workspace `.vscode/settings.json`:

```json
{
  "github.copilot.chat.webSearch.enabled": true
}
```

That's it! Copilot can now search the web when you use the `#websearch` keyword.

### 3. Playwright MCP (Community - ExecuteAutomation)

**What it does**: Browser automation for E2E testing.

**Why you need it**: Testing guardrails require E2E tests.

**Note**: As of October 2025, the official `@microsoft/playwright-mcp` package does not exist. We use the community-maintained `@executeautomation/playwright-mcp-server` instead.

#### Installation

```bash
npm install -g @executeautomation/playwright-mcp-server
```

#### Configuration

Add to `settings.json`:

```json
{
  "github.copilot.chat.mcp.servers": {
    "playwright": {
      "command": "npx",
      "args": [
        "-y",
        "@executeautomation/playwright-mcp-server"
      ]
    }
  }
}
```

### 4. Context7/Upstash MCP

**What it does**: Provides up-to-date library and framework documentation.

**Why you need it**: Research requires official documentation access.

#### Installation

```bash
npm install -g @upstash/context7-mcp
```

#### Configuration

Add to `settings.json`:

```json
{
  "github.copilot.chat.mcp.servers": {
    "context7": {
      "command": "npx",
      "args": [
        "-y",
        "@upstash/context7-mcp"
      ]
    }
  }
}
```

### 5. Microsoft Learn MCP (Remote HTTP Server)

**What it does**: Access to Microsoft documentation (Azure, .NET, VS Code API).

**Why you need it**: If working with Microsoft technologies.

**Note**: Microsoft Learn MCP Server is a remote HTTP-based server, not an npm package. It uses the `mcp-remote` package to connect.

#### Installation

No installation required! Uses the remote endpoint at `https://learn.microsoft.com/api/mcp`

#### Configuration

Add to `settings.json`:

```json
{
  "github.copilot.chat.mcp.servers": {
    "mslearn": {
      "command": "npx",
      "args": [
        "-y",
        "mcp-remote",
        "https://learn.microsoft.com/api/mcp"
      ]
    }
  }
}
```

## Complete Configuration Example

Here's a complete `settings.json` with all essential servers (verified October 2025):

```json
{
  "github.copilot.chat.mcp.enabled": true,
  "github.copilot.chat.webSearch.enabled": true,
  "github.copilot.chat.mcp.servers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "${env:GITHUB_TOKEN}"
      }
    },
    "playwright": {
      "command": "npx",
      "args": ["-y", "@executeautomation/playwright-mcp-server"]
    },
    "context7": {
      "command": "npx",
      "args": ["-y", "@upstash/context7-mcp"]
    },
    "mslearn": {
      "command": "npx",
      "args": [
        "-y",
        "mcp-remote",
        "https://learn.microsoft.com/api/mcp"
      ]
    }
  }
}
```

## Verification

### Test Your Setup

1. **Open GitHub Copilot Chat** (Ctrl+Alt+I or Cmd+Alt+I)

2. **Test Web Search**:

   ```
   @workspace #websearch React Server Components best practices October 2025
   ```

   You should see search results.

3. **Test GitHub MCP**:

   ```
   @workspace List my repositories
   ```

   You should see your GitHub repos.

4. **Test Context7**:

   ```
   @workspace Get documentation for React useEffect
   ```

   You should get official React docs.

5. **Test Playwright**:

   ```
   @workspace Navigate to https://example.com and take a screenshot
   ```

   You should get a browser screenshot.

### Check MCP Server Status

1. Open Command Palette (Ctrl+Shift+P)
2. Type "GitHub Copilot: MCP Server Status"
3. Verify all servers show as "Connected"

## Troubleshooting

### Server Won't Start

**Symptom**: MCP server shows as "Disconnected"

**Solutions**:

1. **Check Node.js version**:

   ```bash
   node --version
   # Should be v18 or higher
   ```

2. **Reinstall server**:

   ```bash
   npm uninstall -g @modelcontextprotocol/server-github
   npm install -g @modelcontextprotocol/server-github
   ```

3. **Check VS Code logs**:
   - Help > Toggle Developer Tools
   - Console tab
   - Look for MCP-related errors

### GitHub Token Issues

**Symptom**: GitHub MCP server can't authenticate

**Solutions**:

1. **Verify token is set**:

   ```bash
   # Windows PowerShell
   $env:GITHUB_TOKEN
   
   # macOS/Linux
   echo $GITHUB_TOKEN
   ```

2. **Regenerate token** with correct scopes

3. **Restart VS Code** after setting token

### Permission Denied

**Symptom**: "EACCES" or permission errors

**Solutions**:

1. **Fix npm permissions**:

   ```bash
   # macOS/Linux
   sudo chown -R $USER /usr/local/lib/node_modules
   
   # Or use nvm (recommended)
   curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
   nvm install 18
   ```

2. **Use npx** instead of global install (no permissions needed)

## Advanced Configuration

### Custom MCP Server Timeouts

```json
{
  "github.copilot.chat.mcp.servers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "${env:GITHUB_TOKEN}"
      },
      "timeout": 30000  // 30 seconds
    }
  }
}
```

### Workspace-Specific MCP Configuration

Create `.vscode/settings.json` in your project:

```json
{
  "github.copilot.chat.mcp.enabled": true,
  "github.copilot.chat.webSearch.enabled": true,
  "github.copilot.chat.mcp.servers": {
    // Project-specific MCP servers
    "database": {
      "command": "npx",
      "args": ["-y", "@mycompany/database-mcp"]
    }
  }
}
```

### Logging and Debugging

Enable verbose MCP logging:

```json
{
  "github.copilot.advanced": {
    "debug.overrideEngine": "copilot-chat",
    "debug.testOverrideProxyUrl": "",
    "debug.overrideProxyUrl": "",
    "debug.filterLogCategories": ["mcp"]
  }
}
```

View logs:

1. Help > Toggle Developer Tools
2. Console tab
3. Filter by "mcp"

## Security Best Practices

### ⚠️ Token Security

**DO**:

- ✅ Use environment variables for tokens
- ✅ Use GitHub fine-grained tokens with minimal scopes
- ✅ Rotate tokens regularly
- ✅ Never commit tokens to git

**DON'T**:

- ❌ Hardcode tokens in settings.json
- ❌ Share tokens
- ❌ Use tokens with excessive permissions
- ❌ Commit `.env` files

### MCP Server Permissions

Only enable MCP servers you actually need. Each server has access to:

- Your codebase
- Your chat history with Copilot
- Any APIs it connects to

Review server source code before using:

```bash
# Check what a server does
npm view @modelcontextprotocol/server-github repository
```

## MCP Server Directory

### Official Microsoft Servers

- **Playwright MCP** - `@microsoft/playwright-mcp`
- **Microsoft Learn MCP** - `@microsoftdocs/mcp`
- **Azure MCP** - `@azure/mcp`
- **Azure DevOps MCP** - `@microsoft/azure-devops-mcp`

### Official Third-Party Servers

- **GitHub MCP** - `@modelcontextprotocol/server-github`
- **Stripe MCP** - `@stripe/agent-toolkit`
- **MongoDB MCP** - `@mongodb-js/mongodb-mcp-server`
- **Elasticsearch MCP** - `@elastic/mcp-server-elasticsearch`
- **Sentry MCP** - `@getsentry/sentry-mcp`

### Community Servers

Find more at: <https://code.visualstudio.com/mcp>

## Usage in Copilot Chat

### Using Web Search

```
@workspace #websearch [query]

Example:
@workspace #websearch Next.js 15 server actions best practices 2025
```

### Using GitHub MCP

```
@workspace List repositories
@workspace Show issues in dstorey87/copilot-guardrails
@workspace Create branch feature/new-feature
```

### Using Playwright MCP

```
@workspace Navigate to https://example.com
@workspace Click on "Login" button
@workspace Take screenshot of current page
```

### Using Context7

```
@workspace Get React documentation for hooks
@workspace Show me TypeScript utility types docs
```

## Enterprise Configuration

### Organization-Wide MCP Policies

For GitHub Copilot Business/Enterprise:

1. Go to GitHub organization settings
2. Navigate to Copilot > Policies
3. Configure "MCP servers in Copilot" policy
4. Approve specific MCP servers for your organization

See: <https://docs.github.com/copilot/managing-copilot/managing-policies-for-copilot-in-your-organization>

### Approved Server List

Create `.github/approved-mcp-servers.json`:

```json
{
  "approved": [
    "@modelcontextprotocol/server-github",
    "@microsoft/playwright-mcp",
    "@upstash/context7-mcp"
  ],
  "blocked": [
    "@untrusted/server"
  ]
}
```

## Updating MCP Servers

### Check for Updates

```bash
# Check outdated global packages
npm outdated -g

# Update specific server
npm update -g @modelcontextprotocol/server-github

# Update all global packages
npm update -g
```

### Automatic Updates with npx

Using `npx -y` automatically uses the latest version:

```json
{
  "github.copilot.chat.mcp.servers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"]
      // Always uses latest version
    }
  }
}
```

## Support and Resources

### Official Documentation

- [GitHub Copilot Docs](https://docs.github.com/copilot)
- [MCP Specification](https://modelcontextprotocol.io)
- [VS Code MCP Guide](https://code.visualstudio.com/docs/copilot/mcp-servers)

### Community

- [GitHub Copilot Discussions](https://github.com/orgs/community/discussions/categories/copilot)
- [VS Code Copilot Issues](https://github.com/microsoft/vscode-copilot-release/issues)
- [MCP Community Discord](https://discord.gg/modelcontextprotocol)

### Getting Help

1. Check this guide
2. Search GitHub Discussions
3. Check MCP server repository issues
4. Contact GitHub Support (for Copilot issues)

---

**Last Updated**: October 2025  
**Maintained By**: dstorey87  
**Related**: [README.md](./README.md) | [Guardrails Instructions](./.github/copilot-instructions.md)
