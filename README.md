# Dual-Engine Automation Skill

让OpenClaw智能体自动搭建双引擎（HEARTBEAT + CRON）自动化运营系统。

---

## 🚀 安装（暂未发布，手动安装）

### 方法1：手动复制（推荐）

```bash
# 1. 克隆仓库
git clone https://github.com/chovizzz/dual-engine-automation.git

# 2. 复制到工作区
cp -r dual-engine-automation ~/.openclaw/workspace/skills/

# 3. 验证安装
ls ~/.openclaw/workspace/skills/dual-engine-automation/
# 输出：SKILL.md README.md IMPLEMENTATION.md TEMPLATES.md EXAMPLE.md
```

### 方法2：直接下载

```bash
cd ~/.openclaw/workspace/skills/
curl -L https://github.com/chovizzz/dual-engine-automation/archive/main.tar.gz | tar xz --strip-components=1
```

> **注意**：此Skill暂未发布到ClawHub，需要手动安装。正式发布后将支持：
> ```bash
> clawdhub install dual-engine-automation
> ```

---

## 一句话描述

> **用户说需求 → Agent自动设计架构 → 生成所有文件 → 配置CRON → 系统启动**

---

## 使用方法

### 1. 启动Skill

```
@dual-engine-automation 我要搭建一个[场景]自动化系统：

监控需求：
- 每30分钟检查：[任务描述]

定时任务：
- 每天[时间]：[任务]
- 每天[时间]：[任务]

通知设置：
- 飞书群组：[chat:oc_xxx]
- 工作区路径：[绝对路径]

其他：
- [可选] 需要自动Git提交
- [可选] 需要发帖功能
```

### 2. Agent自动执行

Agent会自动完成：
- ✅ 解析需求 → 提取HEARTBEAT/CRON任务
- ✅ 设计架构 → 双引擎协作方案
- ✅ 创建文件 → 7个必需配置文件
- ✅ 配置CRON → 自动生成并添加任务
- ✅ 启动通知 → 发送成功消息

### 3. 系统运行

- **HEARTBEAT**：每30分钟自动扫描
- **CRON**：按预设时间执行深度任务
- **防重复**：状态管理避免冲突
- **通知**：重大发现自动发送到飞书

---

## 示例场景

### Reddit运营
```
我要搭建Reddit GEO运营系统：
- 每30分钟扫描r/TechSEO和r/GenEngineOptimization热点
- 每天09:00生成日报，22:00/02:00/08:00检查发帖
- 飞书通知到 chat:oc_xxx
- 工作区 /Users/name/reddit-ops
```

### 竞品监控
```
我要监控竞品动态：
- 每30分钟检查竞品网站价格和促销
- 每天早上9点生成竞品日报
- 飞书通知到 chat:oc_xxx
- 工作区 /Users/name/competitor-monitor
```

### 社媒管理
```
我要管理Twitter和LinkedIn：
- 每30分钟检查消息和@提及
- 每天10:00和15:00发布内容
- 飞书通知到 chat:oc_xxx
```

---

## 文件结构

Skill会自动创建：

```
workspace/
├── HEARTBEAT.md              # HEARTBEAT执行指令
├── SOUL.md                   # 智能体人设
├── AGENTS.md                 # 运营指南
├── memory/
│   ├── cron-execution-state.json    # 状态管理（防重复）
│   ├── content-calendar.md          # 内容日历（如需要发帖）
│   ├── post-performance-log.md      # 表现记录
│   └── learning/                    # 学习归档
└── [其他配置文件...]
```

---

## 双引擎机制

```
┌─────────────────────────────────────────┐
│              双引擎架构                  │
├─────────────────────────────────────────┤
│                                         │
│   HEARTBEAT          CRON               │
│   (每30分钟)        (定时执行)          │
│        │                │               │
│        ▼                ▼               │
│   ┌─────────┐      ┌─────────┐         │
│   │ 轻量检查 │      │ 深度任务 │         │
│   │ 扫描热点 │      │ 生成报告 │         │
│   │ 即时响应 │      │ 执行发帖 │         │
│   └────┬────┘      └────┬────┘         │
│        │                │               │
│        └───────┬────────┘               │
│                ▼                        │
│        ┌─────────────┐                  │
│        │  状态管理    │  ← 防重复       │
│        │  通知路由    │                  │
│        └─────────────┘                  │
│                                         │
└─────────────────────────────────────────┘
```

---

## 🔄 自我升级迭代（进化版）

系统不仅执行任务，还能**自我学习、自我优化、自我进化**：

```
执行 → 分析 → 决策 → 优化 → 更新 → 再执行
  ↑                                    ↓
  └──────────── 闭环迭代 ←─────────────┘
```

### 五层进化架构

| 层级 | 功能 | 说明 |
|------|------|------|
| **执行层** | 数据采集 | 记录每次执行数据 |
| **分析层** | 效果评估 | 分析执行效率、内容效果 |
| **决策层** | 策略优化 | 基于数据生成优化方案 |
| **更新层** | 自动优化 | 更新文档、调整配置 |
| **触发层** | 闭环验证 | 触发验证、持续迭代 |

### 自动优化示例

```
第1周：22:00发帖，记录效果数据
第2周：分析发现21:00互动率高40%
第3周：自动调整发帖时间到21:00
第4周：验证效果，确认提升35%
第5周：继续寻找下一个优化点...
```

### 启用自我进化

在需求中增加：
```
@dual-engine-automation 我要搭建系统：
- 每30分钟检查：[任务]
- 每天[时间]：[任务]
- 启用自我优化：每天20:30自动分析并优化
- 飞书通知到：[chat:oc_xxx]
```

详见 [`SELF_EVOLUTION.md`](SELF_EVOLUTION.md)

---

## 后续管理

搭建完成后，可以自然语言管理：

```
查看当前配置              → 列出所有CRON任务
再加一个下午3点的任务      → 添加CRON 15:00
把日报时间改到8点          → 更新CRON时间
暂停晚上10点的任务         → 禁用CRON任务
重置状态文件               → 重置为pending
```

---

## 文档索引

| 文档 | 内容 |
|------|------|
| `SKILL.md` | Skill使用说明 |
| `IMPLEMENTATION.md` | Agent实现指南 |
| `TEMPLATES.md` | 场景模板库（8个模板）|
| `SELF_EVOLUTION.md` | 自我升级迭代机制 |
| `EXAMPLE.md` | 完整示例 |
| `README.md` | 本文件 |

---

## 核心优势

1. **零配置**：用户只需描述需求，无需技术细节
2. **智能架构**：自动设计最优HEARTBEAT+CRON方案
3. **防重复**：内置状态管理机制
4. **开箱即用**：配置完成立即可运行
5. **可扩展**：随时添加/修改任务

---

## 适用场景

- ✅ Reddit/社媒运营
- ✅ 竞品监控
- ✅ 内容创作
- ✅ 客服支持
- ✅ 数据分析
- ✅ 任何需要"实时监控+定时任务"的场景

---

**本质**：把"手动复制配置"变成"对话式自动搭建"

---

*版本：v1.0*  
*创建：2026-02-14*
