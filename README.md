# opencode-init

A comprehensive OpenCode skill for initializing and configuring OpenCode settings, permissions, agents, MCP servers, models, themes, and tools.

## Overview

`opencode-init` is a reusable skill that helps you set up and configure all aspects of OpenCode for optimal workflow. Whether you're starting a new project or optimizing your existing setup, this skill provides expert guidance on OpenCode configuration best practices.

## Installation

### Global Installation (Recommended)

The skill is automatically available globally when symlinked to your OpenCode configuration:

```bash
# The skill is already symlinked to:
~/.config/opencode/skills/opencode-init -> ~/dev/opencode-init/
```

### Project-Local Installation

If you prefer project-specific configuration:

```bash
cd your-project
mkdir -p .opencode/skills
cp -r ~/dev/opencode-init .opencode/skills/
```

## Usage

Simply ask OpenCode to load the skill:

```
Load the opencode-init skill
```

Or reference it when asking for help:

```
Help me configure OpenCode for this project
```

## What This Skill Covers

### 🎯 Core Configuration
- **Project Config**: `opencode.json` structure and options
- **Global Config**: User-wide settings in `~/.config/opencode/`

### 🔐 Permission System
- Permission levels (`allow`, `deny`, `ask`)
- Pattern-based permissions with wildcards
- Per-agent permission overrides

### 🤖 Agent Configuration
- Built-in agents: `code`, `ask`, `edit`, `plan`, `review`, `researcher`
- Custom agent definition with frontmatter
- Agent modes and tool permissions

### 🔌 MCP Server Setup
- Adding external MCP servers
- Popular MCP servers (Filesystem, Git, SQLite, Brave Search, Puppeteer)
- Environment variable configuration

### 🤖 Model Configuration
- Default model selection
- Per-agent model assignment
- Smart/fast model switching

### 🎨 Theme Configuration
- UI theme customization
- Dark/light mode
- Accent colors and fonts

### 🛠️ Tools Configuration
- Enabling/disabling specific tools
- Per-agent tool control

### 📝 Rules Configuration
- Global project rules
- Per-agent rules
- Code style guidelines

### ⚡ Commands Configuration
- Custom commands
- Slash command creation

### 🔧 Formatters & LSP
- Code formatter setup
- LSP server configuration

## Directory Structure

```
~/dev/opencode-init/
├── SKILL.md          # Main skill definition
├── README.md         # This file
└── .git/            # Git repository
```

## Development

The skill is developed in `~/dev/opencode-init/` and symlinked to `~/.config/opencode/skills/` for global availability.

### Making Changes

1. Edit `SKILL.md` in `~/dev/opencode-init/`
2. Changes are immediately available (symlink is live)
3. Commit your changes:
   ```bash
   cd ~/dev/opencode-init
   git add .
   git commit -m "Your commit message"
   ```

## Future Publishing

This skill can be published to:

- **NPM**: As `opencode-init` package
- **GitHub**: For community sharing
- **OpenCode Ecosystem**: As an official skill

## License

MIT License - See [SKILL.md](SKILL.md) for details

## Contributing

Contributions welcome! Please:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## Support

- **OpenCode Docs**: https://opencode.ai/docs
- **Discord**: https://opencode.ai/discord
- **Issues**: Create an issue on GitHub

---

**Built with ❤️ for the OpenCode community**
