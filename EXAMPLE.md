# 完整示例：Reddit GEO运营系统

## 用户输入

```
我要搭建一个Reddit GEO运营自动化系统：
- 每30分钟扫描r/TechSEO、r/GenEngineOptimization、r/bigseo热点
- 每天09:00生成详细日报，12:00午间学习，18:00晚间复盘
- 每天22:00/02:00/08:00检查发帖（对应EST最佳时间）
- 飞书通知到 chat:oc_ac50ef0887f1d1750a94a5aaecfdb959
- 工作区路径 /Users/javis/.openclaw/workspace
- 需要自动Git提交
- 所有Reddit内容必须用英文
```

---

## Agent自动执行流程

### Step 1: 解析需求

```python
requirements = {
    "scenario": "Reddit GEO运营",
    "heartbeat_tasks": [
        "扫描r/TechSEO热点",
        "扫描r/GenEngineOptimization热点",
        "扫描r/bigseo热点"
    ],
    "cron_tasks": [
        {"time": "09:00", "task": "生成详细日报"},
        {"time": "12:00", "task": "午间学习"},
        {"time": "18:00", "task": "晚间复盘"},
        {"time": "22:00", "task": "检查发帖"},
        {"time": "02:00", "task": "检查发帖"},
        {"time": "08:00", "task": "检查发帖"}
    ],
    "feishu_group": "chat:oc_ac50ef0887f1d1750a94a5aaecfdb959",
    "workspace_path": "/Users/javis/.openclaw/workspace",
    "need_git": True,
    "need_posting": True,
    "language": "英文",
    "platforms": ["Reddit"]
}
```

### Step 2: 选择模板 → reddit-ops

### Step 3: 生成文件

---

## 生成的文件1: HEARTBEAT.md

```markdown
# HEARTBEAT.md - Reddit GEO运营主动监控系统

## 🔔 HEARTBEAT执行指令（每30分钟）

当收到HEARTBEAT时，按以下流程执行：

### Step 0: 状态文件检查（防重复机制）
1. 读取 `memory/cron-execution-state.json`
2. 检查当前时间是否在CRON窗口期（±5分钟）
3. 检查该时段状态：
   - completed → CRON已执行，回复 HEARTBEAT_OK
   - pending → 继续执行检查
   - 无记录 → 继续执行检查
4. 更新状态为 executing (by heartbeat)

### Step 1: Reddit多板块扫描
使用browser工具扫描：
- r/TechSEO (https://www.reddit.com/r/TechSEO)
- r/GenEngineOptimization (https://www.reddit.com/r/GenEngineOptimization)
- r/bigseo (https://www.reddit.com/r/bigseo)

检查内容：
- 热门帖子（按Hot排序）
- 新发布帖子
- 高价值讨论（50+ upvotes）

### Step 2: 多平台监控
扫描以下平台的GEO/AEO相关更新：
- Bing AI Performance Dashboard
- Google SGE更新
- ChatGPT新功能
- Claude更新
- Perplexity动态
- 行业新闻

### Step 3: 判断重大发现

**重大发现标准：**
- ✅ 新AI平台功能发布（Bing/Google/ChatGPT等）
- ✅ 引用机制重大变化
- ✅ 行业报告/研究发布
- ✅ 竞品重大动作
- ✅ Reddit高价值讨论（50+ upvotes）
- ✅ 新的用户痛点集中出现
- ✅ 当前是最佳发帖时间

### Step 4: 通知路由

| 情况 | 通知目标 | 内容 |
|------|---------|------|
| 无重大发现 | 当前会话（个人） | HEARTBEAT_OK |
| 有重大发现 | 个人 + chat:oc_ac50ef0887f1d1750a94a5aaecfdb959 | 详细报告 |

### Step 5: 状态更新
更新 `memory/cron-execution-state.json`：
- 状态改为 completed (by heartbeat)
- 更新时间戳
- 记录执行摘要

### Step 6: 可选 - 即时参与
如发现有价值的讨论且符合参与条件：
1. 阅读帖子全文
2. 准备专业回复（英文）
3. 发送前自检（SOUL.md规则）
4. 提交回复

---

## 📝 通知模板

### HEARTBEAT_OK（个人）
```
⏰ HEARTBEAT检查完成 (HH:MM)

📊 扫描结果：无重大发现
📋 状态：正常运行

下次检查：30分钟后
```

### 重大发现报告（个人+群组）
```
🔥 HEARTBEAT重大发现 (HH:MM)

📊 扫描完成：[N]个板块

🎯 重大发现：
【板块】标题
🔗 链接
💡 核心内容

📋 其他发现：[简要列表]

⏰ 下次扫描：30分钟后
```

---

## 📚 参考文档

执行前必读：
- `BROWSER_OPERATION_STANDARD.md` - 浏览器操作规范
- `SOUL.md` - 智能体人设和行为准则
- `AGENTS.md` - 运营指南和检查清单

---

*生成时间：2026-02-14 01:33*  
*模板版本：reddit-ops v1.0*
```

---

## 生成的文件2: memory/cron-execution-state.json

```json
{
  "version": "1.0",
  "date": "2026-02-14",
  "timezone": "Asia/Shanghai",
  "lastResetAt": "2026-02-14T00:58:00+08:00",
  "executions": {
    "00:00": {
      "status": "completed",
      "scheduledTime": "2026-02-14T00:00:00+08:00",
      "executedAt": "2026-02-14T00:58:00+08:00",
      "executor": "cron"
    },
    "06:00": {
      "status": "pending",
      "scheduledTime": "2026-02-14T06:00:00+08:00"
    },
    "06:10": {
      "status": "pending",
      "scheduledTime": "2026-02-14T06:10:00+08:00"
    },
    "09:00": {
      "status": "pending",
      "scheduledTime": "2026-02-14T09:00:00+08:00"
    },
    "09:10": {
      "status": "pending",
      "scheduledTime": "2026-02-14T09:10:00+08:00"
    },
    "12:00": {
      "status": "pending",
      "scheduledTime": "2026-02-14T12:00:00+08:00"
    },
    "14:00": {
      "status": "pending",
      "scheduledTime": "2026-02-14T14:00:00+08:00"
    },
    "18:00": {
      "status": "pending",
      "scheduledTime": "2026-02-14T18:00:00+08:00"
    },
    "20:00": {
      "status": "pending",
      "scheduledTime": "2026-02-14T20:00:00+08:00"
    },
    "21:00": {
      "status": "pending",
      "scheduledTime": "2026-02-14T21:00:00+08:00"
    },
    "22:00": {
      "status": "pending",
      "scheduledTime": "2026-02-14T22:00:00+08:00"
    }
  },
  "metadata": {
    "totalSlots": 11,
    "completedCount": 1,
    "skippedCount": 0,
    "lastUpdated": "2026-02-14T00:58:00+08:00"
  }
}
```

---

## 生成的文件3: memory/content-calendar.md

```markdown
# 内容发布日历

## 发布状态标记

| 标记 | 含义 | 动作 |
|------|------|------|
| 📝 | 计划中 | 等待发布 |
| ✅ | 已发布 | 跳过检查 |
| ⏸️ | 推迟 | 下一时段重试 |
| ❌ | 取消 | 不再尝试 |

## 最佳发布时间（EST）

| 时段 | 时间 | 适合内容 | 北京时间 |
|------|------|---------|---------|
| 早间 | 9:00-11:00 AM | 数据报告 | 前一天22:00 |
| 午间 | 1:00-3:00 PM | 问题讨论 | 次日02:00 |
| 晚间 | 7:00-9:00 PM | 案例研究 | **次日08:00** |
| 周末 | 10AM-12PM | 资源清单 | 当日23:00 |

## 每周发布计划

| 日期 | 时间(EST) | 北京时间 | 内容主题 | 类型 | 目标板块 | 状态 |
|------|----------|---------|---------|------|---------|------|
| 周一 | 9:00 AM | 22:00 | [待规划] | 数据研究 | r/TechSEO | 📝 |
| 周三 | 1:00 PM | 02:00 | [待规划] | 问题讨论 | r/GenEngineOptimization | 📝 |
| 周五 | 7:00 PM | 08:00 | [待规划] | 资源清单 | r/bigseo | 📝 |

## 发帖前检查清单

- [ ] **所有内容必须使用英文**（Reddit海外社媒运营规则）
- [ ] 阅读板块右侧栏Rules
- [ ] 检查Flair要求
- [ ] 搜索确认48h内无相似帖子
- [ ] 标题含具体数字/数据
- [ ] 80%价值+15%方法论+5%产品
- [ ] 无过度格式化
- [ ] 结尾有开放性问题

## 已发布记录

| 日期 | 帖子标题 | 板块 | URL | Upvotes | Comments |
|------|---------|------|-----|---------|----------|
| 2026-02-13 | What tools are you using to monitor AI citations? | r/TechSEO | https://www.reddit.com/r/TechSEO/comments/1r3uuhi/... | 1 | 0 |

---

*生成时间：2026-02-14*  
*语言要求：英文*
```

---

## 生成的文件4: SOUL.md（节选）

```markdown
# SOUL.md - Reddit GEO运营专家

## 🎭 核心人设

我是**Chovi** - Reddit GEO运营专家，专注于Generative Engine Optimization内容运营。

## 🚫 绝对红线

- **中文内容**: 所有Reddit帖子、评论、互动必须使用英文
- **自点赞**: 绝不给自己帖子/评论点赞
- **求Karma**: 绝不公开索要点赞
- **短链接**: 绝不使用bit.ly等

## 💬 语言风格

- **自然表达**: IMO, TBH, 偶尔小瑕疵
- **数据驱动**: 用真实数据说话
- **谦逊语气**: "TBH, I hadn't considered that..."

## 🎯 运营规范

- 80%价值 + 20%工具提及
- 每次发帖前检查板块规则
- 每日点赞3-5条他人优质内容
- 1-2小时内回复评论
```

---

## 生成的CRON任务（12个）

### 1. 每日状态重置
```bash
openclaw cron add \
  --name "reddit_ops_state_reset" \
  --schedule "cron:0 0 * * *:Asia/Shanghai" \
  --message "重置CRON执行状态：备份当前状态文件到memory/state-backups/，重置所有任务为pending" \
  --target isolated
```

### 2. 02:00 发帖执行
```bash
openclaw cron add \
  --name "reddit_ops_post_02_00" \
  --schedule "cron:0 2 * * *:Asia/Shanghai" \
  --message "执行02:00发帖检查：1)检查状态文件 2)读取content-calendar.md 3)如为📝计划中则执行发帖 4)更新状态为completed 5)发送飞书通知到chat:oc_ac50ef0887f1d1750a94a5aaecfdb959" \
  --target isolated
```

### 3. 06:00 每日报告
```bash
openclaw cron add \
  --name "reddit_ops_daily_report" \
  --schedule "cron:0 6 * * *:Asia/Shanghai" \
  --message "生成每日报告：1)检查状态文件 2)汇总运营数据 3)更新memory/YYYY-MM-DD.md 4)状态标记completed 5)发送飞书群组通知" \
  --target isolated
```

### 4-12. [其他9个任务...]

---

## 启动成功通知

```
✅ Reddit GEO运营系统搭建完成！

📁 工作区：/Users/javis/.openclaw/workspace
📊 配置文件：7个文件已创建
⏰ CRON任务：12个任务已配置
   - 00:00 状态重置
   - 02:00/22:00 发帖执行
   - 06:00 每日报告
   - 09:00 上午运营
   - 12:00 午间学习
   - 14:00 权威建设
   - 18:00 晚间复盘
   - 20:00 Git自动提交
   - 21:00 晚间总结
🔔 通知目标：chat:oc_ac50ef0887f1d1750a94a5aaecfdb959
🌐 语言：英文（所有Reddit内容）

🚀 系统已启动，下次执行：02:00（发帖检查）

💡 使用提示：
- 发送 HEARTBEAT 查看当前状态
- 说"查看配置"查看所有CRON任务
- 说"添加任务 [时间] [任务]"增加新任务
- 所有Reddit内容会自动使用英文
```

---

## 总结

**用户只需说一句话**，Agent自动：
1. ✅ 解析需求 → 提取关键信息
2. ✅ 选择模板 → reddit-ops
3. ✅ 生成文件 → 7个配置文件
4. ✅ 配置CRON → 12个定时任务
5. ✅ 验证通知 → 启动成功

**双引擎机制**：
- HEARTBEAT：每30分钟扫描Reddit
- CRON：12个时间点深度任务
- 状态管理：防重复机制
- 通知路由：个人+群组

这就是**对话式自动化搭建**！
