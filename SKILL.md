---
name: dual-engine-automation
description: Auto-setup OpenClaw dual-engine (HEARTBEAT + CRON) automation system. Use when user needs scheduled tasks, monitoring systems, automated workflows, periodic backups, or recurring content publishing.

## Use When
- User wants to set up scheduled/recurring tasks (CRON)
- User needs monitoring systems that check periodically (HEARTBEAT)
- User mentions "automation", "定时任务", "循环检查", "自动执行"
- User wants Reddit operations, system monitoring, or competitor tracking
- User needs multi-Agent coordination with different channels
- User wants scheduled content posting/publishing (daily/weekly posts)
- User needs periodic backups (daily Git commit, data backup)
- User wants scheduled report generation (daily/weekly reports)
- User needs data synchronization at intervals (hourly/daily sync)
- User wants polling/checking something repeatedly (API status, price changes)

## Do NOT Use When
- One-time immediate execution tasks
- User explicitly says "now" or "immediately"
- Simple one-off requests without scheduling needs
---

# dual-engine-automation

> Auto-setup OpenClaw dual-engine (HEARTBEAT + CRON) automation using natural language.

## Quick Start

### Natural Language Usage

Describe your needs naturally. The Skill auto-translates to technical configuration.

**Example 1: System Monitoring**
```
帮我搭个系统监控：
- 每30分钟检查CPU、内存、磁盘
- 每天9点生成健康报告
- CPU超过80%时告警
- 通知发到飞书 chat:oc_xxx
```

**Example 2: Reddit Operations**
```
我要做Reddit运营：
- 每30分钟扫描r/TechSEO
- 早上9点生成报告，晚上10点自动发帖
- 飞书通知：chat:oc_ac50ef0887f1d1750a94a5aaecfdb959
```

**Example 3: Multi-Agent Routing**
```
设置多渠道运营：
- 飞书消息用main agent处理
- Discord消息用work agent处理
```

## Auto-Translation

| You Say | Skill Configures |
|---------|-----------------|
| "Check every 30 min" | HEARTBEAT Task (30-min cycle) |
| "Daily at XX" | CRON Task (scheduled) |
| "Generate report" | CRON + notification |
| "Post content" | content-calendar + posting |
| "Feishu chat:oc_xxx" | `channel=feishu` |
| No channel specified | Default channel |

## Channel Auto-Detection

| Input Pattern | Result |
|--------------|--------|
| Contains "Feishu" or `chat:oc_xxx` | `channel=feishu` |
| No channel keyword | Default channel |

## Workspace Inheritance

**Important**: This Skill operates in the **calling Agent's Workspace**.

| Calling Agent | Files Created In |
|--------------|-----------------|
| Main Agent | Current workspace: `memory/`, `HEARTBEAT.md` |
| Work Agent | Work workspace: `/workspace-javis-discord/` |

**Path Rules**:
- ✅ Use relative paths: `memory/cron-state.json`
- ❌ Don't use absolute paths

## Directory Structure

Auto-created in calling Agent's workspace:

```
workspace/
├── HEARTBEAT.md                 # HEARTBEAT instructions
├── memory/
│   ├── cron-execution-state.json    # State management
│   ├── content-calendar.md          # Content calendar
│   ├── learning/                    # Learning archive
│   └── ...
├── SOUL.md (optional)
└── AGENTS.md (optional)
```

## Auto-Handled Details

- ✅ Auto `--browser-profile openclaw`, `--target isolated`
- ✅ Auto timezone `Asia/Shanghai`, `channel=feishu`
- ✅ Auto anti-duplication, state backups

## Documentation

- **Advanced Config**: `references/ADVANCED.md`
- **Examples**: `references/EXAMPLES.md`
- **中文文档**: `references/CHINESE.md`
- **Troubleshooting**: `references/TROUBLESHOOTING.md`
