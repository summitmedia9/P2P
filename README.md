# p2p-connect

A serverless peer-to-peer web app built with **WebRTC**. Works in Arc, Chrome, Edge, and any Chromium-based browser — no backend, no plugins, no installs.

## Features

- 💬 **Real-time chat** via `RTCDataChannel`
- 📁 **File transfer** — drag-and-drop, chunked, direct peer-to-peer
- 📷 **Video/audio call** via `getUserMedia` + `RTCPeerConnection`
- 🔒 **No server** — data never leaves your browser (STUN only for NAT traversal)

## Usage

### Option A — Open locally
Just open `index.html` in your browser. No build step needed.

### Option B — Deploy to GitHub Pages
1. Fork this repo
2. Go to **Settings → Pages → Source: main / root**
3. Share the `https://your-username.github.io/p2p-connect` URL with your peer

### Connecting two peers

| Step | Tab A (Caller) | Tab B (Receiver) |
|------|---------------|-----------------|
| 1 | Click **Generate Offer** | — |
| 2 | Copy the offer JSON | Paste it → **Connect Peer** |
| 3 | — | Copy the answer JSON |
| 4 | Paste it → **Connect Peer** | — |
| 5 | 🟢 Connected! | 🟢 Connected! |

> Works between two browser tabs on the same machine, or across different devices on the same (or different) networks.

## How it works

```
Peer A                        Peer B
  |                              |
  |--- Offer SDP (copy/paste) -->|
  |<-- Answer SDP (copy/paste) --|
  |                              |
  |===== Direct P2P Channel =====|
        (chat / file / video)
```

- **Signaling** is done manually via copy-paste (no WebSocket server needed)
- **STUN** servers (Google's public ones) resolve public IPs for NAT traversal
- **Data channels** carry chat messages and binary file chunks
- **Media tracks** carry audio/video streams

## Tech used

| API | Purpose |
|-----|---------|
| `RTCPeerConnection` | Core P2P connection |
| `RTCDataChannel` | Chat + file transfer |
| `getUserMedia()` | Camera + microphone |
| STUN (Google) | NAT traversal |

## Project structure

```
p2p-connect/
├── index.html   # Everything — HTML, CSS, JS in one file
└── README.md
```

## Browser support

| Browser | Status |
|---------|--------|
| Arc | ✅ |
| Chrome 80+ | ✅ |
| Edge 80+ | ✅ |
| Firefox 75+ | ✅ |
| Safari 15.4+ | ✅ |

## License

MIT
