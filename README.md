# Shaka Player

A single-file, browser-based video player built on [Shaka Player](https://github.com/google/shaka-player). Open `index.html` directly in any modern browser — no server or build step required.

## Features

### URL Input
- Paste any **DASH** (`.mpd`) or **HLS** (`.m3u8`) stream URL and press **Enter** or click **Load**
- **Demo** button loads a built-in sample stream instantly
- Supports live and VOD streams

### URL History
- Every URL you load is saved automatically to `localStorage`
- Focus the URL input to see all previously used URLs, newest first
- Type to **filter** the list in real-time — matching text is highlighted
- Click any history entry to fill the input and start playback immediately
- **×** button removes a single entry
- **Clear all history** footer wipes the entire list
- Stores up to 30 entries; persists across sessions and page reloads
- Keyboard-navigable: `↓` from the input enters the list, `↑`/`↓` moves between entries, `Enter` loads, `Esc` closes

### Playback Controls
All controls appear as an overlay at the bottom of the player. They fade in on mouse movement and stay visible while paused.

| Control | Description |
|---------|-------------|
| Play / Pause | Button or click anywhere on the video |
| Progress bar | Click or drag to seek; shows buffered range in grey and played range in red |
| Volume | Hover the speaker icon to reveal a scrubber; drag to set level |
| Mute | Click the speaker icon to toggle mute |
| Time display | Shows `current / total` duration |
| Quality selector | Dropdown populated from the manifest; defaults to **Auto** (ABR) |
| Fullscreen | Expands the player to fill the screen |

### Fullscreen
- Click the fullscreen button or press **F**
- The entire player (video + controls) goes fullscreen — the URL bar is hidden
- Controls still appear on mouse movement while fullscreen
- Press **F** or **Esc** to exit

### Keyboard Shortcuts

| Key | Action |
|-----|--------|
| `Space` or `K` | Play / Pause |
| `→` | Seek forward 10 seconds |
| `←` | Seek back 10 seconds |
| `↑` | Volume +10% |
| `↓` | Volume −10% |
| `M` | Toggle mute |
| `F` | Toggle fullscreen |
| `0` – `9` | Seek to 0% – 90% of total duration |
| `?` | Toggle the shortcuts reference panel |
| `Esc` | Close shortcuts panel / exit fullscreen |

Keyboard shortcuts are suppressed while the URL input is focused so typing a URL works normally.

### Quality Selection
- After a stream loads the quality dropdown is populated with every resolution available in the manifest (e.g. 360p, 720p, 1080p, 4K)
- **Auto** lets Shaka's adaptive bitrate (ABR) algorithm pick the best quality for current bandwidth
- Selecting a resolution disables ABR and switches to the highest-bitrate track at that height

### Buffering
- Forward buffer goal: **5 minutes**
- Buffer behind playhead kept: **1 minute**
- A spinner appears while Shaka is buffering and disappears when playback resumes

### Error Diagnostics
The player shows an inline error panel with actionable guidance rather than a raw error code.

| Situation | Message shown |
|-----------|--------------|
| HTTPS stream with self-signed cert (status 0) | Explains the SSL cert issue and links directly to the stream URL so you can accept the cert in a new tab |
| CORS blocked (status 0, HTTP stream) | Explains that the server needs `Access-Control-Allow-Origin: *` |
| HTTP 403 | Suggests the stream requires authentication/tokens |
| HTTP 404 | Flags the manifest path as not found |
| Manifest parse error | Reports the Shaka error code and confirms the format expected |
| Request timeout | Suggests checking network / server health |

### On-Screen Display (OSD)
Every keyboard action briefly shows a confirmation message in the centre of the video (e.g. `+10s`, `Volume 70%`, `Muted`) so you always know what happened.

## Usage

```
# No installation needed — just open the file
open index.html        # macOS
xdg-open index.html    # Linux
start index.html       # Windows
```

For streams on HTTPS origins with self-signed certificates, open the stream URL in a separate tab first, accept the security warning, then load it in the player.

## Browser Support

Any browser supported by Shaka Player 4.x:

- Chrome 80+
- Firefox 80+
- Safari 14+
- Edge 80+

## Dependencies

- [Shaka Player 4.3.7](https://github.com/google/shaka-player) — loaded from cdnjs, no npm install needed
