---
name: dual-engine-automation
description: Auto-setup OpenClaw dual-engine (HEARTBEAT + CRON) automation system. Describe your monitoring, scheduling, social media operations needs in natural language, auto-complete architecture design, file creation, and task configuration. 自动搭建OpenClaw双引擎（HEARTBEAT + CRON）自动化系统。使用自然语言描述监控、定时任务、社媒运营等需求，自动完成架构设计、文件创建、任务配置。
---

# dual-engine-automation | 双引擎自动化

> **EN**: Describe your needs in **natural language**, auto-setup HEARTBEAT + CRON dual-engine automation system.
> 
> **CN**: 使用**自然语言**描述你的需求，自动搭建HEARTBEAT + CRON双引擎自动化系统。

---

## 🚀 Quick Start | 快速开始

### Natural Language Usage | 自然语言用法

**EN**: Just describe your needs like talking to a person:

**CN**: 像跟人说话一样描述你的需求：

```
我要每30分钟检查服务器CPU和内存，每天上午9点生成健康报告
I want to check server CPU and memory every 30 minutes, generate health reports at 9 AM daily
```

```
我要监控竞品网站，每30分钟检查价格变化，每天早上9点发送竞品日报到飞书群
I want to monitor competitor websites, check price changes every 30 minutes, send daily competitor reports to Feishu at 9 AM
```

```
我要做Reddit运营，每30分钟扫描GEO和TechSEO板块，每天晚上10点自动发帖
I want to operate Reddit, scan GEO and TechSEO subreddits every 30 minutes, auto-post at 10 PM daily
```

### Auto-Translation | 自动理解

| You Say | Skill Understands | Auto-Config |
|---------|------------------|-------------|
| "每30分钟检查/扫描/监控" / "Check/scan every 30 min" | HEARTBEAT Task | 30-min cycle monitoring |
| "每天XX点/定时/自动" / "Daily at XX / schedule" | CRON Task | Scheduled execution |
| "生成报告/发送日报" / "Generate report" | CRON Deep Task | Report + notification |
| "发帖/发布内容" / "Post/publish" | Content Task | content-calendar + posting |
| "到飞书群/通知群组" / "To Feishu group" | Feishu Notify | channel=feishu |

### Channel Auto-Detection | 通道自动识别

**EN**: The Skill automatically detects which channel to use based on your input:

**CN**: Skill 根据你的输入自动识别使用哪个通道：

| User Input | Auto-Detect | Command |
|------------|-------------|---------|
| Mention "Feishu/飞书" OR provide `chat:oc_xxx` | Feishu channel | `channel=feishu` |
| No channel specified | Default channel | No `channel` parameter |

**Examples | 示例**：
```
"通知到飞书群 chat:oc_xxx" → Auto-use: channel=feishu
"发送到当前会话" → Auto-use: default channel (no parameter)
"notify Feishu chat:oc_xxx" → Auto-use: channel=feishu
"send to current session" → Auto-use: default channel
```

---

## 📋 Examples | 示例

### Example 1: System Monitoring | 系统监控

**Natural | 自然语言：**
```
我要监控服务器状态，每30分钟检查CPU和内存，每天9点生成健康报告
I want to monitor server status, check CPU and memory every 30 min, generate health reports at 9 AM daily
```

**Config-Type | 配置型：**
```
监控需求 Monitoring:
- 每30分钟检查 CPU/Memory/Disk every 30 min
- 告警阈值 Thresholds: CPU>80%, Memory>85%, Disk>90%

定时任务 Scheduled Tasks:
- 每天09:00生成日报 Daily report at 09:00
- 每周一09:00生成周报 Weekly report on Monday 09:00

通知设置 Notification:
- 飞书群组 Feishu: chat:oc_xxx
- 告警立即通知 Alerts: immediate
```

---

### Example 2: Reddit Operations | Reddit运营

**Natural | 自然语言：**
```
我要做Reddit运营，每30分钟扫描TechSEO和GEO板块，每天早上9点生成报告，晚上10点自动发帖，飞书通知到chat:oc_xxx
I want Reddit operations, scan TechSEO and GEO subreddits every 30 min, generate reports at 9 AM, auto-post at 10 PM, notify Feishu chat:oc_xxx
```

**Config-Type | 配置型：**
```
监控需求 Monitoring:
- 每30分钟扫描板块 Subreddits: r/TechSEO, r/GenEngineOptimization
- 监控指标 Metrics: new posts, upvotes, comments

定时任务 Scheduled Tasks:
- 09:00 生成晨报 Morning report
- 22:00 发帖检查 Posting (EST 09:00)
- 20:00 Git自动提交 Auto Git commit

通知设置 Notification:
- 飞书群组 Feishu: chat:oc_ac50ef0887f1d1750a94a5aaecfdb959
- 重大发现立即通知 Immediate alert for major findings
```

---

### Example 3: Competitor Monitoring | 竞品监控

**Natural | 自然语言：**
```
我要监控竞品，每30分钟检查竞品网站价格和Twitter动态，每周一上午9点生成周报，通知到飞书
I want competitor monitoring, check website prices and Twitter every 30 min, generate weekly reports on Monday 9 AM, notify Feishu
```

**Config-Type | 配置型：**
```
监控需求 Monitoring:
- 每30分钟检查 Website prices, Twitter updates
- 数据存储 Storage: memory/learning/competitors/

定时任务 Scheduled Tasks:
- 每周一09:00生成周报 Weekly report Monday 09:00

通知设置 Notification:
- 飞书群组 Feishu: chat:oc_xxx
```

---

## 🗂️ Directory Structure | 目录结构

**EN**: Auto-created standard directory structure:

**CN**: 自动创建的标准目录结构：

```
workspace/ | 工作区/
├── HEARTBEAT.md                     # HEARTBEAT execution instructions | 执行指令
├── memory/                          # Data storage | 数据存储
│   ├── cron-execution-state.json    # State management | 状态管理
│   ├── content-calendar.md          # Content calendar (if posting) | 内容日历
│   ├── post-performance-log.md      # Performance logs | 表现记录
│   ├── performance-logs/            # Execution data (self-evolution) | 执行数据
│   ├── optimization-reports/        # Optimization reports | 优化报告
│   └── learning/                    # Learning archive | 学习归档
│       ├── insights/                # Insights analysis | 洞察分析
│       ├── hot-posts/              # Hot posts archive | 热点存档
│       └── competitors/            # Competitor data | 竞品数据
├── SOUL.md                          # Agent persona | 智能体人设
├── AGENTS.md                        # Operations guide | 运营指南
└── OPTIMIZATION.md                  # Optimization records | 优化策略记录
```

> **Note**: All files auto-placed in `memory/` with standard naming. No manual path needed.
> 
> **注意**：所有文件自动放在 `memory/` 目录下，采用标准命名格式，无需手动指定路径。

---

## 📊 Auto-Configured CRON Tasks | 自动配置的CRON任务

### Basic Tasks | 基础任务

| Time | Task | Description |
|------|------|-------------|
| 00:00 | State Reset | Reset cron-execution-state.json |
| Every 30 min | HEARTBEAT Trigger | Execute checks per HEARTBEAT.md |
| Your specified time | Deep Tasks | Reports, sync, posting, etc. |
| 20:00 | Git Auto-Commit | Daily backup (optional) |

### Self-Evolution Tasks (Default On) | 自我进化任务（默认启用）

| Time | Task | Action |
|------|------|--------|
| Daily 20:30 | Data Analysis | Analyze execution data |
| Sunday 20:30 | Strategy Optimization | Weekly optimization plan |
| 1st of month 20:30 | Major Upgrade | Deep analysis + upgrade |

---

## 🔔 Feishu Notification | 飞书通知

### Get Chat ID | 获取会话ID

**EN**: Send a message in the Feishu group, OpenClaw will display:

**CN**: 在飞书群组中发送一条消息，OpenClaw会显示：

```json
{
  "channel": "feishu",
  "chat_id": "oc_ac50ef0887f1d1750a94a5aaecfdb959"
}
```

### Usage | 用法

**With Feishu | 使用飞书：**
```
...飞书通知到chat:oc_ac50ef0887f1d1750a94a5aaecfdb959
...notify Feishu chat:oc_ac50ef0887f1d1750a94a5aaecfdb959
```
→ Auto-generates: `channel=feishu target=chat:oc_xxx`

**Default Channel | 默认通道：**
```
...发送到当前会话
...send to current session
```
→ Auto-generates: No channel parameter (uses default)

### Notification Rules | 通知规则

| User Specifies | Target | Command Generated | Use Case |
|----------------|--------|-------------------|----------|
| Feishu chat:oc_xxx | Feishu group | `channel=feishu target=chat:oc_xxx` | Team collaboration |
| No channel specified | Current session | No channel parameter | Personal testing |

---

## 🔄 Self-Evolution | 自我进化

**EN**: The system has **built-in self-evolution** capability by default:

**CN**: 搭建的系统**默认具备自我进化能力**：

### Evolution Loop | 进化闭环

```
执行 Execute → 分析 Analyze → 决策 Decide → 优化 Optimize → 更新 Update → 再执行 Re-execute
  ↑                                                                              ↓
  └────────────────────────── 持续迭代 Continuous iteration ←────────────────────┘
```

### Auto-Optimization | 自动优化

- **Time Optimization**: Auto-adjust best execution time (e.g., posting time)
- **Content Optimization**: Auto-identify high-performing content types
- **Task Optimization**: Auto-split time-consuming tasks
- **Strategy Optimization**: Auto-update operations strategy docs

### Example | 示例

```
Week 1: Post at 22:00, system records data
Week 2: Analysis shows 21:00 performs better
Week 3: Auto-adjust to 21:00, update docs
Week 4: Verify effect, confirm 35% improvement
→ Self-evolution cycle complete

第1周：22:00发帖，系统记录数据
第2周：分析发现21:00效果更好
第3周：自动调整为21:00，更新文档
第4周：验证效果，确认提升35%
→ 完成一轮自我进化
```

---

## 🔧 Config-Type Usage (Advanced) | 配置型用法（高级）

**EN**: For precise control of each parameter:

**CN**: 如需精确控制每个参数：

### Template | 模板

```
监控需求 Monitoring (HEARTBEAT):
- 每30分钟检查 Check every 30 min: [task]
- 检查内容 Content: [detailed list]
- 告警条件 Alert conditions: [thresholds]

定时任务 Scheduled Tasks (CRON):
- 每天[时间] Daily [time]: [task]
- 每周[X][时间] Weekly [day][time]: [task]

通知设置 Notification:
- 飞书群组 Feishu: [chat:oc_xxx] → channel=feishu
- 默认通道 Default: (leave empty for default channel)
- 通知级别 Level: [all/alerts-only/reports-only]

自我进化 Self-Evolution:
- 启用自动优化 Enabled: [yes/no]
- 数据分析频率 Analysis freq: [daily/weekly]
```

### Config vs Natural Language | 配置型 vs 自然语言

| Aspect | Natural Language | Config-Type |
|--------|-----------------|-------------|
| Setup Speed | 1 minute | 5-10 minutes |
| Precision | Standard config | Exact parameters |
| Use Case | Quick validation | Production deployment |
| Documentation | Auto-generated | Detailed config docs |
| Team Collaboration | Personal | Auditable, reproducible |

**Strategy | 策略**：
1. **Natural Language** → Quick setup and validation
2. **Run and collect data** → Understand actual performance
3. **Config-Type tuning** → Production-grade deployment
4. **Archive final config** → As production standard

---

## 💬 Post-Setup Management | 后续管理

**EN**: Continue managing in natural language:

**CN**: 继续用自然语言管理：

**Add Task | 添加任务：**
> "再加一个每天下午3点检查邮件的任务"
> "Add a task to check emails every day at 3 PM"

**Modify Task | 修改任务：**
> "把日报时间改到8点"
> "Change daily report time to 8 AM"

**Check Status | 查看状态：**
> "查看当前配置和任务状态"
> "View current configuration and task status"

**Pause System | 暂停系统：**
> "暂停所有CRON任务"
> "Pause all CRON tasks"

---

## 🎯 Design Principles | 设计原则

1. **Natural Language First | 自然语言优先**
   - Describe needs in daily language
   - No technical jargon required

2. **Auto Path Planning | 自动路径规划**
   - Files auto-placed in standard directories
   - No manual path specification

3. **Out-of-the-Box | 开箱即用**
   - Ready to run after configuration
   - Immediate execution

4. **Self-Evolution | 自我进化**
   - Auto-analyze data
   - Optimize strategies
   - Continuous iteration

5. **Extensible | 可扩展**
   - Add/modify tasks via conversation
   - Flexible configuration

---

## ⚙️ Auto-Handled Technical Details | 自动处理的技术细节

**EN**: The Skill automatically handles:

**CN**: Skill自动处理：

- ✅ Auto use `--browser-profile openclaw`
- ✅ Auto config `--target isolated`
- ✅ Auto set timezone `Asia/Shanghai`
- ✅ Files auto-store in `memory/` standard directory
- ✅ Auto config `channel=feishu` (if Feishu specified)
- ✅ Auto config anti-duplication mechanism
- ✅ Auto create state backups

---

## 📝 Full Example Dialogue | 完整示例对话

### Scenario: Reddit Operations | 场景：Reddit运营

**User | 用户：**
> 我要搭建Reddit运营系统，每30分钟扫描TechSEO和GEO板块，每天早上9点生成报告，晚上10点自动发帖
> I want to build Reddit operations, scan TechSEO and GEO subreddits every 30 min, generate reports at 9 AM, auto-post at 10 PM

**Skill：**
> ✅ ** understood your requirements | 理解您的需求：**
> - HEARTBEAT: Scan r/TechSEO, r/GenEngineOptimization every 30 min | 每30分钟扫描
> - CRON: 09:00 daily report, 22:00 posting check | 09:00日报，22:00发帖
> - Self-evolution: Enabled (auto-optimize posting time and content) | 自我进化已启用
>
> 📁 **Files Created | 自动创建文件：**
> - HEARTBEAT.md (scan instructions | 扫描指令)
> - memory/cron-execution-state.json (11 time slots state management | 11时段状态管理)
> - memory/content-calendar.md (posting schedule | 发帖计划表)
> - memory/learning/hot-posts/ (hot posts archive | 热点存档)
> - SOUL.md (Reddit persona | Reddit人设)
> - AGENTS.md (operations guide | 运营指南)
>
> ⏰ **CRON Tasks Configured | 配置CRON任务（8个）：**
> - 00:00 State reset | 状态重置
> - 09:00 Generate daily report | 生成日报
> - 09:10 HEARTBEAT trigger | HEARTBEAT触发
> - 22:00 Posting execution | 发帖执行
> - 20:00 Git auto-commit | Git自动提交
> - 20:30 Daily data analysis (self-evolution) | 每日数据分析
>
> 🚀 **System Setup Complete | 系统搭建完成！**
> Next execution | 下次执行：Tomorrow 09:00 | 明天09:00

---

## 📚 Additional Resources | 额外资源

- **Implementation Guide**: `IMPLEMENTATION.md`
- **Templates**: `TEMPLATES.md`
- **Examples**: `EXAMPLE.md`
- **Self-Evolution**: `SELF_EVOLUTION.md`
- **实战指南**: `guides/OPENCLAW_DUAL_ENGINE_GUIDE.md`

---

**Essence | 本质**：

**EN**: Turn "manual copy-paste configuration" into "conversational auto-setup"

**CN**：把"手动复制配置"变成"对话式自动搭建"

Just say | 只需说：
- "我要每30分钟检查XX" / "I want to check XX every 30 min"
- "我要每天9点做XX" / "I want to do XX at 9 AM daily"
- "我要监控XX并通知到飞书" / "I want to monitor XX and notify Feishu"

Skill auto-translates to complete technical configuration | Skill自动翻译成完整技术配置
