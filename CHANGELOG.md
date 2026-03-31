# Changelog

## 1.2.2

### Fixed

- Native module version mismatch errors (e.g., npx caching a better-sqlite3 build for a different Node.js version) now produce actionable diagnostics instead of the misleading "unable to open database file" message.
- `sanitizeError` regex no longer swallows diagnostic text after filesystem paths; NODE_MODULE_VERSION info is now preserved in error output.

### Added

- Startup validation: the server eagerly tests the better-sqlite3 native module via an in-memory database and exits with a clear message if there is a version mismatch.
- `formatToolError` now detects `NODE_MODULE_VERSION`, `dlopen`, and `MODULE_NOT_FOUND` errors and suggests `rm -rf ~/.npm/_npx` as a fix.
- `diagnosePath` helper provides detailed diagnostics (file existence, permissions, file size) when the database file cannot be opened.
- 12 new unit tests for error sanitization and error formatting.

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
