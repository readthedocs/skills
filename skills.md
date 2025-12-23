# Skills

This repository contains Agent Skills for Read the Docs.

## readthedocs-search-api

Query the Read the Docs Search API to find documentation across projects and repositories.

**Location**: `.claude/skills/readthedocs-search-api/`

**Description**: Query the Read the Docs Search API to find documentation across projects and repositories. Use when searching documentation, finding related docs, finding API documentation, or gathering information about projects on Read the Docs.

**Base URL**: `https://readthedocs.org/api/v3/search/`

### Quick Start

```bash
curl "https://readthedocs.org/api/v3/search/?q=authentication"
```

### Features

- Search across millions of pages of documentation
- No authentication required (public API)
- Paginated results
- Project and version information
- HTML highlights of matched text
- Section-level search results

See [.claude/skills/readthedocs-search-api/SKILL.md](.claude/skills/readthedocs-search-api/SKILL.md) for detailed instructions.
