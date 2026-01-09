# GitHub Summary Skill

A skill that generates AI-synthesised summaries of your GitHub activity. Works with **both Claude Code and GitHub Copilot CLI**.

## Features

- **Cross-platform** - Works with Claude Code and GitHub Copilot CLI
- **AI-written summaries** - Contextual narratives explaining what you worked on and why
- **Multiple data sources** - Works with GitHub MCP Server or gh CLI (auto-detects)
- **Rich context** - Fetches comments, linked PRs, review feedback, and sub-issues
- **TLDR section** - Quick bullet points for scanning
- **Flexible output** - Saves to your preferred location

## Installation

### For Claude Code

```bash
mkdir -p .claude/skills/github-summary
curl -o .claude/skills/github-summary/SKILL.md \
  https://raw.githubusercontent.com/gokhanarkan/claude-github-summary/main/SKILL.md
```

### For GitHub Copilot CLI

```bash
mkdir -p .github/skills/github-summary
curl -o .github/skills/github-summary/SKILL.md \
  https://raw.githubusercontent.com/gokhanarkan/claude-github-summary/main/SKILL.md
```

## Prerequisites

You need at least one of these configured:

### GitHub MCP Server (Recommended)

Configure in your Claude Code or Copilot settings. Provides richer context and faster queries.

### GitHub CLI

```bash
# Install gh CLI (if not already installed)
brew install gh  # macOS
# or see https://cli.github.com/

# Authenticate
gh auth login
```

## Usage

### Claude Code

```bash
/github-summary
```

Or natural language:

```bash
Summarise my GitHub activity for the last two weeks
```

### GitHub Copilot CLI

```bash
/github-summary
```

Or reference the skill:

```bash
skill(github-summary)
```

## Interactive Flow

Both tools follow the same flow:

1. **Data source selection** - If both MCP and gh CLI are available, you choose which to use
2. **Organisation selection** - Pick from your organisations or search all
3. **Time period** - Last 7/14/30 days, this month, or custom range
4. **Summary generation** - AI fetches data, synthesises, and outputs the summary

## Output Style

The skill is designed to produce **natural language narratives**, not tables or bullet lists. The writing guidelines explicitly instruct the AI to:

- Write flowing paragraphs that tell a story
- Reference URLs inline within sentences
- Explain significance and context, not just list facts
- Use the TLDR section as the only place for bullet points

Example output:

```markdown
## Overview

This week focused on authentication improvements. I identified a session
handling bug affecting Safari users ([#234](url)), implemented a fix using
PKCE flow ([#312](url)), and updated documentation to reflect the changes.

## Issues

I opened [#234: Safari users experiencing random logouts](url) after
receiving multiple user reports. Investigation revealed the root cause
was Safari's ITP blocking our session cookies...
```

## Example Output

See [examples/sample-output.md](examples/sample-output.md) for a complete Claude-style example.

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
3. **AI synthesis** - AI analyses all context and writes the summary
4. **Output** - Saves markdown file or displays in terminal

## Contributing

Contributions welcome! Please:

1. Test changes with both Claude Code and GitHub Copilot CLI
2. Test with both MCP Server and gh CLI data sources
3. Ensure the skill works across different repository structures
4. Update examples if changing output format

## Related Projects

- [minimal-second-brain](https://github.com/gokhanarkan/minimal-second-brain) - Knowledge management template with Claude integration
- [awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills) - Community collection of Claude skills
- [GitHub Copilot Skills Docs](https://docs.github.com/en/copilot/concepts/agents/about-agent-skills)

## License

MIT License - see [LICENSE](LICENSE)
