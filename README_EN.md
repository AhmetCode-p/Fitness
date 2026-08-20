# Forge — Weekly Workout Program

Forge is a serverless fitness app that runs entirely in the browser. Create weekly workout programs, track your progress, view your statistics, and share any program with a single code.

## Features

- **Welcome screen**: An animated FORGE landing page on first visit — code input, "Create Plan" and "Plan Reader" buttons.
- **7-day program wizard**: Easily build a program by adding a muscle group (tag) and exercises for each day. Empty days are marked as **rest days**.
- **TR / EN interface**: Switch between Turkish and English with the toggle in the top-left.
- **Workout tracking**: Check off completed sets and log weights per exercise; progress is saved automatically.
- **Weekly auto-reset**: All checkmarks reset automatically every **Monday**; your logged weights are kept.
- **Statistics**: The "Statistics" button below the code area shows weekly / monthly completion rates, day-by-day / week-by-week / month-by-month charts, and a weekly **weight progression** chart when you click an exercise.
- **Program codes**: Convert a program into a single-line compressed code. Whoever receives the code pastes it into the site and loads the program in seconds.
- **QR sharing**: The Share button opens a modal with a QR code + native device sharing (WhatsApp, email, etc.) + copy options.
- **Reliable sharing**: Codes are shortened with LZ compression + a custom alphabet and protected by a `checksum` — a corrupted copy is detected instantly and the user gets a clear message.
- **Backward compatible**: Codes from older formats (`ANT1.`, `ANT2.`, `ANT4.`) still open.
- **Data stays on device**: All programs, progress and statistics history are stored in the browser's `localStorage` (no account needed, data never leaves the device).
- **Modern UI**: Liquid Glass effect, soft corners, DM Sans font and button animations.

---

## Quick Start

The project is serverless; just open the HTML file in a browser or publish it via GitHub Pages.

```
https://ahmetcode-p.github.io/Forge/forgev1.html
```

### Create a program

1. Open `forgev1.html`.
2. On the welcome screen hit **"Create Plan"**.
3. Enter a muscle group and exercises (name, sets, reps) for each day.
4. Hit **"Finish & Create"** — the program is saved.

### Track a program

- Tick the box next to each exercise to mark completed sets.
- Enter the weight you used next to each exercise.
- Checkmarks reset automatically every Monday; your weights are kept.

### View statistics

1. Click the **"Statistics"** button below the code area.
2. Use the **Weekly / Monthly** tabs to see completion-rate charts.
3. In the **Exercises** tab, click an exercise — its weekly weight progression chart opens.

### Share a program

1. With the program open, click the **"Share"** button below.
2. Scan the QR code with your phone, send it via **"Share via Device"** (WhatsApp, email, etc.) or copy it with **"Copy"**.
3. The recipient pastes the code into the **"Program code"** box on the site and hits **"Open Code"**.

---

## Code System (how it works)

The program is compressed as JSON with LZ and packed with a custom alphabet (URL-safe `A-Z a-z 0-9 - _ . ~`). This keeps the code both very short and safe to transport anywhere (links, messages, notes).

| Format | Description |
|--------|-------------|
| `ANT1.` | First version — plain base64 (2100+ chars) |
| `ANT2.` | Compressed with LZ + base64 |
| `ANT4.` | LZ + custom alphabet (URL-safe, ~680 chars) |
| `ANT5.` | ANT4 + integrity check (checksum) — current |

Compression gain (sample 4-day / 22-exercise program):

```
ANT1:  2101 chars
ANT2:   805 chars
ANT4:   681 chars
ANT5:   683 chars
```

---

## Files

| File | Description |
|------|-------------|
| `forgev1.html` | Main app: program builder + tracker + statistics + code sharing |
| `manifest.json` | PWA definition (home screen icon and theme color) |
| `favicon.png` | Browser tab logo |
| `icon.png` | Mobile home screen icon |
| `kod.txt` | Ready-to-share sample program code (ANT5) |
| `Program Kodu.txt` | Local copy of the sample code |

---

## Technologies

- Pure HTML + CSS + JavaScript (no external framework)
- [lz-string](https://github.com/pieroxy/lz-string) — LZ-based compression (embedded)
- [api.qrserver.com](https://goqr.me/api/) — QR code generation
- `localStorage` — data storage
- GitHub Pages — hosting

---

## Note

All data is stored in the browser, so clearing browser data deletes your programs. We recommend keeping the codes of important programs somewhere like `kod.txt` — pasting the code again brings the program back.