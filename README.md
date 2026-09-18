Dưới đây là toàn bộ nội dung file README.md hoàn chỉnh cho repository máy chủ Lavalink, đã được sửa triệt để lỗi hiển thị code, chuẩn hóa các thẻ đóng/mở HTML và bố trí lại hàng nút chuyển đổi trực quan:
```markdown
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
├── Dockerfile                                     # Multi-stage container build definition
├── README.md                                      # Technical node documentation
├── YoutubeRestHandlerBinaryCompatibilityTest.java # Binary compatibility test suite for YouTube source
└── application.yml                                # Core Lavalink server configuration & plugin mappings

```
## ⚙️ Configuration (application.yml)
The server configuration defines plugins, network port bindings, and audio filter pipelines:
```yaml
server:
  port: ${PORT:2333}
  address: 0.0.0.0

lavalink:
  plugins:
    - dependency: "dev.lavalink.youtube:youtube-plugin:1.18.2"
      repository: "[https://maven.lavalink.dev/releases](https://maven.lavalink.dev/releases)"

  server:
    password: "YOUR_SECURE_LAVALINK_PASSWORD"
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
      - WEB
      - ANDROID_MUSIC
      - TV

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
## 🔌 Bot Integration & Client Examples
<div align="center">
<img src="https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black" alt="JS" />
<img src="https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white" alt="TS" />
<img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Py" />
<img src="https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white" alt="Java" />
<img src="https://img.shields.io/badge/Go-00ADD8?style=for-the-badge&logo=go&logoColor=white" alt="Go" />
<img src="https://img.shields.io/badge/JSON-000000?style=for-the-badge&logo=json&logoColor=white" alt="JSON" />
</div>
<details open>
<summary><b>🟡 JavaScript / Node.js (<code>config/music.js</code>)</b> — <i>Poru, Kazagumo, Shoukaku, MagmaStream</i></summary>
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
</details>
<details>
<summary><b>🔵 TypeScript (<code>config/music.ts</code>)</b> — <i>Lavalink-Client, Fastlink</i></summary>
```typescript
export interface LavalinkNodeConfig {
  name: string;
  host: string;
  port: number;
  password: string;
  secure?: boolean;
}

export const musicConfig: { nodes: LavalinkNodeConfig[]; defaultSearchEngine: string } = {
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
</details>
<details>
<summary><b>🐍 Python (<code>config/music.py</code>)</b> — <i>Wavelink, Pomice, Mafic</i></summary>
```python
LAVALINK_CONFIG = {
    "nodes": [
        {
            "identifier": "Meow-Production-Node",
            "uri": "[http://127.0.0.1:2333](http://127.0.0.1:2333)",
            "password": "YOUR_SECURE_LAVALINK_PASSWORD",
            "inactive_timeout": 300,
        }
    ],
    "default_source": "youtube"
}

```
</details>
<details>
<summary><b>☕ Java (<code>config/LavalinkConfig.java</code>)</b> — <i>Lavalink-Client Java / JDA</i></summary>
```java
package config;

public class LavalinkConfig {
    public static final String HOST = "127.0.0.1";
    public static final int PORT = 2333;
    public static final String PASSWORD = "YOUR_SECURE_LAVALINK_PASSWORD";
    public static final String IDENTIFIER = "Meow-Production-Node";
}

```
</details>
<details>
<summary><b>🐹 Go (<code>config/music.go</code>)</b> — <i>Waterlink / Disgord</i></summary>
```go
package config

type LavalinkNode struct {
    Name     string
    Host     string
    Port     int
    Password string
    Secure   bool
}

var MeowAudioNode = LavalinkNode{
    Name:     "Meow-Production-Node",
    Host:     "127.0.0.1",
    Port:     2333,
    Password: "YOUR_SECURE_LAVALINK_PASSWORD",
    Secure:   false,
}

```
</details>
<details>
<summary><b>📄 Static JSON (<code>config/music.json</code>)</b> — <i>Universal JSON configuration</i></summary>
```json
{
  "lavalink": {
    "name": "Meow-Production-Node",
    "host": "127.0.0.1",
    "port": 2333,
    "password": "YOUR_SECURE_LAVALINK_PASSWORD",
    "secure": false,
    "defaultSearch": "youtube"
  }
}

```
</details>
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
```

```
