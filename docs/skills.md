# Available skills

## readthedocs-search-api

Query the Read the Docs Search API to find documentation across projects.

**Location**: `.claude/skills/readthedocs-search-api/`

**Use when**:

- Searching documentation
- Finding related docs
- Looking up API references
- Gathering information about Read the Docs projects

**Base URL**: `https://readthedocs.org/api/v3/search/`

### Quick start

```bash
curl "https://readthedocs.org/api/v3/search/?q=authentication"
```

### Scoped search example

Use fielded search syntax to scope by project:

```bash
curl "https://readthedocs.org/api/v3/search/?q=project:docs%20.readthedocs.yaml"
```
