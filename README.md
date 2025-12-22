# Read the Docs Skills

A collection of Agent Skills for interacting with Read the Docs APIs and services.

## What are Agent Skills?

Agent Skills are modular packages that extend AI agent capabilities. Each skill is a folder containing a `SKILL.md` file with instructions, plus optional supporting files like scripts and templates.

Skills are **model-invoked** — agents autonomously decide when to use them based on your request and the skill's description.

Learn more at [agentskills.io](https://agentskills.io)

## Available Skills

### Read the Docs Search API

Query the Read the Docs Search API to find documentation across millions of pages of hosted documentation.

- **Location**: `.claude/skills/readthedocs-search-api/`
- **Use when**: Searching documentation, finding related docs, finding API documentation, or gathering information about projects on Read the Docs
- **Base URL**: `https://readthedocs.org/api/v3/search/`

## Installation

Clone this repository and place it in your project:

```bash
git clone https://github.com/readthedocs/skills.git .claude/skills
```

Or add it as a submodule:

```bash
git submodule add https://github.com/readthedocs/skills.git .claude/skills
```

## Usage

Skills are automatically discovered by Claude and other compatible agents. Simply ask a question that matches a skill's description, and the agent will use it autonomously.

Example:
```
Can you find documentation on Django REST Framework authentication?
```

The Read the Docs Search API skill will activate and search the API for relevant documentation.

## Structure

```
.
├── README.md
└── .claude/skills/
    └── readthedocs-search-api/
        └── SKILL.md
```

## Contributing

To add a new skill:

1. Create a directory in `.claude/skills/` with a descriptive name
2. Add a `SKILL.md` file with YAML frontmatter and instructions
3. (Optional) Add supporting files like scripts or references
4. Test the skill with your agent
5. Submit a pull request

See [agentskills.io/specification](https://agentskills.io/specification) for the complete SKILL.md format specification.

## License

These skills are available under the MIT License. See LICENSE for details.

## Related Links

- [Agent Skills Home](https://agentskills.io)
- [Agent Skills Specification](https://agentskills.io/specification)
- [Read the Docs](https://readthedocs.org)
- [Read the Docs API Documentation](https://docs.readthedocs.io/en/stable/api/v3/)
