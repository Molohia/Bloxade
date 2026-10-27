<div align="center">

# BLOXADE

### Build Roblox experiences with AI, all in one workspace.

**A local-first AI development workspace for Roblox Studio, bringing Claude Code, OpenAI Codex, project tools, and coordinated AI agents together.**

[Getting Started](#getting-started) · [Features](#features) · [Roblox Studio Connection](#connect-to-roblox-studio) · [Development](#for-developers)

</div>

---

## What is BLOXADE?

**BLOXADE** is an independent Windows application designed to help Roblox creators plan, develop, debug, and manage their experiences with AI. Instead of jumping between AI chat windows, terminals, project folders, and Roblox Studio, BLOXADE brings those workflows into one local interface.

Connect supported **Claude Code** and **OpenAI Codex** accounts, organize projects, delegate tasks to multiple agents, review code changes, and use **Roblox Studio's MCP server** to give approved AI tools access to your open place.

> **Project status:** This repository contains a working implementation and its own test records, but integrations depend on the installed Claude/Codex tools and Roblox Studio version. Not every workflow has been independently verified on every Windows system. Review AI-generated changes before applying them.

## Features

| Feature | Description |
| --- | --- |
| **Claude Code + Codex** | Use supported AI coding CLIs from one workspace, with provider-based model selection. |
| **Multiple AI accounts** | Configure separate local profiles for multiple Claude Code and Codex accounts, using their official sign-in flows. |
| **Multi-agent workflows** | Break larger goals into tasks, assign agents, track progress and dependencies, and review results. |
| **Roblox Studio MCP** | Connect to Roblox Studio's official MCP server to inspect and, when authorized, edit your open place. |
| **Project management** | Organize project folders, instructions, chats, files, and tracked changes. |
| **Chat & Cowork modes** | Chat for discussion; Cowork for authorized file and Studio actions. |
| **Approvals & activity** | Control sensitive actions, inspect tool activity, and review changes. |
| **Usage visibility** | View provider-reported usage where available and distinguish it from application estimates. |
| **Efficiency presets** | Choose between Economy, Balanced, Performance, and Maximum Quality modes. |
| **Customizable UI** | Multiple themes and accent colors. |

## Getting started

### Requirements

- **Windows 10 or Windows 11**
- **Claude Code CLI and/or OpenAI Codex CLI**, installed and available on your computer
- **Roblox Studio** for Studio integration
- Internet access for provider sign-in and AI requests

### Start BLOXADE

1. Download or clone this repository.
2. Double-click **`START_BLOXADE.bat`**.
3. On first launch, allow the startup script to set up its local Node.js runtime if needed. An existing compatible Node.js installation can also be used.
4. BLOXADE opens in your browser at **http://127.0.0.1:3000**.
5. Follow the setup flow to connect an AI account and add your project folder.
6. To stop the app, close the launcher window or run **`STOP_BLOXADE.bat`**.

> BLOXADE runs locally, but Claude Code and Codex connect to their respective AI services. Their plans, usage limits, authentication requirements, and terms still apply. BLOXADE does not provide free access to paid models or bypass provider limits.

## Connect to Roblox Studio

1. Open **Roblox Studio** and load the place you want to work on.
2. Open **Assistant → ⋯ → Manage MCP Servers** (the exact wording may vary with Studio updates).
3. Enable **Studio as MCP server**.
4. Start BLOXADE and open **Connections → Roblox Studio**.
5. Click **Test connection**.
6. Open a **Cowork** chat or start an agent task with Studio access enabled.

BLOXADE's MCP bridge is designed to connect through Roblox's local Studio MCP launcher, typically located at `%LOCALAPPDATA%\Roblox\mcp.bat` on Windows.

**Back up your Roblox place before giving any AI agent editing permission.** When several agents work on one project, review changes carefully to avoid conflicts.

## How multi-agent work is organized

A typical workflow might look like this:

1. **Agent 1 — Gameplay:** Implements a Luau gameplay feature.
2. **Agent 2 — Interface:** Builds or improves related UI code.
3. **Agent 3 — Review:** Checks integration, identifies bugs, and proposes fixes.
4. **You — Final approval:** Review diffs, test in Studio, and accept or revert changes.

The codebase includes task coordination, file ownership and locking mechanisms, but **does not currently provide isolated Git worktrees for every agent**. Parallel agents are not guaranteed to avoid all conflicts, especially when editing the same live Studio place.

## For developers

The project uses **TypeScript, React, Vite, Tailwind CSS, Node.js, and SQLite**.

### Development commands

```bash
npm install
npm run dev:server
npm run dev:web
```

The backend runs on port **3000**, while the Vite development frontend normally runs on **5173**.

### Build and test

```bash
npm run typecheck
npm test
npm run build
```

The `package.json` specifies **Node.js 22.13 or newer**.

### Project structure

```text
BLOXADE/
├── src/
│   ├── web/                 # React user interface
│   ├── server/              # API, accounts, agents, projects, Roblox tools
│   │   ├── agents/          # Agent planning and coordination
│   │   ├── providers/       # Claude Code and Codex integrations
│   │   ├── roblox/          # Roblox Studio MCP connection
│   │   └── services/        # Chats, files, approvals, usage, etc.
│   ├── bridge/              # MCP bridge source
│   └── shared/              # Shared types
├── app/                     # Bundled runtime and web assets
├── scripts/                 # Build and setup scripts
├── tests/                   # Automated tests and fixtures
├── START_BLOXADE.bat        # Start on Windows
├── STOP_BLOXADE.bat         # Stop on Windows
├── PROGRESS.md              # Implementation notes
└── TESTING.md               # Test notes and checklist
```

## Privacy and security

- BLOXADE's local web server is designed to bind to **`127.0.0.1`**, not a public network address.
- App data, logs, and account profiles are stored under **`%LOCALAPPDATA%\BLOXADE`**.
- Sign-in uses the supported providers' CLI authentication flows; do not share your passwords, tokens, or local credential files.
- AI providers may receive prompts, code, and project context when you use their tools.
- Review approval prompts and never commit secrets, session data, or private credentials to GitHub.

## Creator

**Created by Blox_soward** — the developer behind BLOXADE.

| Platform | Username |
| --- | --- |
| **Roblox** | `Blox_soward` |
| **Discord** | `knz1w` |
| **GitHub** | [@molohia](https://github.com/molohia) |

## Documentation

- [PROJECT_DESCRIPTION.md](PROJECT_DESCRIPTION.md) — detailed overview of the product and architecture
- [AUTHORS.md](AUTHORS.md) — creator attribution
- [PROGRESS.md](PROGRESS.md) — implementation notes and known limitations
- [TESTING.md](TESTING.md) — test coverage and manual verification notes

## License and affiliation

**No license has been selected yet.** Unless a license is added, publishing this source code does not automatically give others permission to copy, modify, or redistribute it. The project owner may choose a license later.

BLOXADE is an **independent community project**, not an official product of Roblox, Anthropic, or OpenAI. Roblox, Roblox Studio, Claude, Claude Code, ChatGPT, and Codex are trademarks or product names of their respective owners. No endorsement or affiliation is implied.

---

<div align="center">

**BLOXADE — One workspace. Multiple AI agents. More time to create.**

Made by **Blox_soward** · [GitHub @molohia](https://github.com/molohia)

</div>
