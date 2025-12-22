---
name: readthedocs-search-api
description: Query the Read the Docs Search API to find documentation across projects and repositories. Use when searching documentation, finding related docs, finding API documentation, or gathering information about projects on Read the Docs.
metadata:
  source: "https://github.com/readthedocs/readthedocs.org/pull/12601"
---

# Read the Docs Search API

Query the public Read the Docs Search API to find documentation across millions of pages.

## Step-by-step instructions

### 1. Make a search request

Query the API using:
```
GET https://readthedocs.org/api/v3/search/?q={query}&page={page}
```

Required parameters:
- `q`: Your search query (e.g., "authentication", "API pagination")
- `page`: Result page number (default: 1)

### 2. Parse the response

The API returns JSON with this structure:
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

### 3. Handle pagination

If there are more results, use the `next` URL to fetch the next page. Continue until `next` is null.

## Examples

### Search for authentication documentation
```bash
curl "https://readthedocs.org/api/v3/search/?q=authentication"
```

### Search with pagination
```bash
curl "https://readthedocs.org/api/v3/search/?q=API&page=2"
```

### Parse results with Python
```python
import requests

response = requests.get(
    "https://readthedocs.org/api/v3/search/",
    params={"q": "REST API"}
)

data = response.json()
for result in data['results']:
    print(f"{result['project']}: {result['title']}")
    print(f"  Domain: {result['domain']}")
    print(f"  Path: {result['path']}")
```

### Get all paginated results
```python
def search_all(query):
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

## Common edge cases

**No authentication required**: The Search API is public and does not require API keys or authentication.

**Rate limiting**: The API applies reasonable rate limits. If you receive HTTP 429, implement exponential backoff.

**Private documentation excluded**: Only publicly available documentation is searchable. Private projects are not included.

**Search delay**: The search index updates with a slight delay. New documentation may not appear immediately.

**Empty results**: If a query returns no results, try simpler keywords or browse the project directly on Read the Docs.
