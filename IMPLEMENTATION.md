# Dual-Engine Automation Skill - 实现指南

## 如何使用这个Skill

### 对用户的Prompt（他们只需要说）

```
@dual-engine-automation 我要搭建一个[场景]自动化系统：

监控需求：
- 每30分钟检查：[具体任务，如"扫描Reddit r/TechSEO热点"]

定时任务：
- 每天09:00：[任务，如"生成运营日报"]
- 每天22:00：[任务，如"检查并执行发帖"]
- （其他时间点...）

工作区路径：[绝对路径]

通知设置（可选）：
- 飞书群组：[chat:oc_xxx] ← 在飞书群组中发消息即可看到
- 如不设置，默认仅通知当前会话

其他需求：
- [可选] 需要自动Git提交
- [可选] 需要发帖功能
- [可选] 需要多平台监控
```

---

## Agent执行流程

当收到上述需求后，agent自动执行以下步骤：

### Step 1: 需求解析

提取关键信息：
```python
requirements = {
    "scenario": "Reddit GEO运营",           # 场景名称
    "heartbeat_tasks": [                    # HEARTBEAT任务列表
        "扫描r/TechSEO热点",
        "扫描r/GenEngineOptimization热点",
        "扫描r/bigseo热点"
    ],
    "cron_tasks": [                         # CRON任务列表
        {"time": "09:00", "task": "生成运营日报"},
        {"time": "22:00", "task": "检查并执行发帖"},
        {"time": "02:00", "task": "检查并执行发帖"},
        {"time": "08:00", "task": "检查并执行发帖"}
    ],
    "feishu_group": "chat:oc_xxx",          # 飞书群组（可选，默认None=仅当前会话）
    "workspace_path": "/Users/name/xxx",    # 工作区路径
    "need_git": True,                       # 是否需要Git提交
    "need_posting": True,                   # 是否需要发帖功能
    "platforms": ["Reddit"]                 # 监控平台
}
```

### Step 2: 架构设计决策

根据需求自动决策：

```python
design_decisions = {
    # HEARTBEAT任务设计
    "heartbeat_scope": "Reddit多板块扫描",
    "heartbeat_frequency": "30分钟",
    "heartbeat_action": "扫描热点+判断重大发现",
    
    # CRON任务设计
    "cron_count": 8,  # 根据时间点自动计算
    "cron_slots": ["00:00", "09:00", "09:10", "12:00", "14:00", "18:00", "20:00", "22:00"],
    
    # 防重复策略
    "need_state_management": True,
    "state_slots": ["09:00", "09:10", "12:00", "14:00", "18:00", "20:00", "22:00"],
    
    # 自我进化（默认启用）
    "self_evolution": {
        "enabled": True,  # 默认启用
        "daily_analysis": "20:30",
        "weekly_optimization": "周日20:30",
        "monthly_upgrade": "每月1日20:30"
    },
    
    # 通知路由（根据feishu_group自动调整）
    # 如果feishu_group设置：重大发现→个人+群组，CRON→群组
    # 如果feishu_group未设置：所有通知→仅当前会话（个人）
    "heartbeat_notification": "个人(+群组如有设置)",
    "cron_notification": "群组(如有设置)或个人",
    
    # 文件清单
    "required_files": [
        "HEARTBEAT.md",
        "memory/cron-execution-state.json",
        "memory/content-calendar.md",  # 因为need_posting=True
        "memory/post-performance-log.md",
        "SOUL.md",
        "AGENTS.md"
    ]
}
```

### Step 3: 文件自动生成

#### 3.1 生成 HEARTBEAT.md

```markdown
# HEARTBEAT.md - [场景名称]主动监控系统

## 执行指令

当收到HEARTBEAT时：

### Step 0: 状态检查（防重复）
1. 读取 `memory/cron-execution-state.json`
2. 检查当前时间是否在CRON窗口（±5分钟）
3. 如状态为completed → 回复 HEARTBEAT_OK
4. 如状态为pending → 继续执行

### Step 1: 执行[监控平台]扫描
[根据需求自动生成具体扫描指令]
- Reddit: r/TechSEO, r/GenEngineOptimization, r/bigseo
- 检查热门帖子、新帖、高价值讨论

### Step 2: 判断重大发现
标准：
- [根据场景定义标准]
- Reddit: 50+ upvotes, 新研究发布, 竞品动态

### Step 3: 通知路由
- 无重大发现 → 个人会话，回复 HEARTBEAT_OK
- 有重大发现 → 个人 + [飞书群组]，详细报告

### Step 4: 状态更新
更新状态文件为 completed (by heartbeat)
```

#### 3.2 生成 memory/cron-execution-state.json

```json
{
  "version": "1.0",
  "date": "[当前日期]",
  "timezone": "Asia/Shanghai",
  "lastResetAt": "[当前时间]",
  "executions": {
    "[时间点1]": {"status": "pending", "scheduledTime": "[时间点1]"},
    "[时间点2]": {"status": "pending", "scheduledTime": "[时间点2]"},
    ...
  },
  "metadata": {
    "totalSlots": [数量],
    "completedCount": 0,
    "skippedCount": 0,
    "lastUpdated": "[当前时间]"
  }
}
```

#### 3.3 生成 memory/content-calendar.md（如需要发帖）

```markdown
# 内容发布日历

## 发布状态标记
| 标记 | 含义 | 动作 |
|------|------|------|
| 📝 | 计划中 | 等待发布 |
| ✅ | 已发布 | 跳过检查 |
| ⏸️ | 推迟 | 下一时段重试 |
| ❌ | 取消 | 不再尝试 |

## 每周发布计划
| 日期 | 时间(EST) | 北京时间 | 内容主题 | 类型 | 目标板块 | 状态 |
|------|----------|---------|---------|------|---------|------|
| [根据需求填充] | | | | | | 📝 |

## 已发布记录
| 日期 | 帖子标题 | 板块 | URL | Upvotes | Comments |
|------|---------|------|-----|---------|----------|
```

#### 3.4 生成 SOUL.md（智能体人设）

根据场景自动生成：
- 角色定位
- 语言风格
- 运营规范
- 红线规则

#### 3.5 生成自我进化相关文件（默认启用）

```markdown
# memory/performance-logs/ 目录结构
performance-logs/
├── 2026-02-14.json          # 每日执行数据
├── 2026-02-15.json
└── ...

# memory/optimization-reports/ 目录结构
optimization-reports/
├── daily/
│   └── 2026-02-14.md        # 每日优化报告
├── weekly/
│   └── 2026-W07.md          # 周度优化报告
└── monthly/
    └── 2026-02.md           # 月度优化报告

# OPTIMIZATION.md 内容
# 优化策略记录文档
# - 当前最佳实践
# - 已应用的优化
# - 待测试的策略
# - 效果追踪记录
```

### Step 4: 自动配置CRON（含自我进化任务）

#### 4.1 生成CRON配置列表

根据时间点自动生成：

```bash
# 每天00:00 - 状态重置
openclaw cron add \
  --name "[scenario]_state_reset" \
  --schedule "cron:0 0 * * *:Asia/Shanghai" \
  --message "重置CRON状态：将memory/cron-execution-state.json中所有任务重置为pending" \
  --target isolated

# 用户指定的CRON任务
openclaw cron add \
  --name "[scenario]_task_[时间]" \
  --schedule "cron:[分] [时] * * *:Asia/Shanghai" \
  --message "[任务描述]. 1)检查状态文件 2)执行任务 3)更新状态为completed 4)发送飞书通知到[群组]" \
  --target isolated

# HEARTBEAT触发任务（每个CRON后+10分钟）
openclaw cron add \
  --name "[scenario]_heartbeat_[时间]" \
  --schedule "cron:[分+10] [时] * * *:Asia/Shanghai" \
  --message "触发HEARTBEAT检查：阅读HEARTBEAT.md执行补充扫描" \
  --target isolated

# Git自动提交（如需要）
openclaw cron add \
  --name "[scenario]_git_commit" \
  --schedule "cron:0 20 * * *:Asia/Shanghai" \
  --message "Git自动提交：cd [工作区路径] && git add . && git commit -m 'Daily update' && git push" \
  --target isolated

# 自我进化任务（默认启用）
# 每日数据分析
openclaw cron add \
  --name "[scenario]_daily_analysis" \
  --schedule "cron:30 20 * * *:Asia/Shanghai" \
  --message "每日数据分析：1)读取今日执行日志 2)分析执行效率 3)生成优化建议 4)如置信度>0.8则自动应用优化 5)发送优化报告" \
  --target isolated

# 周度策略优化
openclaw cron add \
  --name "[scenario]_weekly_optimization" \
  --schedule "cron:30 20 * * 0:Asia/Shanghai" \
  --message "周度策略优化：1)汇总本周所有数据 2)深度分析趋势 3)生成策略优化方案 4)更新相关文档 5)发送优化报告" \
  --target isolated

# 月度策略升级
openclaw cron add \
  --name "[scenario]_monthly_upgrade" \
  --schedule "cron:30 20 1 * *:Asia/Shanghai" \
  --message "月度策略升级：1)分析整月数据趋势 2)对比行业最佳实践 3)生成重大策略调整 4)全面更新文档体系 5)规划下月目标" \
  --target isolated
```

#### 4.2 执行配置命令

自动执行上述命令，记录每个任务的job_id。

### Step 5: 验证与通知

#### 5.1 验证检查

- [ ] 所有文件创建成功
- [ ] CRON任务配置正确（`openclaw cron list`）
- [ ] 状态文件格式正确
- [ ] 飞书通知测试成功

#### 5.2 发送启动通知

```
✅ [场景]双引擎系统搭建完成！

📁 工作区：[路径]
📊 配置文件：7个文件已创建
⏰ CRON任务：[N]个任务已配置
   - 00:00 状态重置
   - [其他时间点任务...]
   - 20:30 每日自我分析 ⭐
   - 周日20:30 周度策略优化 ⭐
   - 每月1日20:30 月度升级 ⭐
🔔 通知目标：[飞书群组]
🧬 自我进化：已启用（自动分析+优化）

🚀 系统已启动，下次执行：[最近的时间点]

💡 使用提示：
- 发送 HEARTBEAT 查看当前状态
- 说"查看配置"查看所有CRON任务
- 说"添加任务 [时间] [任务]"增加新任务

🔄 自我进化：
- 系统会自动分析执行数据
- 每天20:30生成优化建议
- 自动应用高置信度优化
- 持续迭代，越用越智能
```

---

## 后续管理命令

用户可以使用的自然语言命令：

### 查看状态
```
查看当前配置
→ 列出所有CRON任务、状态文件、下次执行时间
```

### 添加任务
```
再加一个每天下午3点检查邮件的任务
→ 自动添加CRON 15:00任务
```

### 修改任务
```
把日报时间改到8点
→ 更新CRON时间，同步更新HEARTBEAT.md
```

### 暂停/恢复
```
暂停晚上10点的任务
→ 更新CRON enabled为false
```

### 重置状态
```
重置状态文件
→ 备份当前状态，重置为pending
```

---

## 示例完整对话

### 示例1: 系统监控

**用户输入**
```
我要搭建服务器监控：
- 每30分钟检查CPU、内存、磁盘使用率
- 每天09:00生成系统健康日报
- CPU超过80%时立即告警
- 飞书通知到 chat:oc_xxx
- 工作区 /Users/alice/system-monitor
```

**Agent自动执行**

**Step 1**: 解析需求
```
场景：系统监控
HEARTBEAT：CPU/内存/磁盘检查
CRON：09:00健康日报
告警：CPU>80%
```

**Step 2**: 设计架构
```
HEARTBEAT任务：系统资源检查
CRON任务：报告生成
状态管理：需要
文件清单：6个
```

**Step 3**: 创建文件
```
✅ HEARTBEAT.md（监控指令）
✅ memory/cron-execution-state.json
✅ memory/metrics/（性能数据目录）
✅ SOUL.md（系统管理员人设）
✅ AGENTS.md（监控指南）
```

**Step 4**: 配置CRON（4个任务）
```
✅ 00:00 状态重置
✅ 09:00 健康日报
✅ 09:10 HEARTBEAT触发
✅ 20:00 Git提交
```

**Step 5**: 验证通知
```
✅ 系统监控搭建完成！
   - 下次执行：09:00
   - 监控指标：CPU/内存/磁盘
   - 告警阈值：CPU>80%
```

---

### 示例2: 数据同步

**用户输入**
```
我要搭建数据同步：
- 每30分钟检查源数据库变化
- 每小时自动同步到目标库
- 每天09:00生成同步报告
- 飞书通知到 chat:oc_xxx
- 工作区 /Users/bob/data-sync
```

**Agent自动执行**

**Step 1**: 解析需求
```
场景：数据同步
HEARTBEAT：检查数据变化
CRON：每小时同步、09:00报告
```

**Step 2**: 设计架构
```
HEARTBEAT任务：数据变化检测
CRON任务：同步执行+报告生成
状态管理：需要
文件清单：6个
```

**Step 3**: 创建文件
```
✅ HEARTBEAT.md（数据检查指令）
✅ memory/cron-execution-state.json
✅ memory/sync-logs/（同步日志）
✅ SOUL.md（数据工程师人设）
✅ AGENTS.md（同步指南）
```

**Step 4**: 配置CRON（6个任务）
```
✅ 00:00 状态重置
✅ 每小时 数据同步
✅ 09:00 同步报告
✅ 20:00 Git提交
```

**Step 5**: 验证通知
```
✅ 数据同步系统搭建完成！
   - 同步频率：每小时
   - 报告时间：09:00
```

---

### 示例3: 电商竞品监控

**用户输入**
```
我要搭建一个电商竞品监控系统：
- 每30分钟检查竞品网站价格和促销活动
- 每天早上9点生成竞品动态日报
- 每周一上午10点生成周报
- 飞书通知到 chat:oc_xxx
- 工作区 /Users/alice/competitor-monitor
- 需要自动Git提交
```

**Agent自动执行**

**Step 1**: 解析需求
```
场景：电商竞品监控
HEARTBEAT：网站价格检查、促销活动扫描
CRON：09:00日报、周一10:00周报、20:00 Git提交
```

**Step 2**: 设计架构
```
HEARTBEAT任务：浏览器访问竞品网站，提取价格信息
CRON任务：数据分析+报告生成
状态管理：需要（防重复检查）
文件清单：7个（包含周报模板）
```

**Step 3**: 创建文件
```
✅ HEARTBEAT.md（网站抓取指令）
✅ memory/cron-execution-state.json（5个时段）
✅ memory/weekly-report-template.md（周报模板）
✅ SOUL.md（竞品分析师人设）
✅ AGENTS.md（监控指南）
```

**Step 4**: 配置CRON（5个任务）
```
✅ 00:00 状态重置
✅ 09:00 竞品日报
✅ 09:10 HEARTBEAT触发
✅ 10:00 周一周报
✅ 20:00 Git提交
```

**Step 5**: 验证通知
```
✅ 电商竞品监控系统搭建完成！
   - 下次执行：明天09:00
   - 监控网站：[竞品列表]
   - 通知群组：chat:oc_xxx
```

---

## 关键技术点

### 1. 需求解析逻辑

从自然语言提取：
- 时间表达式 → CRON时间
- 频率词汇 → HEARTBEAT vs CRON
- 动作描述 → 任务指令
- 平台名称 → 具体操作

### 2. 架构决策树

```
用户说"30分钟/实时/持续监控" → HEARTBEAT
用户说"每天/定时/周期" → CRON
用户说"发帖/发布" → 需要content-calendar
用户说"报告/总结" → CRON深度任务
用户说"Git提交" → 自动添加20:00任务
```

### 3. 文件模板系统

预定义模板，根据需求填充变量：
- `{scenario}` → 场景名称
- `{heartbeat_tasks}` → HEARTBEAT任务列表
- `{cron_slots}` → CRON时间点列表
- `{feishu_group}` → 飞书群组ID
- `{workspace_path}` → 工作区路径

### 4. 错误处理

- 文件创建失败 → 重试3次
- CRON配置失败 → 记录错误，继续其他任务
- 权限不足 → 提示用户授权
- 路径不存在 → 自动创建目录

---

## 扩展性设计

### 插件机制

可以扩展支持：
- `browser-automation`: 浏览器操作模板
- `api-monitoring`: API监控模板
- `data-analysis`: 数据分析模板
- `multi-platform`: 多平台监控模板

### 模板库

预定义场景模板：
- `reddit-ops`: Reddit运营（当前示例）
- `competitor-monitor`: 竞品监控
- `social-media`: 社媒管理
- `content-creator`: 内容创作
- `customer-support`: 客服监控

---

**核心优势**：用户只需描述业务需求，技术细节全部自动化。
