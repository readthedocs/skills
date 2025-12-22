---
name: readthedocs-search-api
description: Query the Read the Docs Search API to find documentation across projects and repositories. Use when searching documentation, finding related docs, or gathering information about projects on Read the Docs.
---

# Read the Docs Search API

Search across millions of pages of documentation hosted on Read the Docs using the public Search API.

## Overview

The Read the Docs Search API allows you to search documentation indexed by Read the Docs. This is useful for finding documentation, understanding project structures, and gathering information about projects hosted on the platform.

**Base URL**: `https://readthedocs.org/api/v3/search/`

## Authentication

The Search API is public and does not require authentication. You can make requests directly without API tokens.

## Search Endpoint

### Request

```
GET https://readthedocs.org/api/v3/search/?q={query}&page={page}
```

### Query Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `q` | string | **Required**. Search query (e.g., "authentication", "API docs") |
| `page` | integer | Page number for paginated results (default: 1) |

### Response Format

```json
{
  "count": 1234,
  "next": "https://readthedocs.org/api/v3/search/?q=query&page=2",
  "previous": null,
  "results": [
    {
      "id": "project-name:doc-title",
      "project": "project-name",
      "version": "latest",
      "title": "Documentation Title",
      "path": "/en/latest/path/to/page.html",
      "domain": "project-name.readthedocs.io",
      "highlight": "snippet of matching <mark>text</mark>...",
      "blocks": [
        {
          "id": "section-id",
          "title": "Section Title",
          "path": "/path#section-id"
        }
      ]
    }
  ]
}
```

### Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `count` | integer | Total number of results |
| `next` | string | URL for next page (null if no more pages) |
| `previous` | string | URL for previous page (null if first page) |
| `results` | array | Array of search result objects |

### Result Object Fields

| Field | Type | Description |
|-------|------|-------------|
| `id` | string | Unique result identifier (project:title) |
| `project` | string | Project slug/name |
| `version` | string | Documentation version (e.g., "latest", "stable") |
| `title` | string | Page title |
| `path` | string | URL path to the documentation |
| `domain` | string | Read the Docs domain for the project |
| `highlight` | string | HTML snippet showing matched text with `<mark>` tags |
| `blocks` | array | Sections within the page that match the query |

## Usage Examples

### Basic Search

Search for "authentication" across all documentation:

```bash
curl "https://readthedocs.org/api/v3/search/?q=authentication"
```

### Search with Pagination

Get the second page of results:

```bash
curl "https://readthedocs.org/api/v3/search/?q=API&page=2"
```

### Search Specific Project

To find documentation for a specific project, use the project name in your query:

```bash
curl "https://readthedocs.org/api/v3/search/?q=project:django+forms"
```

### Parse Results Programmatically

Example parsing search results:

```python
import requests
import json

response = requests.get(
    "https://readthedocs.org/api/v3/search/",
    params={"q": "REST API"}
)

data = response.json()
for result in data['results']:
    print(f"Project: {result['project']}")
    print(f"Title: {result['title']}")
    print(f"Domain: {result['domain']}")
    print(f"Path: {result['path']}")
    print("---")
```

## Best Practices

### Query Formulation

- **Be specific**: Use detailed keywords for better results (e.g., "JWT authentication" instead of "auth")
- **Use project names**: Prefix with project name for focused searches (e.g., "django:ORM")
- **Handle quotes**: Wrap multi-word phrases in quotes for exact matches

### Rate Limiting

- The API has reasonable rate limits for public use
- If you receive 429 responses, implement exponential backoff
- Cache results when possible to reduce API calls

### Error Handling

```python
import requests

try:
    response = requests.get(
        "https://readthedocs.org/api/v3/search/",
        params={"q": "query"},
        timeout=10
    )
    response.raise_for_status()
    results = response.json()
except requests.exceptions.RequestException as e:
    print(f"Search failed: {e}")
```

## Common Use Cases

### Find Documentation for a Topic

```bash
curl "https://readthedocs.org/api/v3/search/?q=websockets"
```

### Search Within a Specific Project

```bash
curl "https://readthedocs.org/api/v3/search/?q=django+middleware"
```

### Get All Results for a Query

Handle pagination to retrieve all results:

```python
def get_all_results(query):
    all_results = []
    page = 1
    while True:
        response = requests.get(
            "https://readthedocs.org/api/v3/search/",
            params={"q": query, "page": page}
        )
        data = response.json()
        all_results.extend(data['results'])
        if not data['next']:
            break
        page += 1
    return all_results
```

## Response Codes

| Code | Meaning |
|------|---------|
| 200 | Success - Results returned |
| 400 | Bad Request - Invalid query parameters |
| 429 | Rate Limited - Too many requests |
| 503 | Service Unavailable - Temporary issue |

## Limitations

- Results are limited to publicly available documentation
- Private documentation is not included in search results
- Search index updates may have a slight delay (typically seconds to minutes)
- Maximum query length is subject to URL constraints

## Tips for Using This Skill

When searching documentation:

1. **Start with broad queries** if you're unsure of the exact terminology
2. **Review the highlights** in results to understand context
3. **Check multiple results** - there may be relevant documentation in different projects
4. **Use project information** to navigate to the full documentation
5. **Cache results** when building tools that make multiple searches

## Examples

### Finding REST API Documentation

```
Search: "REST API pagination"
Result: Django REST Framework pagination docs
Domain: django-rest-framework.org
```

### Finding Security Best Practices

```
Search: "password hashing best practices"
Result: Multiple frameworks with security guidelines
```

### Locating Version-Specific Documentation

```
Search: "deprecation warnings version 2.0"
Result: Release notes and migration guides
```
