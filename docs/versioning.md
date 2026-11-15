# Versioning

Semantic versioning, adapted to n8n workflows.

| Change | Bump | Example |
|---|---|---|
| Data table columns renamed or removed, a workflow replaced, or setup steps change | MAJOR | 0.3.0 → 1.0.0 |
| New workflow, channel or visible behaviour | MINOR | 0.1.0 → 0.2.0 |
| Bug fix or wording only | PATCH | 0.1.0 → 0.1.1 |

The version must match in three places: `package.json`, the top of `CHANGELOG.md` and the **Current version** line in `README.md`. Each release is published as a GitHub release with the changelog section as notes.

## Releasing workflow changes
1. Change the workflow in n8n and test it.
2. In n8n: **⋯ → Download** and save it over the matching file in `workflows/`.
3. Before committing, open the file and check it contains no credential values and no real customer data.
4. Update the changelog, version and decision records, then commit.
