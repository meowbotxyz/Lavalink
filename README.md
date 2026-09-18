<div align="center">

# 🎵 Meow Bot — Lavalink Audio Node

**High-Performance Standalone Audio Routing Engine powering Meow Bot**

[![Lavalink](https://img.shields.io/badge/Lavalink-v4.x-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://github.com/lavalink-devs/Lavalink)
[![Java](https://img.shields.io/badge/Java-17%20%2F%2021-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)](https://www.oracle.com/java/)
[![Audio Engine](https://img.shields.io/badge/Audio-Lossless%20Stream-brightgreen?style=for-the-badge&logo=spotify&logoColor=white)](https://meowbot.xyz)
[![Hosting](https://img.shields.io/badge/Host-OriHost%20Engine-00C7B7?style=for-the-badge&logo=serverfault&logoColor=white)](https://ppanel.orihost.com)
[![Status](https://img.shields.io/badge/Node-Internal%20Private-red?style=for-the-badge&logo=git&logoColor=white)](LICENSE)

[🌐 Web Dashboard](https://meowbot.xyz) • [💬 Support Server](https://discord.gg/PaqFDgWe4J) • [➕ Invite Bot](https://discord.com/oauth2/authorize?client_id=1491052906496131296)

---

</div>

> **Chú ý:** Đây là repository cấu hình máy chủ âm thanh riêng tư (Lavalink v4 node) phục vụ hệ thống phát nhạc chất lượng cao cho **Meow Bot**. Cổng kết nối và mật khẩu được mã hóa và bảo mật nội bộ.

---

## 📌 Tổng Quan Hệ Thống (System Overview)

Máy chủ Lavalink này chịu trách nhiệm:
* Xử lý, giải mã và trích xuất luồng âm thanh độc lập với tiến trình bot chính để tránh nghẽn luồng sự kiện Discord Gateway.
* Hỗ trợ tìm kiếm và phát âm thanh từ nhiều nền tảng: YouTube, Deezer, Spotify, SoundCloud, Bandcamp và Direct HTTP links.
* Tích hợp các bộ lọc âm thanh nâng cao (Bassboost, Nightcore, 8D, Karaoke, Tremolo, Vaporwave).

---

## 🗂️ Cấu Trúc Thư Mục Node (Directory Layout)

```text
Meow-Lavalink/
├── plugins/                 # Plugins mở rộng (LavaSrc, YouTube Source Plugin)
│   ├── lavasrc-plugin.jar
│   └── youtube-plugin.jar
├── application.yml          # File cấu hình port, password, sources và filters
├── Lavalink.jar             # Lavalink standalone binary executable
├── start.sh                 # Bash script khởi động máy chủ (Linux/OriHost)
├── start.bat                # Batch script khởi động máy chủ (Windows)
└── README.md                # Tài liệu vận hành nội bộ
