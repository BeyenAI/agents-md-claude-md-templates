# Multi-Client MCP Configuration Examples (2026)

> Generate, lint for plaintext secrets, and convert between all 6 client formats interactively at **[findaitier.com/mcp-config-generator/](https://findaitier.com/mcp-config-generator/)**.

Different AI coding clients use incompatible root keys and secret-injection syntax for the Model Context Protocol (MCP):

- **Claude Code (`.mcp.json`) / Claude Desktop / Cursor (`.cursor/mcp.json`) / Windsurf**: Root key is `"mcpServers"`.
- **VS Code (`.vscode/mcp.json`)**: Root key is `"servers"` and uses an `"inputs"` array (`${input:api-key}`) to avoid committing plaintext secrets.
- **OpenAI Codex CLI (`~/.codex/config.toml`)**: Uses TOML tables `[mcp_servers.<name>]` instead of JSON.

---

## 1. Claude Code (`.mcp.json`) & Cursor (`.cursor/mcp.json`)

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "./src"]
    },
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "${GITHUB_PERSONAL_ACCESS_TOKEN}"
      }
    }
  }
}
```

## 2. VS Code (`.vscode/mcp.json`)

```json
{
  "inputs": [
    {
      "type": "promptString",
      "id": "github-token",
      "description": "GitHub Personal Access Token",
      "password": true
    }
  ],
  "servers": {
    "filesystem": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "${workspaceFolder}/src"]
    },
    "github": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "${input:github-token}"
      }
    }
  }
}
```

## 3. OpenAI Codex CLI (`~/.codex/config.toml`)

```toml
[mcp_servers.filesystem]
command = "npx"
args = ["-y", "@modelcontextprotocol/server-filesystem", "./src"]

[mcp_servers.github]
command = "npx"
args = ["-y", "@modelcontextprotocol/server-github"]
env = { GITHUB_PERSONAL_ACCESS_TOKEN = "${GITHUB_PERSONAL_ACCESS_TOKEN}" }
```

---

Need to add Playwright, Postgres, Context7, Sequential Thinking, or custom HTTP/SSE servers? Build and export your config at **[FindAITier MCP Config Generator](https://findaitier.com/mcp-config-generator/)**.
