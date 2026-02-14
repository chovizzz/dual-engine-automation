---
name: dual-engine-automation
description: Auto-setup OpenClaw dual-engine (HEARTBEAT + CRON) automation system. Describe your monitoring, scheduling, social media operations needs in natural language, auto-complete architecture design, file creation, task configuration.
---

# dual-engine-automation

> Auto-setup OpenClaw dual-engine (HEARTBEAT + CRON) automation system using natural language.

## Quick Start

### Natural Language Usage

Describe your needs like talking to a person. The Skill will auto-translate to complete technical configuration.

#### Example 1: System Monitoring
**You say:**
```
帮我搭个系统监控：
- 每30分钟检查CPU、内存、磁盘
- 每天9点生成健康报告
- CPU超过80%、内存超过85%时告警
- 通知发到飞书
```

**Skill auto-configures:**
- HEARTBEAT task: 每30分钟检查系统状态
- CRON task: 每天09:00生成报告
- State management: 11个时段状态追踪
- Feishu notification: `channel=feishu`

#### Example 2: Reddit Operations
**You say:**
```
我要做Reddit运营：
- 每30分钟扫描r/TechSEO和r/GenEngineOptimization
- 早上9点生成报告，晚上10点自动发帖
- 飞书通知：chat:oc_ac50ef0887f1d1750a94a5aaecfdb959
```

**Skill auto-configures:**
- HEARTBEAT: Reddit热点扫描
- CRON: 09:00报告 + 22:00发帖检查
- Content calendar: 自动创建并管理
- Anti-duplication: 防止重复发帖机制

#### Example 3: Competitor Monitoring
**You say:**
```
监控竞品价格：
- 每30分钟检查竞品网站价格变化
- 每周一9点生成周报
- 价格变动超过10%立即告警
```

**Skill auto-configures:**
- HEARTBEAT: 价格监控
- CRON: 每周一09:00周报
- Alert system: 阈值触发通知
- Data archive: 历史价格记录

#### Example 4: Multi-Agent Routing
**You say:**
```
设置多渠道运营：
- 飞书消息用main agent处理
- Discord消息用work agent处理
- 两边都走双引擎监控
```

**Skill auto-configures:**
- Bindings: Discord→work, Feishu→main
- Separate workspaces: 各自独立工作区
- Unified monitoring: 统一监控面板

### Auto-Translation

| You Say | Skill Understands | Auto-Config |
|---------|------------------|-------------|
| "Check/scan/monitor every 30 min" | HEARTBEAT Task | 30-min cycle monitoring |
| "Daily at XX / schedule" | CRON Task | Scheduled execution |
| "Generate report" | CRON Deep Task | Report + notification |
| "Post/publish content" | Content Task | content-calendar + posting |
| "To Feishu group" OR "chat:oc_xxx" | Feishu Notify | channel=feishu |
| "No channel specified" | Default Channel | No channel parameter |

### Workspace Inheritance

**Important**: This Skill operates within the **calling Agent's Workspace**.

| Calling Agent | Workspace Path | Files Created Here |
|--------------|----------------|-------------------|
| Main Agent | Current Agent's workspace | `memory/`, `HEARTBEAT.md`, etc. |
| Work Agent (Discord) | `/Users/xxx/workspace-javis-discord/` | Relative to that workspace |

**Path Rules**:
- ✅ Use **relative paths**: `memory/cron-execution-state.json`
- ✅ Use **workspace-relative**: `HEARTBEAT.md`, `SOUL.md`
- ❌ Do NOT use absolute paths like `/Users/xxx/workspace/...`

The Skill automatically places all files in the correct location based on which Agent invoked it.

### Channel Auto-Detection

The Skill automatically detects which channel to use:

| Input Pattern | Detection | Command |
|--------------|-----------|---------|
| Contains "Feishu" OR `chat:oc_xxx` | Feishu channel | `channel=feishu` |
| No channel keyword | Default channel | No `channel` parameter |

## Examples

### Example 1: System Monitoring (Simple)

**Natural Language:**
```
I want to build system monitoring:
- Check CPU, memory, disk every 30 minutes
- Generate daily report at 09:00
- Alert thresholds: CPU>80%, Memory>85%, Disk>90%
- Feishu notify: chat:oc_xxx
```

> Files auto-created in calling Agent's workspace. No manual path needed.

**Config-Type (Advanced):**
```
Monitoring (HEARTBEAT):
- Check every 30 min: CPU, Memory, Disk
- Alert conditions: CPU>80%, Memory>85%, Disk>90%

Scheduled Tasks (CRON):
- Daily at 09:00: System health report
- Weekly on Monday 09:00: Resource trend analysis

Notification:
- Feishu: chat:oc_xxx
- Alert level: immediate

Self-Evolution:
- Enabled: yes
- Auto-optimize thresholds: yes
```

### Example 2: Reddit Operations

**Natural Language:**
```
I want to build Reddit operations:
- Scan r/TechSEO and r/GenEngineOptimization every 30 min
- Generate report at 09:00, auto-post at 22:00
- Feishu notify: chat:oc_ac50ef0887f1d1750a94a5aaecfdb959
```

> Files auto-created in calling Agent's workspace. No manual path needed.

**Config-Type (Advanced):**
```
Monitoring:
- Scan subreddits: r/TechSEO, r/GenEngineOptimization
- Metrics: new posts, upvotes, comments
- High-value threshold: 50+ upvotes

Scheduled Tasks:
- 09:00: Morning report
- 22:00: Posting check (EST 09:00)
- Sunday 20:00: Weekly report

Notification:
- Feishu: chat:oc_ac50ef0887f1d1750a94a5aaecfdb959
- Major findings: immediate
- Routine reports: scheduled

Self-Evolution:
- Enabled: yes
- Optimize: posting time, content type, engagement
- A/B testing: yes
```

### Example 3: Competitor Monitoring (Default Channel)

**Natural Language:**
```
I want to build competitor monitoring:
- Check competitor prices every 30 minutes
- Generate weekly report on Monday 09:00
# No Feishu specified → Uses default channel
```

> Files auto-created in calling Agent's workspace. No manual path needed.

## Directory Structure

**Default Structure** (auto-created in calling Agent's workspace):

```
workspace/                           # Calling Agent's workspace (auto-detected)
├── HEARTBEAT.md                     # HEARTBEAT instructions
├── memory/                          # Data storage
│   ├── cron-execution-state.json    # State management (11 time slots)
│   ├── content-calendar.md          # Content calendar (if posting enabled)
│   ├── content-ideas.md             # Content ideas library
│   ├── post-performance-log.md      # Performance tracking
│   ├── YYYY-MM-DD.md                # Daily reports
│   ├── performance-logs/            # Execution data
│   ├── optimization-reports/        # Optimization records
│   └── learning/                    # Learning archive
│       ├── daily-reports/           # Daily learning summaries
│       ├── insights/                # Strategy insights
│       ├── hot-posts/               # Hot content archive
│       └── competitors/             # Competitor intelligence
├── SOUL.md                          # Agent persona (optional)
├── AGENTS.md                        # Operations guide (optional)
└── OPTIMIZATION.md                  # Optimization records (optional)
```

### Key Points

✅ **Auto-Placement**: All files automatically created in correct locations  
✅ **No Manual Path**: Don't specify paths, Skill handles it  
✅ **Relative Paths**: Use `memory/xxx.md` in all commands  
✅ **Workspace Inheritance**: Files go to calling Agent's workspace  

### Multi-Agent Setup

When using Multi-Agent Routing:

| Agent | Files Created In | Example |
|-------|-----------------|---------|
| Main Agent | Main workspace | `workspace/memory/...` |
| Work Agent (Discord) | Work workspace | `workspace-javis-discord/memory/...` |

Each Agent maintains separate file structure in its own workspace.

## Auto-Configured CRON Tasks

### Basic Tasks

| Time | Task | Description |
|------|------|-------------|
| 00:00 | State Reset | Reset cron-execution-state.json |
| Every 30 min | HEARTBEAT | Execute per HEARTBEAT.md |
| Your time | Deep Tasks | Reports, sync, posting |
| 20:00 | Git Commit | Daily backup (optional) |

### Self-Evolution Tasks (Default On)

| Time | Task | Action |
|------|------|--------|
| Daily 20:30 | Data Analysis | Analyze execution data |
| Sunday 20:30 | Strategy Optimization | Weekly optimization |
| 1st of month 20:30 | Major Upgrade | Deep analysis |

## Feishu Notification

### Get Chat ID

Send a message in the Feishu group, OpenClaw will display:
```json
{
  "channel": "feishu",
  "chat_id": "oc_ac50ef0887f1d1750a94a5aaecfdb959"
}
```

### Usage

**With Feishu:**
```
...notify Feishu chat:oc_ac50ef0887f1d1750a94a5aaecfdb959
```
→ Generates: `channel=feishu target=chat:oc_xxx`

**Default Channel:**
```
...send to current session
```
→ Uses: Default channel (no `channel` parameter)

### Notification Rules

| User Specifies | Target | Command | Use Case |
|---------------|--------|---------|----------|
| Feishu + chat:oc_xxx | Feishu group | `channel=feishu` | Team collaboration |
| No channel | Current session | No param | Personal testing |

## Self-Evolution Mechanism

Systems built with this Skill have **built-in self-evolution** by default.

### Evolution Loop

```
Execute → Analyze → Decide → Optimize → Update → Re-execute
   ↑                                            ↓
   └──────────── Continuous Iteration ←─────────┘
```

### Auto-Optimization

- **Time Optimization**: Auto-adjust best execution time
- **Content Optimization**: Auto-identify high-performing content
- **Task Optimization**: Auto-split time-consuming tasks
- **Strategy Optimization**: Auto-update strategy docs

### Example: Posting Time Optimization

```
Week 1: Post at 22:00, system records data
Week 2: Analysis shows 21:00 performs better
Week 3: Auto-adjust to 21:00, update docs
Week 4: Verify 35% improvement
→ Self-evolution cycle complete
```

## Config-Type Usage (Advanced)

For precise control of each parameter:

### Template

```
Monitoring (HEARTBEAT):
- Check every 30 min: [task]
- Content: [detailed list]
- Alert conditions: [thresholds]

Scheduled Tasks (CRON):
- Daily [time]: [task]
- Weekly [day][time]: [task]

Notification:
- Feishu: [chat:oc_xxx] → channel=feishu
- Default: (leave empty for default)
- Level: [all/alerts-only/reports-only]

Self-Evolution:
- Enabled: [yes/no]
- Analysis frequency: [daily/weekly]
```

### Config vs Natural Language

| Aspect | Natural | Config-Type |
|--------|---------|-------------|
| Setup Speed | 1 minute | 5-10 minutes |
| Precision | Standard | Exact parameters |
| Use Case | Quick validation | Production deployment |
| Documentation | Auto-generated | Detailed docs |
| Team Collaboration | Personal | Auditable |

**Strategy:**
1. **Natural Language** → Quick setup and validation
2. **Run and collect data** → Understand performance
3. **Config-Type tuning** → Production-grade deployment
4. **Archive final config** → Production standard

## Post-Setup Management

Continue managing in natural language:

**Add Task:**
> "Add a task to check emails every day at 3 PM"

**Modify Task:**
> "Change daily report time to 8 AM"

**Check Status:**
> "View current configuration and task status"

**Pause System:**
> "Pause all CRON tasks"

## Design Principles

1. **Natural Language First**: Use daily language, no jargon
2. **Auto Path Planning**: Files auto-placed in standard dirs
3. **Out-of-the-Box**: Ready to run after configuration
4. **Self-Evolution**: Auto-analyze, optimize, iterate
5. **Extensible**: Add/modify tasks via conversation

## Auto-Handled Technical Details

The Skill automatically handles:

- ✅ Auto use `--browser-profile openclaw`
- ✅ Auto config `--target isolated`
- ✅ Auto set timezone `Asia/Shanghai`
- ✅ Files auto-store in `memory/` standard directory
- ✅ Auto config `channel=feishu` (if specified)
- ✅ Auto config anti-duplication mechanism
- ✅ Auto create state backups

## Full Example Dialogue

### Scenario: Reddit Operations

**User:**
> I want to build Reddit operations, scan TechSEO and GEO subreddits every 30 min, generate reports at 9 AM, auto-post at 10 PM

**Skill:**
> ✅ **Understood your requirements:**
> - HEARTBEAT: Scan r/TechSEO, r/GenEngineOptimization every 30 min
> - CRON: 09:00 daily report, 22:00 posting check
> - Self-evolution: Enabled (auto-optimize)
>
> 📁 **Files Created:**
> - HEARTBEAT.md (scan instructions)
> - memory/cron-execution-state.json (11 time slots)
> - memory/content-calendar.md (posting schedule)
> - memory/learning/hot-posts/ (archive)
> - SOUL.md (Reddit persona)
> - AGENTS.md (operations guide)
>
> ⏰ **CRON Tasks (8):**
> - 00:00 State reset
> - 09:00 Generate report
> - 09:10 HEARTBEAT trigger
> - 22:00 Posting execution
> - 20:00 Git auto-commit
> - 20:30 Daily data analysis
>
> 🚀 **System Setup Complete!**
> Next execution: Tomorrow 09:00

---

## Chinese Reference / 中文参考

### 工作区继承规则

**重要**: 本 Skill 在**调用它的 Agent 的工作区**中运行。

| 调用 Agent | 工作区路径 | 文件创建位置 |
|-----------|-----------|-------------|
| Main Agent | 当前 Agent 的工作区 | `memory/`、`HEARTBEAT.md` 等 |
| Work Agent (Discord) | `/Users/xxx/workspace-javis-discord/` | 相对于该工作区 |

**路径规则**:
- ✅ 使用**相对路径**: `memory/cron-execution-state.json`
- ✅ 使用**工作区相对路径**: `HEARTBEAT.md`、`SOUL.md`
- ❌ 不要使用绝对路径如 `/Users/xxx/workspace/...`

本 Skill 根据调用它的 Agent 自动将所有文件放置在正确位置。

### 快速开始

#### 自然语言用法（推荐）

**系统监控：**
```
帮我搭个系统监控：
- 每30分钟检查CPU、内存、磁盘
- 每天9点生成健康报告
- CPU超过80%、内存超过85%时告警
- 通知发到飞书
```

**Reddit运营：**
```
我要做Reddit运营：
- 每30分钟扫描r/TechSEO和r/GenEngineOptimization
- 早上9点生成报告，晚上10点自动发帖
- 飞书通知：chat:oc_ac50ef0887f1d1750a94a5aaecfdb959
```

**竞品监控：**
```
监控竞品价格：
- 每30分钟检查竞品网站价格变化
- 每周一9点生成周报
- 价格变动超过10%立即告警
```

**配置型用法（高级）：**
```
监控需求：
- 每30分钟检查：CPU、内存、磁盘
- 告警阈值：CPU>80%

定时任务：
- 每天09:00：生成日报
- 每周一09:00：生成周报

通知设置：
- 飞书：chat:oc_xxx
```

### 默认文件结构

Skill自动在调用Agent的工作区创建：

```
workspace/                    # 调用Agent的工作区（自动识别）
├── HEARTBEAT.md              # HEARTBEAT指令
├── memory/                   # 数据存储
│   ├── cron-execution-state.json    # 状态管理
│   ├── content-calendar.md          # 内容日历
│   ├── content-ideas.md             # 内容创意库
│   ├── post-performance-log.md      # 表现追踪
│   └── learning/                    # 学习归档
│       ├── daily-reports/           # 每日学习报告
│       ├── insights/                # 策略洞察
│       ├── hot-posts/               # 热点内容
│       └── competitors/             # 竞品情报
├── SOUL.md                   # Agent人设（可选）
├── AGENTS.md                 # 运营指南（可选）
└── OPTIMIZATION.md           # 优化记录（可选）
```

✅ **自动创建**：所有文件自动放置在正确位置  
✅ **无需指定路径**：不用告诉Skill放哪里，自动处理  
✅ **使用相对路径**：所有操作使用 `memory/xxx.md`  
✅ **多Agent支持**：每个Agent在自己的workspace中管理文件  

### 通道自动识别

| 输入 | 识别结果 | 命令 |
|-----|---------|------|
| 包含"飞书"或 `chat:oc_xxx` | Feishu通道 | `channel=feishu` |
| 无通道关键词 | 默认通道 | 不添加参数 |

---

**核心本质**：把"手动复制粘贴配置"变成"对话式自动搭建"

直接说：
- "我想每30分钟检查XX"
- "我想每天9点做XX"
- "我想监控XX并通知飞书"

Skill自动翻译成完整的技术配置。
