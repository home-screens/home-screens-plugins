# Contributing to the Home Screens Plugin Registry

Thank you for your interest in building plugins for Home Screens! This guide covers how to create a plugin and submit it to the registry.

## Overview

Home Screens supports community plugins that add new module types to the display system. Plugins are loaded at runtime and appear alongside built-in modules in the editor.

The plugin system works as follows:

1. You build a plugin as a standalone package with a `manifest.json` and a bundled component.
2. You publish a release (tarball) to your GitHub repository.
3. You submit a PR to this registry repo adding your plugin entry to `plugins.json`.
4. Once merged, users can discover and install your plugin from the Plugin Store in the editor.

## Creating a Plugin

Start with the official template:

**[home-screens-plugin-template](https://github.com/home-screens/home-screens-plugin-template)**

The template includes:

- A working example plugin with a React component
- A `manifest.json` pre-configured with the required fields
- Build tooling to produce the plugin tarball
- Instructions for local development and testing

### Plugin Structure

Every plugin package must contain:

- **`manifest.json`** — Plugin metadata, validated against [`schema/manifest-schema.json`](schema/manifest-schema.json)
- **`dist/bundle.js`** — Bundled IIFE component code (the `exports.component` field in the manifest points to the export name)

### manifest.json

Key fields:

| Field | Description |
|---|---|
| `id` | Unique identifier, lowercase with hyphens (e.g. `my-widget`) |
| `name` | Human-readable name |
| `version` | Semver version string |
| `moduleType` | Bare identifier without prefix (e.g. `my-widget`). The app registers it as `plugin:my-widget` internally. |
| `category` | One of the 7 categories listed below |
| `icon` | A [Lucide](https://lucide.dev) icon name |
| `defaultConfig` | Default configuration values for new instances |
| `defaultSize` | Default grid size `{ w, h }` |
| `exports.component` | The export name of the React component (typically `"default"`) |

See the full schema at [`schema/manifest-schema.json`](schema/manifest-schema.json).

### Categories

Your plugin **must** use one of these exact category values:

- `Time & Date`
- `Weather & Environment`
- `News & Finance`
- `Knowledge & Fun`
- `Personal`
- `Media & Display`
- `Travel`

## Submitting a Plugin

### Prerequisites

Before submitting, make sure you have:

- [ ] A working plugin with a valid `manifest.json`
- [ ] At least one published release (a `.tar.gz` file attached to a GitHub release)
- [ ] The SHA-256 hash of the tarball
- [ ] A license file in your repo (MIT or compatible license recommended)

### Steps

1. **Fork** this repository.

2. **Add your plugin** to `plugins.json`. Insert a new entry in the `plugins` array:

   ```json
   {
     "id": "my-widget",
     "name": "My Widget",
     "description": "A brief description of what it does",
     "author": "your-github-username",
     "repo": "your-username/home-screens-plugin-my-widget",
     "license": "MIT",
     "category": "Knowledge & Fun",
     "tags": ["example", "widget"],
     "icon": "sparkles",
     "verified": false,
     "versions": [
       {
         "version": "1.0.0",
         "minAppVersion": "0.16.0",
         "releaseDate": "2026-03-20T00:00:00Z",
         "downloadUrl": "https://github.com/your-username/home-screens-plugin-my-widget/releases/download/v1.0.0/plugin.tar.gz",
         "sha256": "abc123...",
         "changelog": "Initial release"
       }
     ]
   }
   ```

3. **Validate** your entry against the schema:

   ```bash
   npx ajv validate -s schema/plugins-schema.json -d plugins.json --spec=draft2020
   ```

4. **Open a Pull Request** with a clear description of your plugin.

### Computing the SHA-256 Hash

On macOS:

```bash
shasum -a 256 plugin.tar.gz
```

On Linux:

```bash
sha256sum plugin.tar.gz
```

### Requirements

- The `id` field must be unique across all plugins in the registry.
- The `category` must be one of the 7 categories listed above. Do not invent new categories.
- The `verified` field must be set to `false` in your submission. The `verified` flag is set by maintainers only after review.
- Each version entry must include a valid `sha256` hash of the downloadable tarball.
- The `downloadUrl` must point to a publicly accessible file (typically a GitHub release asset).
- The `minAppVersion` must be `0.16.0` or later (the first version with plugin support).
- A license is required. MIT or Apache-2.0 are recommended for maximum compatibility.

## Review Process

After you open a PR:

1. A maintainer will review your submission for completeness and schema compliance.
2. The plugin will be installed and tested in a development environment.
3. If everything looks good, the PR will be merged and your plugin will appear in the Plugin Store.
4. Maintainers may set the `verified` flag after extended testing and review.

## Updating Your Plugin

To publish a new version:

1. Release a new tarball on your GitHub repo.
2. Open a PR adding the new version entry to the beginning of your `versions` array in `plugins.json`.
3. Include the new SHA-256 hash and download URL.

## Questions?

Open an issue in this repository or in the [main Home Screens repo](https://github.com/home-screens/home-screens).
