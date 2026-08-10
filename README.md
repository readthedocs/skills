# Read the Docs Skills

A collection of Agent Skills for interacting with Read the Docs APIs and services.

**Warning:** These skills can modify production Read the Docs data. Use with caution and review commands that will be run carefully.

## Documentation

Official documentation lives in the Read the Docs docs:
https://docs.readthedocs.com/platform/latest/reference/agent-skills.html

## Available skills

- **[Read the Docs API](skills/readthedocs-api/SKILL.md)**: API v3 client guidance for building requests and integrations.
- **[Read the Docs Config Writer](skills/readthedocs-write-config/SKILL.md)**: Create or update ``.readthedocs.yaml`` files for Sphinx and MkDocs.
- **[Read the Docs Search API](skills/readthedocs-search-api/SKILL.md)**: Query documentation across projects and versions.
- **[Read the Docs Project Manager](skills/readthedocs-project-manager/SKILL.md)**: Create projects, trigger builds, and sync versions.
- **[Read the Docs Redirects Manager](skills/readthedocs-redirects-manager/SKILL.md)**: List, create, update, and delete redirects.
- **[Read the Docs Build Failure Triage](skills/readthedocs-build-failure-triage/SKILL.md)**: Analyze build failures using logs and config context.
- **[Read the Docs Build Optimization](skills/readthedocs-build-optimization/SKILL.md)**: Troubleshoot and speed up slow documentation builds.
See the official docs for full descriptions and usage examples.

## Contributing
To add a new skill:

1. Create a directory under `skills/` with a descriptive name.
2. Add a `SKILL.md` file with YAML frontmatter and instructions.
3. (Optional) Add supporting files like scripts or references.
4. Test the skill with your agent.
5. Submit a pull request.

## License

MIT. See [LICENSE](LICENSE).
Pathum25 
