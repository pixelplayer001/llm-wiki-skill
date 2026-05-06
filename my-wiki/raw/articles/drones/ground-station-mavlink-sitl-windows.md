# 地面站、MAVLink 与 Windows 上的 SITL 开发环境

**来源：** DeepSeek 对话导出 PDF 摘要（见 `raw/articles/topic-inventory.md`）。

**DeepSeek share (reference):** https://chat.deepseek.com/share/krcvr538zt632sy0c4 — digest from **user-supplied** PDF; original chat AI-generated.

## 飞控 ≠ 地面站

对话明确：**ArduPilot 是运行在机载飞控硬件上的固件**，不是地面站软件。地面站（GCS）跑在 PC/平板上，负责参数、航线、遥测与指令交互；二者经 **USB/数传** 等链路上的 **MAVLink** 协同。

列举的地面站包括 **Mission Planner**（Windows 为主、功能全）、**QGroundControl**（跨平台）、**MAVProxy**（开发者向）、以及部分移动端方案等。

## Windows + WSL 与 SITL

对话中大量篇幅涉及在 **Windows 上用 WSL** 编译与运行 **ArduPilot SITL**（软件在环仿真），并与桌面端 **Mission Planner** 联调：源码宜放在 **WSL 本地文件系统**而非 `/mnt/c/` 以减轻 IO 性能问题；可选 **VcXsrv** 等 X11 显示；并对比 **Cygwin** 等非首选路径。

## 实践提示

联调前需理清：**哪一端跑仿真机**、**哪一端打开 GCS**、**连接 URI（如 UDP 端口）** 是否与官方文档一致。
