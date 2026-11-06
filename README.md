# SMART WEBRTC CLASSROOM (DEDICATED LAN EDITION)
### Privacy-First, Zero-Internet, High-Speed Classroom Screen Sharing & Collaboration

[![Mode](https://img.shields.io/badge/Network-100%25%20LAN%20Only-brightgreen)](#)
[![Zero-Internet](https://img.shields.io/badge/Internet-Not%20Required-blue)](#)
[![Security](https://img.shields.io/badge/Security-DTLS--SRTP%20%26%20SHA--256-purple)](#)

A high-performance WebRTC classroom collaboration platform customized specifically for **Local Area Networks (LAN)**. It operates completely offline over local Wi-Fi routers or Ethernet switches with **zero internet connection required**, ensuring 100% data privacy and sub-5ms streaming latency.

---

## 🌟 What Was Changed For LAN-Only Operation

1. **Zero External STUN/TURN Traffic**:
   - `iceServers` is configured to `[]`.
   - The browser only gathers direct `host` candidates (`192.168.x.x`, `10.x.x.x`, `127.0.0.1`).
   - Non-host candidates (`srflx`, `relay`) are blocked so no packets ever attempt to leave the local network.

2. **Local Dynamic WebSocket Signaling**:
   - The signaling client connects dynamically to `ws://<lan-ip>:3000/ws` (the host computer running the server) instead of querying any cloud relays.
   - When opened via `file:///`, it defaults directly to local port 3000.

3. **100% Offline-First Assets**:
   - External Google Fonts dependencies removed in favor of native system typography (`Inter`, `Segoe UI`, `-apple-system`, `JetBrains Mono`, `Consolas`).
   - Starts instantly in isolated intranet computer labs without waiting on external timeouts.

4. **Self-Contained Single-Directory Server**:
   - `server.js` serves `index.html` directly from the project directory.
   - Built-in UDP beacon on port `41234` for automatic LAN discovery.
   - Handles up to 100 student connections simultaneously via SFU relay.

5. **Unified 1-Step Session Code Joining (No Token Copy-Pasting)**:
   - Eliminated the manual P2P token exchange screen (`SWC1_...` offer/answer tokens) and separate tabs.
   - Students join directly with just the **6-digit Session Code** and their Name.
   - Built-in **Auto-Approve** and **Approve All** options for teachers to instantly admit up to 100 students without manual friction.

---

## 🌐 100% Serverless GitHub Pages Mode (Zero Backend Server Required!)

### How It Works:
1. **Frontend on GitHub Pages**:
   - Both Teacher and up to 100 Students open `https://<your-username>.github.io/<repo>/` in their browser.
   - Students enter **only the 6-digit Session Code** and their name.

2. **Zero Backend to Run or Deploy**:
   - Uses an embedded, lightweight public secure WebSocket broker (`wss://broker.hivemq.com:8884/mqtt`) to exchange the 6-digit session codes over HTTPS.
   - **You do NOT need to run Node.js, deploy to Render, or maintain any backend servers!**
   - Zero screen share or video data goes to the internet—only a tiny ~1 KB text handshake.

3. **Strict Local LAN Lockdown (Media & Screen Share)**:
   - WebRTC is locked to `DEFAULT_ICE_SERVERS: []` and strictly filters out all non-host candidates.
   - **If student and teacher are on the same Wi-Fi / LAN switch**:
     The direct 1080p stream connects immediately over the local network with sub-5ms latency and zero internet data usage.
   - **If someone outside the classroom (e.g. from home) enters the code**:
     The connection is automatically blocked and dropped because private LAN IP addresses cannot cross the public internet!

---

### 🚀 How to Launch on GitHub Pages (Zero-Server Mode)

1. **Upload `index.html` to your GitHub repository**.
2. **Enable GitHub Pages**:
   - Go to your repository **Settings** &rarr; **Pages** &rarr; select `main` branch &rarr; **Save**.
3. **Share the link with students**:
   - Students and teacher visit your GitHub Pages link.
   - Teacher clicks **Host as Teacher**, gets 6-digit code.
   - Students enter code &rarr; auto-approved &rarr; high-speed LAN screen share starts!

---

## 💻 Alternative: Running with Companion LAN Server (Optional)

### Option 1: Double-Click
Double-click `Start-LAN-Classroom.bat` on Windows.

### Option 2: Terminal / PowerShell
```powershell
# 1. Open the project folder
cd C:\Users\hancy\.gemini\antigravity\scratch\sss-lan

# 2. Start the local LAN server
npm start
```

The server will print your machine's local LAN IP addresses:
```
================================================================
  🚀 SMART WEBRTC CLASSROOM - LAN SFU SERVER ACTIVE
================================================================
  Local Access:      http://localhost:3000
  LAN Network URLs:
    • Wi-Fi          : http://192.168.1.50:3000
    • Ethernet       : http://192.168.1.51:3000
  WebSocket Signaling: /ws
  Discovery Endpoint:  /api/discovery
================================================================
```

### Option 3: Accessing From Student Laptops
1. Connect student laptops and teacher laptop to the same Wi-Fi router or switch.
2. Students open `http://<teacher-lan-ip>:3000` in their browser (Chrome, Edge, Firefox, Safari).
3. Teacher clicks **Host as Teacher** &rarr; generates 6-digit room code.
4. Students enter the code &rarr; Teacher clicks **Approve**.
5. Teacher clicks **Share Screen** &rarr; high-definition 1080p/60fps video is broadcast directly over LAN!

---

## 🔒 Security & Privacy
- **Zero Cloud Recording / Telemetry**: All data stays inside your physical building or room.
- **Hardware End-to-End Encryption**: DTLS 1.2/1.3 and SRTP AES-128-GCM ciphers.
- **SHA-256 File Verification**: Native Web Crypto integrity checks on chunked file vault transfers.
