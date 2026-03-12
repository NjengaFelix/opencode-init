---
name: opencode-init
description: Initialize OpenCode settings, permissions, agents, MCP servers, models, themes, and tools for optimal workflow
license: MIT
compatibility: opencode
metadata:
  category: configuration
  type: official
---

# OpenCode Configuration Guide

This skill helps configure all aspects of OpenCode for your workspace.

## Core Configuration Files

### 1. Project Config: `opencode.json`

The main configuration file in your project root:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "default_agent": "researcher",
  "permission": {
    "skill": "ask",
    "webfetch": "allow",
    "read": "allow",
    "write": "allow",
    "edit": "allow",
    "bash": "allow",
    "glob": "allow",
    "grep": "allow"
  }
}
```

### 2. Global Config: `~/.config/opencode/opencode.json`

User-wide settings that apply to all projects.

---

## Permission System

### Permission Levels

| Level | Behavior |
|-------|----------|
| `allow` | Immediate execution |
| `deny` | Block and hide from agent |
| `ask` | Prompt user for approval |

### Pattern-Based Permissions

```json
{
  "permission": {
    "skill": {
      "*": "allow",
      "pr-review": "allow",
      "internal-*": "deny",
      "experimental-*": "ask"
    }
  }
}
```

### Per-Agent Permissions

```json
{
  "agent": {
    "plan": {
      "permission": {
        "skill": {
          "internal-*": "allow"
        }
      }
    }
  }
}
```

---

## Agent Configuration

### Built-in Agents

Available built-in agents: `code`, `ask`, `edit`, `plan`, `review`, `researcher`

### Custom Agent Definition

Create `.opencode/agents/my-agent.md`:

```markdown
---
description: Specialized agent for [purpose]
mode: primary|secondary
tools:
  skill: true
  webfetch: true
  read: true
  write: true
  edit: true
  bash: true
permission:
  skill:
    "*": "allow"
---

# My Agent

## Purpose
What this agent does...

## Workflow
1. Step one
2. Step two

## Tools
- Use `skill` to load domain knowledge
- Use `read` to examine files
```

### Agent Frontmatter Options

| Field | Description |
|-------|-------------|
| `description` | Short description for agent selection |
| `mode` | `primary` (default) or `secondary` |
| `tools` | Enable/disable specific tools |
| `permission` | Override global permissions |

---

## MCP Server Configuration

### Adding MCP Servers

```json
{
  "mcpServers": {
    "server-name": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/path"],
      "env": {
        "ENV_VAR": "value"
      }
    }
  }
}
```

### Popular MCP Servers

- **Filesystem**: `@modelcontextprotocol/server-filesystem`
- **Git**: `@modelcontextprotocol/server-git`
- **SQLite**: `@modelcontextprotocol/server-sqlite`
- **Brave Search**: `@modelcontextprotocol/server-brave-search`
- **Puppeteer**: `@modelcontextprotocol/server-puppeteer`

### Environment Variables

```json
{
  "mcpServers": {
    "brave-search": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-brave-search"],
      "env": {
        "BRAVE_API_KEY": "${BRAVE_API_KEY}"
      }
    }
  }
}
```

---

## Model Configuration

### Setting Default Models

```json
{
  "model": {
    "default": "claude-sonnet-4",
    "fast": "claude-haiku-4",
    "smart": "claude-opus-4"
  }
}
```

### Per-Agent Models

```json
{
  "agent": {
    "code": {
      "model": "claude-sonnet-4"
    },
    "plan": {
      "model": "claude-opus-4"
    }
  }
}
```

### Model Options

Available models depend on your providers. Common options:
- `claude-opus-4`
- `claude-sonnet-4`
- `claude-haiku-4`
- `gpt-4o`
- `gpt-4o-mini`

---

## Theme Configuration

### UI Themes

```json
{
  "theme": {
    "mode": "dark",
    "accent": "blue",
    "font": "jetbrains-mono"
  }
}
```

### Available Themes

Check current themes with: `/theme` command in TUI

---

## Tools Configuration

### Enabling/Disabling Tools

```json
{
  "tools": {
    "skill": true,
    "webfetch": true,
    "read": true,
    "write": true,
    "edit": true,
    "bash": true,
    "glob": true,
    "grep": true
  }
}
```

### Per-Agent Tool Control

```json
{
  "agent": {
    "review": {
      "tools": {
        "write": false,
        "edit": false,
        "bash": false
      }
    }
  }
}
```

---

## Rules Configuration

### Global Rules

Create `.opencode/rules.md` for project-wide rules:

```markdown
# Project Rules

## Code Style
- Use TypeScript strict mode
- Prefer async/await over callbacks

## File Organization
- Place tests in `__tests__/` directories
- Use kebab-case for file names
```

### Per-Agent Rules

```json
{
  "agent": {
    "code": {
      "rules": [
        "Always add JSDoc comments",
        "Follow existing code patterns"
      ]
    }
  }
}
```

---

## Commands Configuration

### Custom Commands

```json
{
  "commands": {
    "test": "npm test",
    "build": "npm run build",
    "lint": "npm run lint"
  }
}
```

### Slash Commands

Create custom slash commands in `.opencode/commands/`:

```javascript
// .opencode/commands/deploy.js
export default async function({ context }) {
  await context.tools.bash.execute({
    command: "npm run build && npm run deploy"
  });
}
```

---

## Formatters Configuration

### Setting Formatters

```json
{
  "formatters": {
    "typescript": "prettier",
    "javascript": "prettier",
    "json": "prettier",
    "markdown": "prettier"
  }
}
```

### Formatter Options

```json
{
  "formatters": {
    "prettier": {
      "printWidth": 100,
      "tabWidth": 2,
      "semi": true,
      "singleQuote": false
    }
  }
}
```

---

## LSP Server Configuration

### Adding LSP Servers

```json
{
  "lsp": {
    "typescript": {
      "command": "typescript-language-server",
      "args": ["--stdio"]
    },
    "eslint": {
      "command": "vscode-eslint-language-server",
      "args": ["--stdio"]
    }
  }
}
```

---

## Complete Example Configuration

```json
{
  "$schema": "https://opencode.ai/config.json",
  "default_agent": "code",
  
  "permission": {
    "skill": "ask",
    "webfetch": "allow",
    "read": "allow",
    "write": "allow",
    "edit": "ask",
    "bash": "ask",
    "glob": "allow",
    "grep": "allow"
  },
  
  "model": {
    "default": "claude-sonnet-4",
    "fast": "claude-haiku-4",
    "smart": "claude-opus-4"
  },
  
  "agent": {
    "code": {
      "model": "claude-sonnet-4",
      "permission": {
        "write": "allow",
        "edit": "allow"
      }
    },
    "plan": {
      "model": "claude-opus-4",
      "permission": {
        "skill": {
          "internal-*": "allow"
        }
      }
    }
  },
  
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "."]
    }
  },
  
  "commands": {
    "test": "npm test",
    "build": "npm run build"
  },
  
  "formatters": {
    "typescript": "prettier",
    "javascript": "prettier"
  },
  
  "theme": {
    "mode": "dark",
    "accent": "blue"
  }
}
```

---

## Best Practices

### Security
- Use `ask` permission for destructive operations
- Store sensitive env vars in `.env` files, not in config
- Review MCP server permissions before adding

### Organization
- Keep project-specific settings in `opencode.json`
- Use global config (`~/.config/opencode/opencode.json`) for user preferences
- Create custom agents for specialized workflows

### Version Control
- Commit `opencode.json` to share team settings
- Don't commit API keys or secrets
- Document custom agents and skills in README

### Skills Discovery
- Load this skill to reference configuration options
- Create domain-specific skills for repeated tasks
- Use pattern matching for skill permissions

---

## Troubleshooting

### Config Not Loading
1. Verify `$schema` is correct
2. Check JSON syntax is valid
3. Ensure file is named exactly `opencode.json`

### Agent Not Found
1. Check agent file is in `.opencode/agents/`
2. Verify frontmatter has `description`
3. Ensure `.md` extension

### MCP Server Failing
1. Verify command is in PATH
2. Check environment variables are set
3. Review MCP server logs with `--verbose`

### Permissions Not Applying
1. Check permission hierarchy (global vs project vs agent)
2. Verify pattern syntax for wildcards
3. Restart OpenCode to reload config

---

## When to Use

Use this skill when you need to:
- Set up a new OpenCode project
- Configure permissions for security
- Add MCP servers for extended functionality
- Customize agents for specific workflows
- Troubleshoot configuration issues
- Optimize model selection for tasks
- Set up global defaults
