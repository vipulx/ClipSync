# ClipSync

A real-time synced clipboard web application designed for Raspberry Pi. It works across your devices with support for Text, Links, Code snippets, and Files.

## 🚀 Setup Instructions

1. **Install Dependencies**
   Navigate to this directory on your Raspberry Pi and run:
   ```bash
   npm install
   ```

2. **Configuration**
   Copy the `.env.example` to `.env`:
   ```bash
   cp .env.example .env
   ```
   Edit `.env` to set your custom 4-digit PIN and session secret.
   *By default, the PIN is `1234`.*

3. **Start the Server**
   ```bash
   node server.js
   ```
   *The server will run on port 3000.*

---

## 🌐 WebSocket Integration

The app uses `socket.io` for instant cross-device updates without refreshing.
- The **Server (`server.js`)** spins up a `socket.io` instance sharing the same Express session, ensuring only authenticated connections are accepted.
- When an item is added or deleted via REST API or WebSocket, the server broadcasts `new_clip` or `delete_clip` events.
- The **Client (`public/app.js`)** listens to these events, dynamically mutating the DOM and emitting a notification.
- To prevent infinite loops with Auto Sync, the client checks the hash of incoming socket clips against the current clipboard state.

---

## 🚇 Cloudflare Tunnel Command

To expose your Raspberry Pi to the internet safely using Cloudflare Tunnel, run:

```bash
cloudflared tunnel --url http://localhost:3000
```

*Alternatively, if you have a named tunnel configured:*
```bash
cloudflared tunnel route dns [tunnel-name] clipboard.yourdomain.com
cloudflared tunnel run [tunnel-name]
```

## Features Complete:
- Auto-sync via `navigator.clipboard`
- Tag filtering
- Dynamic card rendering based on content
- Dark mode toggle based on OS class (with Tailwind)
- Haptic / Notification feedbacks.
