# PhoneSpeaker 🔊

Stream audio from your laptop to any phone — in real-time, no app install needed.

<img width="515" height="446" alt="image" src="https://github.com/user-attachments/assets/ad70a714-78f4-4c68-b355-fb0c5aee345d" />

## How it works

- Your **laptop** captures system audio (or mic) and streams it via WebRTC
- Your **phone** opens a browser tab and plays the audio through its speaker
- A lightweight **Node.js server** handles the initial WebRTC handshake (signalling)
- After that, audio flows peer-to-peer — the server is barely involved

## Setup

```bash
git clone https://github.com/silasamoah/Sonno.git
```

```bash
cd Sonno
```

### 1. Install dependencies

```bash
npm install
```

### 2. Start the server

```bash
npm start
```

### 3. Open the sender on your laptop

```bash
http://localhost:3000/sender.html
```

### 4. Open the receiver on your phone

Your **laptop and phone must be on the same Wi-Fi network.**

Find your laptop's local IP (e.g. `192.168.1.42`) and open:

```bash
http://192.168.1.42:3000/receiver.html
```

Type **The code** shown on the sender page.

---

## Usage

1. On the **laptop sender page**:
   - Choose audio source: **System Audio** (everything playing) or **Microphone**
   - Click **Create Room & Go Live**
   - For system audio: in the screen-share picker, **check "Share audio"** ✅
   - A room code + QR code will appear

2. On the **phone receiver page**:
   - Enter the 6-character room code (or scan the QR)
   - Tap **Join** — audio starts playing immediately

3. Use the **volume slider** on the phone to adjust playback.

---

## Tips

- **System audio on Chrome**: You must share a browser tab or entire screen and check "Share audio" in the dialog. Only Chrome on desktop supports tab audio capture.
- **Latency**: Typically 50–150ms on a good local network — great for music, podcasts, calls.
- **Multiple phones**: You can connect as many phones as you want to the same room.
- **HTTPS for production**: If deploying beyond localhost, you'll need HTTPS (WebRTC requires it). Use [ngrok](https://ngrok.com) for quick testing: `ngrok http 3000`.

## Tech Stack

- **Signalling**: Node.js + `ws` (WebSocket)
- **Audio transport**: WebRTC `RTCPeerConnection`
- **Capture**: `getDisplayMedia()` for system audio, `getUserMedia()` for mic
- **Frontend**: Vanilla HTML/CSS/JS — no framework, no bundler
