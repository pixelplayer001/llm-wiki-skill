# 数传、多地面站、串口服务器与「串口 vs IP 端口」

**来源：** DeepSeek 对话导出 PDF 摘要（见 `raw/articles/topic-inventory.md`）。

**DeepSeek share (reference):** https://chat.deepseek.com/share/krcvr538zt632sy0c4 — digest from **user-supplied** PDF; original chat AI-generated.

## 多地面站同一架机

对话讨论：**技术上**多台电脑经网络访问同一数传链路可行，但 **MAVLink 本身不提供完善的多主仲裁**；需通过 **SysID**、主从席位、权限设计或硬件上的 **优先级/交换** 避免指令冲突。工业场景提到 **串口交换机** 一类思路：为飞控链路设更高优先级、做端口级会话与回传分发。

## 串口服务器与 RFD900

针对 **RFD900** 等电台，对话比较 **迈威（Mport3102 / Mport3208 等）** 与 **Moxa NPort** 系列：路数、隔离、虚拟串口（RealCOM）、TCP Server 多会话、SSL/SSH、断网缓存（SD 卡）等差异，并提醒 **TTL vs RS232/RS485 电平匹配**、波特率一致、独立供电等工程细节。

## 串口与 TCP 端口

用类比说明：**串口**像独占物理线路的端到端管道；**IP 端口**是在网络地址上的逻辑通道，可多路复用、路由与加密。地面站软件既可用 **虚拟 COM**，也可用 **TCP 客户端** 直接指到服务器 IP:port。
