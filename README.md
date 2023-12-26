# renovate-config

To host the renovate config.

- `config.js` holds the self-hosted Renovate configuration so that Renovate knows what and how it should process.
- `renovate.json` in this repository ensures to receive Renovate updates.
- `default.json` holds the basic config for all repositories. It extends the presets by the renovate project defined in `renovate-schema.json`.
- Each repository can extend/alter this config by adding a `renovate.json` file to the root of the repository.

## Reusable presets

### Golang dependency group

What it does:

- Groups all Golang dependencies into one PR
  - Respects your repository's `separateMajorMinor` setting[^1]
- Runs `go mod tidy` before committing to ensure a clean `go.sum`[^2]

Usage:

```diff
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": [
    "local>gitea/renovate-config",
+   "local>gitea/renovate-config:go-deps"
  ]
}
```

### NPM dependency group

What it does:

- Groups all NPM dependencies[^3] into one PR
  - Respects your repository's `separateMajorMinor` setting[^1]
- Groups all NPM dev-dependencies[^3] into one PR
  - Respects your repository's `separateMajorMinor` setting[^1]

Usage:

```diff
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": [
    "local>gitea/renovate-config",
+   "local>gitea/renovate-config:npm-deps"
  ]
}
```

### Workflow dependency group

What it does:

- Groups all workflow dependencies into one PR
  - Respects your repository's `separateMajorMinor` setting[^1]

Usage:

```diff
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": [
    "local>gitea/renovate-config",
+   "local>gitea/renovate-config:workflow-deps"
  ]
}
```

### Security fixes

What it does:

- Bumps a dependency to resolve a vulnerability[^4]
  - Overrules any scheduling and grouping for that vulnerability

Usage:

```diff
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": [
    "local>gitea/renovate-config",
+   "local>gitea/renovate-config:security"
  ]
}
```

[^1]: [Renovate Docs: separateMajorMinor](https://docs.renovatebot.com/configuration-options/#separatemajorminor)
[^2]: [Renovate Docs: postUpdateOptions](https://docs.renovatebot.com/configuration-options/#postupdateoptions)
[^3]: [Renovate Docs: npm dependency types](https://docs.renovatebot.com/modules/manager/npm/#additional-information)
[^4]: [Renovate Docs: osv vulnerabilities](https://docs.renovatebot.com/configuration-options/#osvvulnerabilityalerts) and [Renovate Docs: vulnerabilityAlerts](https://docs.renovatebot.com/configuration-options/#vulnerabilityalerts)
