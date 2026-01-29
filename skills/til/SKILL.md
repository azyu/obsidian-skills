---
name: til
description: Fetch URL content, auto-summarize, and add TIL entry to Obsidian Daily Note. Usage: /til <URL> [description] [--tag=category]
user-invocable: true
---

# TIL (Today I Learned) Skill

Summarize URL content and add it to the TIL section in Daily Note.

## Usage

```
/til <URL> [description] [--tag=category]
```

**Examples:**
- `/til https://example.com/article`
- `/til https://github.com/repo "usage notes"`
- `/til https://blog.com/post --tag=tech`
- `/til https://book.com/review "great book" --tag=book`

## Workflow

### 1. Parse Arguments

Arguments: `$ARGUMENTS`

Extract the following:
- **URL** (required): First argument starting with http/https
- **Description** (optional): Text in quotes or text after URL
- **Tag** (optional): `--tag=<category>` format, auto-detect if not provided

### 2. Check Daily Note Path

```
VAULT_PATH="/Users/azyu/Library/Mobile Documents/iCloud~md~obsidian/Documents/Vault"
TODAY=$(date +%Y-%m-%d)
DAILY_NOTE="$VAULT_PATH/10_Daily/$TODAY.md"
```

If Daily Note doesn't exist:
1. Check for `00_Templates/Daily Note Template.md` template
2. If template exists, copy to create new note
3. If no template, create with basic structure

### 3. Fetch URL Content

Use WebFetch tool to get URL content:
1. Extract **title** (page title or h1)
2. Generate **summary** (2-3 sentences, in Korean)

If URL is inaccessible:
- Notify user
- Use URL domain as title
- Mark summary as "Content unavailable"

### 4. Auto-detect Tag

If `--tag` is not provided, auto-detect based on URL content:

| Tag | Keywords |
|-----|----------|
| `#til/tech` | programming, code, API, tool, AI, dev, software, github |
| `#til/career` | job, interview, workplace, hiring, resume, salary |
| `#til/life` | life, hobby, personal, health, travel, food |
| `#til/finance` | money, investment, stock, crypto, finance, budget |
| `#til/book` | book, reading, review, author, novel |

Default: `#til/tech`

### 5. TIL Entry Format

```markdown
### [Title](URL)
**Tags:** #til/category
**Summary:** URL content summary (2-3 sentences, in Korean)
**My Note:** User's description (omit this line if no description)
```

### 6. Add to Daily Note

1. Read Daily Note file
2. Find `## TIL (오늘 내가 배운 것)` section
   - If section doesn't exist, create it at end of file
3. Add new entry right after section header
4. Update `updated:` timestamp in frontmatter (if present)

### 7. Completion Message

```
✅ TIL added!
- Title: [title]
- Tag: #til/category
- File: 10_Daily/YYYY-MM-DD.md
```

## Error Handling

| Situation | Response |
|-----------|----------|
| No URL | Output "Please provide a URL" |
| URL inaccessible | Offer to save with title+description only |
| No TIL section | Auto-create section |
| No Daily Note | Create from template or basic structure |

## Important Notes

- Check if same URL already exists; notify user if duplicate
- Summary MUST be written in Korean
- Never delete existing Daily Note content
