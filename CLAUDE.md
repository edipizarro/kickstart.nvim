# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a personal fork of kickstart.nvim - a Neovim configuration written entirely in Lua. The main configuration lives in `init.lua` (~1000 lines) with optional plugin modules in `lua/kickstart/plugins/`.

## Commands

**Lint Lua code:**
```bash
stylua --check .
```

**Format Lua code:**
```bash
stylua .
```

**Check Neovim health:**
```
:checkhealth
```

**Manage plugins:**
```
:Lazy          # Open plugin manager UI
:Lazy sync     # Update and install plugins
:Lazy update   # Update plugins
```

## Architecture

### Plugin Manager
Uses **lazy.nvim** for plugin management. Plugins are bootstrapped automatically on first run (lines 207-217 in init.lua).

### Configuration Structure
- `init.lua` - Main configuration file containing core settings, keymaps, and plugin definitions
- `lua/kickstart/plugins/` - Optional plugin modules that can be enabled by uncommenting requires in init.lua:
  - `lint.lua` - Currently enabled; configures nvim-lint with markdownlint
  - `debug.lua` - DAP debugging configuration
  - `gitsigns.lua` - Git signs with extended keymaps
  - `autopairs.lua` - Auto-closing brackets
  - `indent_line.lua` - Indentation guides
  - `neo-tree.lua` - File explorer
- `lua/custom/plugins/init.lua` - Reserved for personal plugin additions
- `lua/kickstart/health.lua` - Health check module for `:checkhealth`

### LSP Configuration
LSP servers are managed via **mason.nvim** and configured in the `servers` table (~line 530). Currently configured:
- `gopls` (Go)
- `pyright` (Python)
- `ruff` (Python linting)
- `ts_ls` (TypeScript/JavaScript)
- `eslint` (JS/TS linting, with increased memory: 12288MB)
- `terraformls` (Terraform)
- `lua_ls` (Lua, with special lazydev integration)

### Formatting
Handled by **conform.nvim** (~line 760). Configured formatters:
- Lua: stylua
- Python: ruff, isort

### Key Patterns
- Leader key: `<Space>`
- Keymaps organized by prefix: `<leader>s*` (search), `<leader>c*` (code), `<leader>g*` (git), `<leader>d*` (document)
- Plugins use lazy loading via `event`, `keys`, `cmd`, and `ft` options

## Code Style

Lua formatting is enforced via stylua. Configuration in `.stylua.toml`:
- 2-space indentation
- 160 character line width
- Single quotes preferred
- No call parentheses for simple calls

## Working on This Config

When making changes, proactively suggest improvements if there's a better way to configure Neovim - whether that's newer plugin alternatives, more efficient lazy-loading patterns, cleaner Lua idioms, or better keybinding organization.
