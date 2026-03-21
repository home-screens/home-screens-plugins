# Home Screens Plugin Registry

The curated plugin registry for [Home Screens](https://github.com/home-screens/home-screens), a smart display system for Raspberry Pi.

This repository contains the plugin catalog that the Home Screens app fetches to discover and install community plugins. The app reads the registry from:

```
https://raw.githubusercontent.com/home-screens/home-screens-plugins/main/plugins.json
```

## Structure

```
plugins.json                   # The plugin catalog (list of all registered plugins)
schema/
  plugins-schema.json          # JSON Schema for plugins.json
  manifest-schema.json         # JSON Schema for a plugin's manifest.json
```

### plugins.json

The registry file listing all available plugins with their metadata, versions, and download URLs. Validated by `schema/plugins-schema.json`.

### manifest-schema.json

Every plugin ships a `manifest.json` in its package. This schema defines the required structure, including module type, default config, default size, and exports. Validated by `schema/manifest-schema.json`.

## Categories

Plugins must belong to one of the following categories:

- **Time & Date** — Clocks, calendars, countdowns
- **Weather & Environment** — Weather, air quality, sunrise/sunset
- **News & Finance** — News feeds, stocks, crypto
- **Knowledge & Fun** — Trivia, quotes, word of the day
- **Personal** — Todo lists, meal planners, chore charts
- **Media & Display** — Photo slideshows, images, iframes
- **Travel** — Traffic, transit, maps

## Contributing

Want to publish a plugin? See [CONTRIBUTING.md](CONTRIBUTING.md) for submission guidelines.

## License

MIT
