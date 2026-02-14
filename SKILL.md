---
name: dual-engine-automation
description: Auto-setup OpenClaw dual-engine (HEARTBEAT + CRON) automation system. Describe your monitoring, scheduling, social media operations needs in natural language, auto-complete architecture design, file creation, task configuration.
---

# dual-engine-automation

> Auto-setup OpenClaw dual-engine (HEARTBEAT + CRON) automation system using natural language.

## Quick Start

### Natural Language Usage

Describe your needs like talking to a person:

```
I want to check server CPU and memory every 30 minutes, generate health reports at 9 AM daily
```

```
I want to monitor competitor websites, check price changes every 30 minutes, send daily reports to Feishu at 9 AM
```

```
I want to operate Reddit, scan GEO and TechSEO subreddits every 30 minutes, auto-post at 10 PM daily
```

### Auto-Translation

| You Say | Skill Understands | Auto-Config |
|---------|------------------|-------------|
| "Check/scan/monitor every 30 min" | HEARTBEAT Task | 30-min cycle monitoring |
| "Daily at XX / schedule" | CRON Task | Scheduled execution |
| "Generate report" | CRON Deep Task | Report + notification |
| "Post/publish content" | Content Task | content-calendar + posting |
| "To Feishu group" OR "chat:oc_xxx" | Feishu Notify | channel=feishu |
| "No channel specified" | Default Channel | No channel parameter |

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
- Workspace: /Users/name/system-monitor
```

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
- Workspace: /Users/name/reddit-ops
```

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
- Workspace: /Users/name/competitor-monitor
# No Feishu specified → Uses default channel
```

## Directory Structure

Auto-created standard directory structure:

```
workspace/
├── HEARTBEAT.md                     # HEARTBEAT instructions
├── memory/                          # Data storage
│   ├── cron-execution-state.json    # State management
│   ├── content-calendar.md          # Content calendar (if posting)
│   ├── post-performance-log.md      # Performance logs
│   ├── performance-logs/            # Execution data
│   ├── optimization-reports/        # Optimization reports
│   └── learning/                    # Learning archive
│       ├── insights/                # Insights
│       ├── hot-posts/              # Hot posts
│       └── competitors/            # Competitor data
├── SOUL.md                          # Agent persona
├── AGENTS.md                        # Operations guide
└── OPTIMIZATION.md                  # Optimization records
```

> All files auto-placed in `memory/` with standard naming. No manual path needed.

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

### 快速开始

**自然语言用法：**
```
我要每30分钟检查服务器CPU和内存，每天9点生成健康报告
```

**配置型用法：**
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

### 通道自动识别

| 输入 | 识别结果 | 命令 |
|-----|---------|------|
| 包含"飞书"或 `chat:oc_xxx` | Feishu通道 | `channel=feishu` |
| 无通道关键词 | 默认通道 | 不添加参数 |

---

**Essence**: Turn "manual copy-paste configuration" into "conversational auto-setup"

Just say:
- "I want to check XX every 30 min"
- "I want to do XX at 9 AM daily"
- "I want to monitor XX and notify Feishu"

Skill auto-translates to complete technical configuration.
