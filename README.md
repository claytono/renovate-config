# renovate-config

The Renovate settings Clayton's repositories share. Each repository extends
this preset and keeps only what is particular to it:

```json
{
  "extends": ["github>claytono/renovate-config"]
}
```

A change here reaches every repository on its next Renovate run, with no pull
request in each one. Before merging one, check the preset with
`renovate-config-validator --no-global default.json`, then point infra's
config at the branch
(`github>claytono/renovate-config#BRANCH`) and run `scripts/renovate-dryrun`
there.

The preset extends claytono/renovate-docker-datasource, which dates Docker
image tags so that the 14-day wait works for them; that repository's README
covers what it needs. A repository can leave it out:

```json
{
  "extends": ["github>claytono/renovate-config"],
  "ignorePresets": ["github>claytono/renovate-docker-datasource"]
}
```

Rules in a repository come after the preset's, so a repository overrides a
setting by setting it again. For example, infra holds pre-commit hook updates
for manual review:

```json
{
  "extends": ["github>claytono/renovate-config"],
  "packageRules": [
    {
      "matchManagers": ["pre-commit"],
      "automerge": false
    }
  ]
}
```
