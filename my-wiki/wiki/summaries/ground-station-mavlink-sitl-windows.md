---
title: ground-station-mavlink-sitl-windows
type: summary
created: 2026-05-07
updated: 2026-05-07
sources: [ground-station-mavlink-sitl-windows]
tags: [deepseek, mavlink, gcs, sitl]
---

# ground-station-mavlink-sitl-windows

> Source: `raw/articles/drones/ground-station-mavlink-sitl-windows.md`.

## Takeaways

- **飞控固件 ≠ 地面站**；Mission Planner / QGC 等与机载栈经 **MAVLink** 交互。  
- **Windows + WSL** 跑 ArduPilot **SITL**，桌面开 GCS 联调；源码宜放 WSL 本地盘以减轻 IO 瓶颈。  
- 联调关键是 URI/端口与角色分工清晰。

## See

- [[DeepSeek Into the Unknown Digest]]
