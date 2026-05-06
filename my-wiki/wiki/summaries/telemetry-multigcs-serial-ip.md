---
title: telemetry-multigcs-serial-ip
type: summary
created: 2026-05-07
updated: 2026-05-07
sources: [telemetry-multigcs-serial-ip]
tags: [deepseek, telemetry, serial, mavlink]
---

# telemetry-multigcs-serial-ip

> Source: `raw/articles/drones/telemetry-multigcs-serial-ip.md`.

## Takeaways

- 多地面站共享数传需 **SysID/主从/优先级** 设计，MAVLink 缺省仲裁有限。  
- **串口服务器**（迈威/Moxa 等）可把 RFD900 等电台接入局域网；注意 **TTL/RS232/RS485** 与波特率。  
- **串口**近似独占管道；**TCP 端口**为可路由的逻辑通道，可用虚拟串口或直连 TCP。

## See

- [[DeepSeek Into the Unknown Digest]]
