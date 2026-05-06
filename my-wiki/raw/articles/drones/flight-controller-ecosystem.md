# 无人机飞控生态：Betaflight、INAV、ArduPilot、PX4 与 Pixhawk

**来源：** DeepSeek 对话导出 PDF 摘要（见 `raw/articles/topic-inventory.md`）。

**DeepSeek share (reference):** https://chat.deepseek.com/share/krcvr538zt632sy0c4 — digest from **user-supplied** PDF; original chat AI-generated.

## 选型维度

对话按 **「可玩性 vs 专业性」** 将常见开源/半开源路线分为几类：

- **Betaflight** — FPV 穿越机、花飞事实标准；强调手动模式下的敏捷与滤波（如 RPM 滤波）；GPS 救援等多为**应急级**，不适合复杂自主任务。

- **INAV** — 在手动飞行与 **GPS 导航**（定点、返航、航线）之间折中；对固定翼支持较好；适合「想飞远一点、又要一定自主能力」的场景。

- **ArduPilot / PX4** — **工业与科研**常用：机型覆盖广、参数与日志体系深。ArduPilot 与 **Mission Planner** 深度绑定做配置与日志分析；PX4 与 **QGroundControl** 等现代地面站配合，在科研、仿真链路（如与 MATLAB/Simulink）上常被提及。

## Pixhawk 与算力架构

对话澄清 **Pixhawk 通常指硬件平台系列**（飞控板），上面运行 ArduPilot 或 PX4 等固件；并解释 **Cortex-M 实时飞控** 与 **Cortex-A/Linux 协处理器**（树莓派等）分工：前者保证硬实时控制回路，后者跑视觉、网络等重负载，双方经 **MAVLink** 等协同。

## 注意

产品型号与固件版本迭代快；选型请以官方文档与社区发布为准。
