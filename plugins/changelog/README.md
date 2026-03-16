# Changelog Plugin

Auto-generate CHANGELOG.md entries from git history using [Keep a Changelog](https://keepachangelog.com/en/1.0.0/) format.

## Overview

This plugin provides an agent skill that analyzes your git history, reviews diffs, and generates structured changelog entries. It filters noise commits, groups changes into standard sections, and inserts entries into your CHANGELOG.md.

## Features

**Agent Skill:**
- `changelog` - Generates CHANGELOG.md entries from git commits since last recorded entry

## Quick Start

Ask Claude to update your changelog:

```
"Update the changelog"
"Generate changelog entries from recent commits"
"Add recent changes to the changelog"
```

Claude will automatically:
1. Read your existing CHANGELOG.md (or create one)
2. Find commits since the last recorded entry
3. Filter out noise (config-only, changelog-only commits)
4. Review actual diffs for accuracy
5. Generate grouped entries (Added, Changed, Fixed, Removed)
6. Insert the new entry into CHANGELOG.md

## Format

Entries follow Keep a Changelog format with timestamped headers:

```markdown
## 2026-03-16 14:30:00 `abc1234`

### Added
- New user authentication flow (`def5678`)

### Fixed
- Resolve crash on empty input (`789abcd`)
```

Each entry references the git hash it covers through.

## Installation

### From cc-marketplace

```bash
# Add the marketplace
/plugin marketplace add tasanakorn/cc-marketplace

# Install the plugin
/plugin install changelog
```

### Manual Installation

```bash
cp -r plugins/changelog ~/.claude/plugins/
```

## Plugin Structure

```
changelog/
├── .claude-plugin/
│   └── plugin.json        # Plugin metadata
├── skills/
│   └── changelog/
│       └── SKILL.md       # Changelog generation skill
└── README.md              # This file
```

## Author

Tasanakorn Phaipool <tasanakorn@gmail.com>
