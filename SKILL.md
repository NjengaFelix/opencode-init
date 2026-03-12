---
name: opencode-init
description: Initialize and configure OpenCode settings, permissions, agents, and tools for new projects
license: MIT
compatibility: opencode
metadata:
  category: configuration
  type: community
---

## What I do

I help you initialize OpenCode configurations for optimal development workflows:

- **Quick setup** - Choose from ready-to-use configuration templates
- **Permissions** - Configure safe defaults for solo or team development
- **Agents** - Create custom agents for specific tasks
- **MCP servers** - Add external tools (filesystem, search, databases)
- **Models** - Select optimal models for different use cases
- **Troubleshooting** - Fix common configuration issues

## When to use me

Load this skill when:

- **Setting up a new project** - "Initialize OpenCode for this project"
- **First-time setup** - "Help me configure OpenCode"
- **Security review** - "Make my OpenCode setup more secure"
- **Team onboarding** - "Set up OpenCode for our team"
- **Troubleshooting** - "My config isn't working"

## Quick Setup Templates

### Secure Team Setup (Recommended)
For collaborative projects requiring approval for destructive actions:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "default_agent": "build",
  "permission": {
    "skill": "ask",
    "webfetch": "allow",
    "read": "allow",
    "write": "ask",
    "edit": "ask",
    "bash": "ask",
    "glob": "allow",
    "grep": "allow"
  }
}
```

### Fast Solo Development
For personal projects where you trust the AI:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "default_agent": "build",
  "permission": {
    "skill": "allow",
    "webfetch": "allow",
    "read": "allow",
    "write": "allow",
    "edit": "allow",
    "bash": "ask",
    "glob": "allow",
    "grep": "allow"
  }
}
```

### Read-Only Analysis
For exploring code without making changes:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "default_agent": "plan",
  "permission": {
    "skill": "ask",
    "webfetch": "allow",
    "read": "allow",
    "write": "deny",
    "edit": "deny",
    "bash": "deny",
    "glob": "allow",
    "grep": "allow"
  }
}
```

## Essential Configurations

### Permission Patterns

Control what actions require approval:

| Level | Use case |
|-------|----------|
| `allow` | Safe operations (read, glob, grep) |
| `ask` | Destructive operations (write, edit, bash) |
| `deny` | Disable entirely |

**Pattern matching for specific tools:**
```json
{
  "permission": {
    "bash": {
      "*": "ask",
      "git status*": "allow",
      "git log*": "allow"
    }
  }
}
```

### MCP Server Quick Add

Add external capabilities (place in `opencode.json`):

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "."]
    },
    "brave-search": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-brave-search"],
      "env": {
        "BRAVE_API_KEY": "{env:BRAVE_API_KEY}"
      }
    }
  }
}
```

Popular MCP servers: filesystem, git, sqlite, brave-search, puppeteer

### Custom Agent Template

Create `.opencode/agents/my-agent.md`:

```markdown
---
description: What this agent does and when to use it
mode: subagent
tools:
  write: false
  edit: false
  bash: true
---

Your specific instructions here. Be clear about:
- What this agent should focus on
- What it should avoid
- How to provide output
```

### Model Selection

Choose appropriate models for different tasks:

```json
{
  "model": {
    "default": "anthropic/claude-sonnet-4",
    "fast": "anthropic/claude-haiku-4",
    "smart": "anthropic/claude-opus-4"
  }
}
```

## Common Workflows

### 1. New Project Setup
```
Load opencode-init
"Set up OpenCode for this Node.js project with team-friendly permissions"
```

### 2. Add MCP Server
```
"Help me add the filesystem MCP server to this project"
```

### 3. Create Code Review Agent
```
"Create an agent that reviews code without making edits"
```

### 4. Configure Models
```
"Set up fast model for simple tasks and smart model for complex ones"
```

## Best Practices

### Security
- **Never commit secrets** - Use `{env:VARIABLE}` syntax
- **Start restrictive** - Use `ask` permission, relax as needed
- **Review MCP servers** - Understand what access they need

### Organization
- **Global config** (`~/.config/opencode/`) for personal preferences
- **Project config** (`opencode.json`) for team-shared settings
- **Keep configs in git** - Safe to share (no secrets)

### Maintenance
- **Document custom agents** - Add README in `.opencode/agents/`
- **Version control skills** - Track custom skills in git
- **Test permissions** - Verify `ask` prompts work as expected

## Troubleshooting

### Config not loading
1. Verify file is named exactly `opencode.json`
2. Check JSON syntax with `jq opencode.json`
3. Ensure `$schema` is correct

### Agent not found
1. Check agent is in `.opencode/agents/` or `~/.config/opencode/agents/`
2. Verify frontmatter has `description`
3. Ensure file ends with `.md`

### Permission not applying
1. Check hierarchy: global → project → agent
2. Use wildcards correctly: `git *` not `git*`
3. Restart OpenCode to reload config

## Next Steps

For detailed configuration in specific areas, load these skills:

- **opencode-permissions** - Deep dive into security and permissions
- **opencode-mcp** - MCP server setup and management
- **opencode-agents** - Creating and customizing agents
- **opencode-models** - Model selection and optimization
