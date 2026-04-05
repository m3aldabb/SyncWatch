# SyncWatch

A minimal web app for **watching together in sync**: two people join the same room and share play, pause, skip back, and skip forward actions in real time. The UI is a phone-friendly “remote” you can add to your home screen as a simple PWA.

**Live:** [https://syncwatch-three.vercel.app](https://syncwatch-three.vercel.app)

## Features

- **Rooms** — Create a room or join with a 4-character code (no accounts).
- **Presence** — See when your partner is connected (heartbeat + visibility handling so screen lock does not strand you as “offline” forever).
- **Shared controls** — Play/pause and ±10s; both sides see toasts and a rough latency hint when the partner acts.
- **Recent rooms** — Last few codes stored locally in the browser for quick re-entry.

## Stack

- Single-page **static** app: `index.html` (inline CSS and JavaScript).
- **[Firebase Realtime Database](https://firebase.google.com/docs/database)** (compat SDK) for rooms, member presence, and command messages.
- **[Web App Manifest](https://developer.mozilla.org/en-US/docs/Web/Manifest)** (`manifest.json`) for installable / standalone behavior.

## Local development

Serve the folder as static files (any HTTP server works). Examples:

```bash
python3 -m http.server 8080
```

Then open `http://localhost:8080`.

> **Note:** `manifest.json` references `/icon.png`. Add a `icon.png` at the repo root (e.g. 192×192 and 512×512 as noted in the manifest) if you want proper PWA icons; without it, installs may show a broken icon.

## Firebase

The app expects a Firebase project with **Realtime Database** enabled. Client configuration lives in the `firebase.initializeApp({ ... })` block in `index.html`.

You should configure **[Realtime Database security rules](https://firebase.google.com/docs/database/security)** for production (the default wide-open rules are not suitable for public apps). Typical patterns restrict writes to authenticated users or use validation rules that match your threat model.

## Deployment

The project is set up for **[Vercel](https://vercel.com/)** as a static site: deploy the repository root; the entry is `index.html`.
