# ClearChat Desktop + Web source

This repository contains the ClearChat React/Vite app plus an Electron wrapper to build a Windows installer.

## What the GitHub workflow builds
- `ClearChat-Setup-1.1.0.exe`: Windows installer artifact.
- `Web-ClearChat-Build`: built static website artifact (`dist/`).

## Get the Windows installer
1. Commit the repository to the `main` branch.
2. Open the repository's **Actions** tab.
3. Open the latest successful **Build ClearChat Desktop and Web** run.
4. Under **Artifacts**, download `ClearChat-Windows-Installer`.
5. Extract the downloaded artifact ZIP, then run `ClearChat-Setup-1.1.0.exe`.

## Local development
Install Node.js 22+, then run:
```bash
npm install
npm run dev
```
For a local desktop build:
```bash
npm run desktop
```
To build a Windows installer from Windows:
```bash
npm run dist:win
```

## Enable real online rooms and chat
This project uses Supabase. Create a Supabase project, run `supabase/schema.sql` in its SQL Editor, and configure the GitHub repository secrets:
- `VITE_SUPABASE_URL`
- `VITE_SUPABASE_ANON_KEY`

Use the Supabase publishable/anon key only; never use a service-role key in the client. The workflow passes those secrets at build time. If the secrets are absent, the app can build but its online features remain in demo/unconfigured mode.

## Important feature limits
The desktop app is a packaged version of the current ClearChat prototype, not a complete WhatsApp replacement. Real online messaging requires Supabase configuration and the schema to be applied. Voice recording is currently local preview rather than shared audio messaging. Event alarms work while the app is open; reliable alerts when the app is closed require a server-side push/scheduling system. A Windows installer is not an iOS/Android app. The website build can be hosted separately for browsers.


## If GitHub Actions fails
Open the failed `build-windows` job and expand the red step to see the exact error. The summary page's generic `exit code 1` message alone doesn't identify the underlying cause.
