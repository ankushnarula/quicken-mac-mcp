# Changelog

## 1.0.2

### Fixed

- Server no longer crashes on startup when no `.quicken` bundle is found. The MCP server now starts successfully and returns helpful error messages at tool-call time instead of failing during initialization.
- When multiple `.quicken` bundles exist in `~/Documents`, the server auto-selects the most recently modified one instead of crashing with an ambiguous error.
- Documented that Quicken For Mac must be open for the server to work (Quicken encrypts its database when closed). Tool errors now detect the "no such table" symptom and tell the user to open Quicken.

### Changed

- Database connection is now lazy — deferred to first tool call rather than opening eagerly at startup.
- Tool error handling unified via `safeTool` wrapper, removing per-tool try/catch boilerplate.
- MCP server instructions now guide the calling agent to confirm the auto-detected Quicken file with the user and suggest setting `QUICKEN_DB_PATH` to disambiguate.

## 1.0.0

Initial release.
