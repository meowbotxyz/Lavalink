<div align="center">

# 🎵 Meow Bot — Lavalink Music Node

**High-Performance Standalone Audio Routing Engine powering Meow Bot**

[![Lavalink](https://img.shields.io/badge/Lavalink-v4.x-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://github.com/lavalink-devs/Lavalink)
[![Docker](https://img.shields.io/badge/Docker-Containerized-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
[![Java](https://img.shields.io/badge/Java-17%20%2F%2021-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)](https://www.oracle.com/java/)
[![Audio Engine](https://img.shields.io/badge/Audio-Lossless%20Stream-brightgreen?style=for-the-badge&logo=spotify&logoColor=white)](https://meowbot.xyz)
[![Status](https://img.shields.io/badge/Access-Private%20%2F%20Internal-red?style=for-the-badge&logo=git&logoColor=white)](LICENSE)

[🌐 Web Dashboard](https://meowbot.xyz) • [💬 Support Server](https://discord.gg/PaqFDgWe4J) • [➕ Invite Bot](https://discord.com/oauth2/authorize?client_id=1491052906496131296)

---

</div>

> **Notice:** This repository contains the standalone audio server configuration and containerized deployment workflow for **Meow Bot**. Network endpoints and authentication secrets are strictly confidential.

---

## 📌 System Overview

This dedicated Lavalink node isolates heavy multimedia decoding and stream extraction from the core bot process:
* **Offloaded Audio Processing:** Prevents audio transcoding from blocking the Discord Gateway event loop.
* **Multi-Source Support:** Streams audio from YouTube, Deezer, Spotify, SoundCloud, Bandcamp, and direct HTTP streams.
* **Binary Testing & Stability:** Includes automated source plugin compatibility verifications to guarantee continuous uptime across upstream API updates.

---

## 🗂️ Repository Directory Structure

```text
Meow-Lavalink/
├── Dockerfile                                    # Multi-stage container build definition
├── README.md                                     # Technical node documentation
├── YoutubeRestHandlerBinaryCompatibilityTest.java # Binary compatibility test suite for YouTube source
└── application.yml                               # Core Lavalink server configuration & plugin mappings

```
## ⚙️ Configuration (application.yml)
The server configuration defines plugins, network port bindings, and audio filter pipelines:
```yaml
server:
  port: ${PORT:2333}
  address: 0.0.0.0

lavalink:
  plugins:
    # Plugin YouTube được cộng đồng lavalink-devs duy trì, thay cho source cũ đã bị deprecated.
    # Version hiện tại (theo trang Releases bạn vừa check): 1.18.2
    # Nếu về sau có bản mới hơn, xem tại: https://github.com/lavalink-devs/youtube-source/releases
    - dependency: "dev.lavalink.youtube:youtube-plugin:1.18.2"
      repository: "https://maven.lavalink.dev/releases"

  server:
    password: "matkhau_cua_ban_123"
    sources:
      youtube: false
      soundcloud: true
      bandcamp: true
      twitch: true
      vimeo: true
      http: true
      local: false
    bufferDurationMs: 400
    playerUpdateInterval: 5

plugins:
  youtube:
    enabled: true
    allowSearch: true
    allowDirectVideoIds: true
    allowDirectPlaylistIds: true
    clients:
      - WEB            # Search + phát bình thường (không OAuth, đủ cho hầu hết video)
      - ANDROID_MUSIC   # Dự phòng thêm cho search + phát bình thường
      - TV              # DUY NHẤT client hỗ trợ OAuth thật -> phát được cả video "requires login"
    oauth:
      enabled: true
      # Sau khi deploy, xem Deploy Logs — sẽ in ra link https://www.google.com/device + mã pairing.
      # Mở link đó, đăng nhập bằng acc Google PHỤ (không dùng acc chính), nhập mã, xác nhận.
      # Sau khi xong, log in ra "refreshToken": "...". Copy giá trị đó dán vào dòng dưới rồi
      # deploy lại 1 lần nữa, để lần sau khỏi phải pairing lại mỗi khi container rebuild.
      # refreshToken: ""

logging:
  level:
    root: INFO
    lavalink: INFO

```
## 🐳 Docker Deployment
The containerized workflow handles Java runtime dependencies and plugin caching automatically.
### 1. Build the Docker Image
```bash
docker build -t meow-lavalink:latest .

```
### 2. Run the Container
```bash
docker run -d \
  --name meow-lavalink \
  -p 2333:2333 \
  --restart unless-stopped \
  meow-lavalink:latest

```
### 3. Check Container Logs
```bash
docker logs -f meow-lavalink

```
## 🧪 Compatibility Verification
The repository includes YoutubeRestHandlerBinaryCompatibilityTest.java to test binary compatibility with the YouTube plugin REST API wrapper:
 * Validates plugin classpath bindings against current Lavalink binary releases.
 * Ensures non-breaking changes when updating plugin dependencies.
## 🔌 Bot Integration (config/music.js)
Configure the node client inside Meow Bot (using Poru, Kazagumo, or Shoukaku):
```javascript
module.exports = {
  nodes: [
    {
      name: "Meow-Production-Node",
      host: "127.0.0.1",
      port: 2333,
      password: "YOUR_SECURE_LAVALINK_PASSWORD",
      secure: false
    }
  ],
  defaultSearchEngine: "youtube"
};

```
## 👥 Core Team & Infrastructure
<div align="center">
| Engineer | Role | Responsibilities |
|---|---|---|
| **Ws ZieeLord** (@4qg1) | **Lead Architect** | Container Architecture, Server Infrastructure & Web Dashboard Sync |
| **NNK** (@nnk_cool1) | **System Integrator** | Bot Music Client Integration, Audio Filter Tuning & Performance |
</div>
<div align="center">
Copyright © 2026 **Ws ZieeLord & NNK**. All rights reserved.
*Confidential internal deployment assets. Do not distribute.*
</div>