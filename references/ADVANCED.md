# Advanced Configuration Guide

> Config-Type usage for precise control of each parameter.

## Template

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

## Config vs Natural Language

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

## Detailed Parameters

### HEARTBEAT Configuration

```yaml
frequency: 30min  # 30min, 1h, 2h
tasks:
  - type: scan
    target: [reddit/subreddit, website, system]
    output: memory/xxx.md
  - type: check
    metric: [cpu, memory, disk, price]
    threshold: [value]
```

### CRON Configuration

```yaml
timezone: Asia/Shanghai
tasks:
  - schedule: "0 9 * * *"  # Daily 09:00
    type: report
    format: markdown
    notification: feishu
  
  - schedule: "0 22 * * *"  # Daily 22:00
    type: content_post
    platform: reddit
    check_calendar: true
```

### Notification Rules

| Level | Triggers | Use Case |
|-------|----------|----------|
| all | Every event | Development/testing |
| alerts-only | Only warnings/errors | Production monitoring |
| reports-only | Scheduled reports | Executive summary |

### Self-Evolution Settings

```yaml
enabled: true
optimization_frequency: daily  # daily, weekly, monthly
metrics:
  - task_completion_rate
  - notification_response_time
  - content_performance
  - system_health
adjustments:
  - time_optimization: true
  - content_optimization: true
  - task_splitting: true
```
