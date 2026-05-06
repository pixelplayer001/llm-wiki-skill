# Topic inventory — DeepSeek「Into the Unknown」PDF digest

**Source:** `d:\A\downloads\DeepSeek - Into the Unknown.pdf` (DeepSeek shared conversation export; AI-generated, for reference only.)

**Share link (reference):** [https://chat.deepseek.com/share/krcvr538zt632sy0c4](https://chat.deepseek.com/share/krcvr538zt632sy0c4) — automated fetch from tooling may return 403; this digest was produced from the **user-supplied** PDF export.

**Extraction:** Plain text extracted with `pypdf` from **320** PDF pages (~396k characters).

## Representative topic threads (condensed)

Grouped bullets for traceability (not an exhaustive transcript index):

- **Mobility / robotics:** 机器人小车单电机中央驱动 vs 四轮无刷独立驱动；麦克纳姆/全向轮；成本、控制复杂度、机动性、折中双电机差速。
- **Automotive / NEV:** 纯电/新能源常见布置（单电机、双电机四驱、三/四电机、轮毂电机展望）；「机械集中 vs 电子分布」趋势。
- **4WD / chassis:** 分时四驱 vs 全时四驱；分动箱、铺装路面干涉；整体桥 vs 独立悬架；止推杆、潘哈德/瓦特连杆；门桥；电动车分动箱讨论等。
- **Drones / FC:** Betaflight、INAV、ArduPilot、PX4 选型；Pixhawk 硬件；MCU 实时飞控与 Linux 协处理、MAVLink 协同。
- **GCS / dev:** 飞控 vs 地面站；Mission Planner、QGC、MAVProxy；Windows + WSL 编译运行 SITL、与 GCS 联调注意点。
- **Telemetry / IP:** RFD900 数传；多地面站、SysID、指令冲突与主从；串口服务器（迈威、Moxa）；串口 vs TCP/IP 端口类比。
- **FPV / payload:** FPV 与航拍相机；视频切换器共用图传 vs 双路图传；舵机云台与航拍云台；推重比 TWR、有效载荷估算、eCalc 等。
- **RC:** RC 车为何少见中央「飞控」；接收机、遥控器混控、陀螺仪救车；与无人机控制哲学对比；AM32 等上下文。
- **Language:** 英文 *convention* / *follows* / *adheres to* 措辞纠错一则。

## How “topics” were estimated

| Signal | Count | Note |
|--------|------:|------|
| PDF pages | 320 | Physical pagination of export |
| `This shared conversation…` / `This response is AI-generated` markers | 31 | Stitch points between export segments |
| Unique lines ending with `？` / `?` (heuristic, de-duplicated) | 304 | Includes many **assistant sub-headings** (e.g. “我应该怎么选？”), not only user turns |

**Interpretation:** Treat the corpus as **one long multi-thread technical Q&A** spanning vehicles, drones, RC, and a small English-usage aside. A conservative human-style count of **distinct discussion themes** is on the order of **90–120** (many short follow-ups on the same theme: e.g. 分动箱 → 整体桥 → 门桥 → 电调).

**Thematic clusters (for articles):** **8** articles in **5** top-level folders under **`raw/articles/`** (same directory as this `topic-inventory.md` in the example wiki).

## Article map

| Folder | Article | Themes covered |
|--------|---------|----------------|
| `raw/articles/mobility/` | `small-robot-drivetrain-single-vs-quad-bldc.md` | 机器人小车单电机 vs 四轮无刷独立驱动；麦克纳姆/全向轮；成本/控制/机动性权衡 |
| `raw/articles/mobility/` | `new-energy-vehicle-motor-layouts.md` | 新能源汽车单电机、双电机四驱、三/四电机、轮毂电机趋势 |
| `raw/articles/mobility/` | `four-wheel-drive-and-solid-axle-chassis.md` | 分时/全时四驱；整体桥 vs 独立悬挂；止推杆/多连杆；门桥；电动车分动箱等延伸问答 |
| `raw/articles/drones/` | `flight-controller-ecosystem.md` | 飞控选型 Betaflight / INAV / ArduPilot / PX4；Pixhawk 与 MCU vs Linux 协同 |
| `raw/articles/drones/` | `ground-station-mavlink-sitl-windows.md` | 地面站与飞控区别；Mission Planner / QGC；MAVLink；Windows+WSL 与 SITL 开发环境 |
| `raw/articles/drones/` | `telemetry-multigcs-serial-ip.md` | 数传、RFD900、串口服务器（迈威/Moxa）、多地面站、SysID；串口 vs IP 端口 |
| `raw/articles/drones/` | `fpv-video-payload-thrust-weight.md` | FPV 与航拍相机、视频切换器、双路图传；整机负载与推重比 TWR、eCalc 等 |
| `raw/articles/rc/` | `rc-car-control-vs-drone-flight-controller.md` | RC 车分散控制 vs 无人机集中飞控；接收机/陀螺仪；AM32 电调等 |
| `raw/articles/language/` | `english-technical-phrasing-convention.md` | 英文措辞纠错（convention / follows / adheres to） |

---

*Digest produced for repository `llm-wiki-skill`; not a substitute for the original PDF.*
