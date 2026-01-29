# Obsidian Skills

A collection of Claude Code skills for Obsidian vault management.

## Available Skills

| Skill | Description |
|-------|-------------|
| [til](./skills/til) | Fetch URL content, auto-summarize, and add TIL entry to Daily Note |

## Installation

### 1. Add this marketplace

```bash
/plugin marketplace add https://github.com/azyu/obsidian-skills.git
```

### 2. Install a skill

```bash
/plugin install til@obsidian-skills
```

## til Usage

```
/til <URL> [description] [--tag=category]
```

### Examples

```bash
/til https://example.com/article
/til https://github.com/repo "usage notes"
/til https://blog.com/post --tag=tech
/til https://book.com/review "great book" --tag=book
```

### Workflow

1. **Parse Arguments** - Extract URL, description, and tag from input
2. **Check Daily Note** - Find or create today's Daily Note
3. **Fetch Content** - Get URL content and generate Korean summary
4. **Auto-detect Tag** - Categorize based on content keywords
5. **Add Entry** - Insert TIL entry to Daily Note
6. **Confirm** - Display completion message

### Auto-detect Tags

| Tag | Keywords |
|-----|----------|
| `#til/tech` | programming, code, API, tool, AI, dev, software, github |
| `#til/career` | job, interview, workplace, hiring, resume, salary |
| `#til/life` | life, hobby, personal, health, travel, food |
| `#til/finance` | money, investment, stock, crypto, finance, budget |
| `#til/book` | book, reading, review, author, novel |

### TIL Entry Format

```markdown
### [Title](URL)
**Tags:** #til/category
**Summary:** URL content summary (2-3 sentences, in Korean)
**My Note:** User's description (if provided)
```

## License

MIT
