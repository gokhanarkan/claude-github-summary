# GitHub Summary Skill

A Claude Code skill that generates AI-synthesised summaries of your GitHub activity. Get a natural language narrative of your issues, pull requests, and commits with inline URL references.

## Features

- **AI-written summaries** - Not just lists, but contextual narratives explaining what you worked on and why
- **Multiple data sources** - Works with GitHub MCP Server or gh CLI (auto-detects and lets you choose)
- **Rich context** - Fetches comments, linked PRs, review feedback, and sub-issues
- **TLDR section** - Quick bullet points for scanning
- **Flexible output** - Saves to your preferred location with proper formatting

## Installation

### Option 1: Copy to your project

```bash
# Create the skills directory if it doesn't exist
mkdir -p .claude/skills/github-summary

# Download the skill
curl -o .claude/skills/github-summary/SKILL.md \
  https://raw.githubusercontent.com/gokhanarkan/claude-github-summary/main/SKILL.md
```

### Option 2: Clone and symlink

```bash
git clone https://github.com/gokhanarkan/claude-github-summary.git
ln -s $(pwd)/claude-github-summary/SKILL.md .claude/skills/github-summary/SKILL.md
```

## Prerequisites

You need at least one of these configured:

### GitHub MCP Server (Recommended)

Configure in your Claude Code settings. Provides richer context and faster queries.

### GitHub CLI

```bash
# Install gh CLI (if not already installed)
brew install gh  # macOS
# or see https://cli.github.com/

# Authenticate
gh auth login
```

## Usage

Simply invoke the skill in Claude Code:

```
/github-summary
```

Or use natural language:

```
Summarise my GitHub activity for the last two weeks
```

### Interactive Flow

1. **Data source selection** - If both MCP and gh CLI are available, you choose which to use
2. **Organisation selection** - Pick from your organisations or search all
3. **Time period** - Last 7/14/30 days, this month, or custom range
4. **Summary generation** - Claude fetches data, synthesises, and writes the summary

## Example Output

```markdown
# GitHub Summary

**Period:** 2 January 2026 to 9 January 2026
**Organisation:** acme-corp

---

## TLDR

- Shipped new authentication flow with OAuth 2.0 PKCE support, improving security for mobile clients
- Merged 5 PRs across api-gateway and web-dashboard repositories
- Resolved critical session handling bug affecting 15% of users on Safari
- Reviewed 3 PRs including the new rate limiting middleware

---

## Overview

This week focused on authentication improvements and bug fixes across the platform.
The main initiative was implementing OAuth 2.0 PKCE for our mobile applications...

## Issues

I opened [#234: Safari users experiencing random logouts](https://github.com/acme-corp/api-gateway/issues/234)
which had been affecting approximately 15% of our Safari user base...

## Pull Requests

### Authored

The main authentication work landed in [#312: Implement OAuth 2.0 PKCE flow](https://github.com/acme-corp/api-gateway/pull/312)
which adds PKCE support to our OAuth implementation...

### Reviewed

I reviewed [#320: Add rate limiting middleware](https://github.com/acme-corp/api-gateway/pull/320) by @alice,
which implements Redis-backed rate limiting...
```

See [examples/sample-output.md](examples/sample-output.md) for a complete example.

## Configuration

The skill automatically determines where to save the summary:

1. Looks for an `Inbox/` folder in the current directory
2. If using a pillar structure (e.g., `GitHub/`, `Personal/`), uses the appropriate pillar's Inbox
3. Falls back to current directory if no structure is found

### Customisation

You can modify `SKILL.md` to:

- Change the output template structure
- Adjust the TLDR bullet count
- Add custom tags
- Modify date format preferences

## How It Works

1. **Discovery phase** - Searches for issues you created AND issues you're involved in (assigned, commented, mentioned)
2. **Deep context fetch** - For each item, fetches comments, reviews, linked PRs, timeline events
3. **AI synthesis** - Claude analyses all context and writes a coherent narrative
4. **Output** - Saves markdown file with TLDR, Overview, Issues, PRs, and Commits sections

## Contributing

Contributions welcome! Please:

1. Test changes with both MCP Server and gh CLI
2. Ensure the skill works across different repository structures
3. Update examples if changing output format

## Related Projects

- [minimal-second-brain](https://github.com/gokhanarkan/minimal-second-brain) - Knowledge management template with Claude integration
- [awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills) - Community collection of Claude skills

## License

MIT License - see [LICENSE](LICENSE)
