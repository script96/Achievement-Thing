# Achievement-Thing

Achievement-Thing is a desktop app (built with **Wails + Go + Svelte**) that watches local achievement save files and shows toast notifications when a new achievement is unlocked.

## What it does

- Watches configured folders for supported achievement files (`.ini` and `.json` variants used by some Steam-related setups)
- Parses achievement state changes
- Detects newly unlocked achievements
- Looks up achievement metadata from the Steam Web API
- Sends a Windows-style notification with title, description, and icon

## How it works

1. On startup, the watcher service loads settings from:
   - `%LOCALAPPDATA%/Achievement-Thing/settings.json`
2. It scans configured folders for achievement files and stores the initial state.
3. It starts recursive filesystem watchers.
4. When a file changes, it:
   - extracts the game App ID from the file path
   - parses achievements
   - compares against previous state
   - sends notifications only for newly unlocked achievements
5. Steam achievement data and icons are cached under:
   - `%LOCALAPPDATA%/Achievement-Thing/cache`

## Development

### Run in dev mode

```bash
wails dev
```

### Build frontend only

```bash
cd frontend
npm ci
npm run build
```

### Build app package

```bash
wails build
```

## Project status

⚠️ **This project is still in active development.**

Current behavior and file format support may change as the app is improved.
