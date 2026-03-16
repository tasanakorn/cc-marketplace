---
name: changelog
description: Auto-generates CHANGELOG.md entries from git history using Keep a Changelog format. Analyzes commits since last recorded entry, filters noise, reviews diffs, and groups changes into Added/Changed/Fixed/Removed sections.
---

# Changelog Skill

Generate CHANGELOG.md entries from git history using [Keep a Changelog](https://keepachangelog.com/en/1.0.0/) format.

## Capabilities

- Read existing CHANGELOG.md and detect where to insert new entries
- Analyze git history since last recorded commit
- Filter out noise commits (changelog-only, config-only changes)
- Review actual diffs to write accurate, user-facing descriptions
- Group changes into standard sections: Added, Changed, Fixed, Removed

## Usage

This skill activates when:
- User asks to "update the changelog"
- User asks to "generate changelog entries"
- User wants to "add recent changes to CHANGELOG.md"
- User mentions "changelog" in context of git history

## Approach

### Step 1: Read Current State

Read `CHANGELOG.md` in the project root. Extract the last recorded commit hash from the first `## ... \`hash\`` header line.

- If CHANGELOG.md does not exist, create one with a title and description header
- If no hash is found in any header, fall back to the repository's initial commit

### Step 2: Get New Commits

Run:
```bash
git log <LAST_HASH>..HEAD --format="%h %s" --reverse
```

If there are no new commits, inform the user and stop.

### Step 3: Filter Noise Commits

Skip commits that ONLY touch:
- `CHANGELOG.md`
- `CLAUDE.md` or `.claude/` files
- `.gitignore`
- Dev config files (editor settings, linter configs) with no functional code changes

### Step 4: Review Diffs

For each remaining commit, review the actual diff:
```bash
git diff <HASH>^..<HASH>
```

Diffs are the source of truth — do not rely solely on commit messages.

### Step 5: Group and Write Entries

Group changes into sections (omit empty ones):
- **Added** — New features or capabilities
- **Changed** — Modifications to existing functionality
- **Fixed** — Bug fixes
- **Removed** — Removed features or capabilities

Merge related commits into single bullets. Write concise, user-facing descriptions. Reference the git hash each entry covers through.

### Step 6: Format Header

Use the author date of HEAD:
```bash
git log -1 HEAD --format="%h %ai"
```

Header format:
```
## YYYY-MM-DD HH:mm:ss `SHORT_HASH`
```

### Step 7: Insert Entry

Insert the new entry after the CHANGELOG.md header block (title + description paragraph), before the first existing `##` entry.

### Step 8: Report

Tell the user what was added. Do NOT commit the changes — leave that to the user.

## Output Format

The generated CHANGELOG.md entry follows this structure:

```markdown
## 2026-03-16 14:30:00 `abc1234`

### Added
- New feature description (`def5678`)

### Changed
- Modified behavior description (`abc1234`)

### Fixed
- Bug fix description (`789abcd`)
```

## Notes

- Each entry references the git hash it covers through
- Description paragraph in CHANGELOG.md: "Maintained with the help of AI tooling. Each entry references the git hash it covers through."
- Keep bullets concise and user-facing — avoid implementation details
- When multiple commits relate to the same feature, merge them into one bullet
