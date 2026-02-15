# Example Library

Complete examples for various use cases.

## System Monitoring

### Natural Language
```
I want to build system monitoring:
- Check CPU, memory, disk every 30 minutes
- Generate daily report at 09:00
- Alert thresholds: CPU>80%, Memory>85%, Disk>90%
- Feishu notify: chat:oc_xxx
```

### Config-Type
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

---

## Reddit Operations

### Natural Language
```
I want to build Reddit operations:
- Scan r/TechSEO and r/GenEngineOptimization every 30 min
- Generate report at 09:00, auto-post at 22:00
- Feishu notify: chat:oc_ac50ef0887f1d1750a94a5aaecfdb959
```

### Config-Type
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

---

## Competitor Monitoring

### Natural Language
```
I want to build competitor monitoring:
- Check competitor prices every 30 minutes
- Generate weekly report on Monday 09:00
# No Feishu specified → Uses default channel
```

### Config-Type
```
Monitoring:
- Check every 30 min: Competitor website prices
- Track: price changes, availability, promotions
- Alert threshold: price change >10%

Scheduled Tasks:
- Monday 09:00: Weekly price report
- Daily 20:00: Price change summary (if any)

Notification:
- Default channel
- Immediate alert on >10% change

Data Archive:
- Historical prices: memory/competitor-prices/
- Trend analysis: weekly
```

---

## Multi-Agent Routing

### Natural Language
```
设置多渠道运营：
- 飞书消息用main agent处理
- Discord消息用work agent处理
- 两边都走双引擎监控
```

### Config-Type
```
Multi-Agent Setup:
- Main Agent (Feishu): HEARTBEAT + CRON
- Work Agent (Discord): HEARTBEAT + CRON

Routing:
- Feishu → main Agent
- Discord → work Agent

Unified Monitoring:
- Cross-agent status check: daily
- Aggregated reporting: weekly
```

---

## Full Dialogue Example

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
