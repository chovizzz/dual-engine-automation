# 场景模板库

通用双引擎模板，支持监控、通知、自动化等各种场景。

## 模板1: 社媒运营系统 (social-media-ops)

### 适用场景
- Twitter/X运营
- LinkedIn内容管理
- Instagram/Facebook监控
- 多平台社媒统一运营
- 定时内容发布
- 互动管理

### 用户需求示例
```
我要搭建社媒运营系统，30分钟检查私信和@提及，每天10点和15点发布内容，周一10点发周报
```

### 自动生成的架构

#### HEARTBEAT任务
- 检查私信/消息
- 监控@提及和评论
- 追踪热门话题
- 识别互动机会

#### CRON任务（6-8个）
| 时间 | 任务 | 说明 |
|------|------|------|
| 00:00 | 状态重置 | 每日初始化 |
| [用户指定] | 内容发布 | 定时发帖 |
| [用户指定+10min] | HEARTBEAT触发 | 补充扫描 |
| 周一[时间] | 周报生成 | 如需要 |
| 20:00 | Git提交 | 自动备份 |

#### 生成文件
```
social-media-ops/
├── HEARTBEAT.md              # 社媒监控指令
├── memory/
│   ├── cron-execution-state.json
│   ├── content-calendar.md      # 内容日历
│   ├── inbox/                  # 消息归档
│   └── analytics/              # 数据分析
├── SOUL.md                   # 社媒运营人设
└── AGENTS.md                 # 运营指南
```

---

## 模板2: 系统监控告警 (system-monitor)

### 适用场景
- 服务器性能监控（CPU/内存/磁盘）
- 服务健康检查
- 异常告警通知
- 系统资源管理

### 用户需求示例
```
我要搭建系统监控，30分钟检查CPU内存磁盘，每天9点生成健康报告，CPU超80%告警
```

### 自动生成的架构

#### HEARTBEAT任务
- 检查CPU使用率
- 检查内存使用率
- 检查磁盘使用率
- 检查服务状态
- 异常时立即告警

#### CRON任务（7-9个）
| 时间 | 任务 | 说明 |
|------|------|------|
| 00:00 | 状态重置 | 每日初始化 |
| 09:00 | 健康日报 | 生成系统报告 |
| 09:10 | HEARTBEAT触发 | 补充检查 |
| 20:00 | Git提交 | 自动备份 |
| **20:30** | **每日分析** | **自我进化：分析当日监控数据** |
| **周日20:30** | **周度优化** | **自我进化：优化告警策略** |
| **每月1日20:30** | **月度升级** | **自我进化：策略升级** |

#### 生成文件
```
system-monitor/
├── HEARTBEAT.md              # 监控检查指令
├── memory/
│   ├── cron-execution-state.json
│   ├── metrics/                # 性能指标记录
│   │   ├── cpu/               # CPU历史数据
│   │   ├── memory/            # 内存历史数据
│   │   └── disk/              # 磁盘历史数据
│   └── alerts/                 # 告警记录
├── SOUL.md                   # 系统管理员人设
└── AGENTS.md                 # 监控指南
```

---

## 模板3: 数据同步 (data-sync)

### 适用场景
- 数据库同步
- 文件同步
- API数据拉取
- 数据备份

### 用户需求示例
```
我要搭建数据同步，30分钟检查源库变化，每小时自动同步，每天9点生成同步报告
```

### 自动生成的架构

#### HEARTBEAT任务
- 检查源数据变化
- 监控同步状态
- 检查同步延迟
- 异常告警

#### CRON任务（8-10个）
| 时间 | 任务 | 说明 |
|------|------|------|
| 00:00 | 状态重置 | 每日初始化 |
| 每小时 | 数据同步 | 定时同步任务 |
| 09:00 | 同步报告 | 生成日报 |
| 20:00 | Git提交 | 自动备份 |
| **20:30** | **每日分析** | **自我进化：分析同步效率** |
| **周日20:30** | **周度优化** | **自我进化：优化同步策略** |
| **每月1日20:30** | **月度升级** | **自我进化：架构升级** |

#### 生成文件
```
data-sync/
├── HEARTBEAT.md              # 数据检查指令
├── memory/
│   ├── cron-execution-state.json
│   ├── sync-logs/              # 同步日志
│   ├── failed-records/         # 失败记录
│   └── reports/                # 同步报告
├── SOUL.md                   # 数据工程师人设
└── AGENTS.md                 # 同步指南
```

---

## 模板4: 定时任务调度 (task-scheduler)

### 适用场景
- 定时脚本执行
- 批量任务处理
- 定时数据清理
- 自动化工作流

### 用户需求示例
```
我要搭建定时任务，30分钟检查队列状态，每天凌晨2点执行清理，周一9点生成统计
```

### 自动生成的架构

#### HEARTBEAT任务
- 检查任务队列状态
- 监控执行进度
- 检查失败任务
- 资源使用监控

#### CRON任务（7-9个）
| 时间 | 任务 | 说明 |
|------|------|------|
| 00:00 | 状态重置 | 每日初始化 |
| 02:00 | 数据清理 | 定时清理任务 |
| 周一09:00 | 周报生成 | 生成统计报告 |
| 20:00 | Git提交 | 自动备份 |
| **20:30** | **每日分析** | **自我进化：分析任务执行效率** |
| **周日20:30** | **周度优化** | **自我进化：优化调度策略** |
| **每月1日20:30** | **月度升级** | **自我进化：容量规划** |

#### 生成文件
```
task-scheduler/
├── HEARTBEAT.md              # 队列检查指令
├── memory/
│   ├── cron-execution-state.json
│   ├── queue/                  # 队列状态
│   ├── logs/                   # 执行日志
│   └── reports/                # 执行报告
├── SOUL.md                   # 调度员人设
└── AGENTS.md                 # 调度指南
```

---

## 模板5: Reddit运营系统 (reddit-ops)

### 适用场景
- Reddit多板块监控
- GEO/SEO内容运营
- 定时发帖
- 社区互动

### 用户需求示例
```
我要搭建Reddit GEO运营系统，30分钟扫描TechSEO和GEO板块，每天9点发报告，晚上10点发帖
```

### 自动生成的架构

#### HEARTBEAT任务
- 扫描r/TechSEO、r/GenEngineOptimization、r/bigseo
- 检查热门帖子（50+ upvotes）
- 识别重大发现（研究发布、竞品动态）

#### CRON任务（11个）
| 时间 | 任务 | 说明 |
|------|------|------|
| 00:00 | 状态重置 | 每日初始化 |
| 09:00 | 生成日报 | 深度分析 |
| 09:10 | HEARTBEAT触发 | 补充扫描 |
| 12:00 | 午间学习 | 热点精读 |
| 14:00 | 权威建设 | 专业参与 |
| 18:00 | 晚间复盘 | 数据汇总 |
| 20:00 | Git提交 | 自动备份 |
| 22:00 | 发帖执行 | 检查发布 |
| **20:30** | **每日分析** | **自我进化：分析发帖效果** |
| **周日20:30** | **周度优化** | **自我进化：优化内容策略** |
| **每月1日20:30** | **月度升级** | **自我进化：运营策略升级** |

#### 生成文件清单
```
reddit-ops/
├── HEARTBEAT.md              # Reddit扫描指令
├── memory/
│   ├── cron-execution-state.json    # 8个时段状态
│   ├── content-calendar.md          # 发帖计划
│   ├── post-performance-log.md      # 表现追踪
│   ├── 2026-02-14.md               # 每日报告
│   └── learning/
│       ├── hot-posts/              # 热点归档
│       ├── insights/               # 痛点挖掘
│       └── competitors/            # 竞品情报
├── SOUL.md                   # Reddit运营专家人设
├── AGENTS.md                 # 运营指南
└── BROWSER_OPERATION_STANDARD.md   # 浏览器规范
```

---

## 模板2: 竞品监控系统 (competitor-monitor)

### 适用场景
- 竞品网站监控
- 价格追踪
- 促销活动监控
- 产品动态跟踪

### 用户需求示例
```
我要监控竞品网站，每30分钟检查价格和促销，每天早上9点生成日报
```

### 自动生成的架构

#### HEARTBEAT任务
- 浏览器访问竞品网站
- 提取价格信息
- 识别促销活动变化

#### CRON任务（7个）
| 时间 | 任务 | 说明 |
|------|------|------|
| 00:00 | 状态重置 | 每日初始化 |
| 09:00 | 竞品日报 | 数据汇总 |
| 09:10 | HEARTBEAT触发 | 补充扫描 |
| 20:00 | Git提交 | 自动备份 |
| **20:30** | **每日分析** | **自我进化：分析监控效率** |
| **周日20:30** | **周度优化** | **自我进化：优化监控策略** |
| **每月1日20:30** | **月度升级** | **自我进化：竞品分析升级** |

#### 生成文件清单
```
competitor-monitor/
├── HEARTBEAT.md              # 网站抓取指令
├── memory/
│   ├── cron-execution-state.json    # 4个时段状态
│   ├── competitor-data/            # 竞品数据
│   │   ├── prices/                # 价格记录
│   │   └── promotions/            # 促销记录
│   └── daily-reports/              # 日报归档
├── SOUL.md                   # 竞品分析师人设
└── AGENTS.md                 # 监控指南
```

---

## 模板3: 社媒管理系统 (social-media)

### 适用场景
- 多平台社媒运营
- 定时内容发布
- 互动管理
- 数据报告

### 用户需求示例
```
我要管理Twitter和LinkedIn账号，每30分钟检查消息，每天上午10点和下午3点发布内容
```

### 自动生成的架构

#### HEARTBEAT任务
- 检查私信和@提及
- 监控热门话题
- 识别互动机会

#### CRON任务（9个）
| 时间 | 任务 | 说明 |
|------|------|------|
| 00:00 | 状态重置 | 每日初始化 |
| 10:00 | 上午发布 | 内容发布 |
| 10:10 | HEARTBEAT触发 | 补充扫描 |
| 15:00 | 下午发布 | 内容发布 |
| 15:10 | HEARTBEAT触发 | 补充扫描 |
| 20:00 | Git提交 | 自动备份 |
| **20:30** | **每日分析** | **自我进化：分析发布效果** |
| **周日20:30** | **周度优化** | **自我进化：优化内容策略** |
| **每月1日20:30** | **月度升级** | **自我进化：运营策略升级** |

#### 生成文件清单
```
social-media/
├── HEARTBEAT.md              # 社媒监控指令
├── memory/
│   ├── cron-execution-state.json    # 6个时段状态
│   ├── content-calendar.md          # 内容日历
│   ├── post-performance-log.md      # 发布记录
│   └── inbox/                      # 消息归档
├── SOUL.md                   # 社媒运营人设
└── AGENTS.md                 # 社媒指南
```

---

## 模板4: 内容创作系统 (content-creator)

### 适用场景
- 热点追踪
- 内容灵感收集
- 定时发布
- 效果分析

### 用户需求示例
```
我要做科技内容创作，每30分钟扫描HackerNews和Reddit寻找灵感，每天下午2点发布文章
```

### 自动生成的架构

#### HEARTBEAT任务
- 扫描HackerNews热门
- 扫描Reddit r/technology
- 收集内容灵感

#### CRON任务（7个）
| 时间 | 任务 | 说明 |
|------|------|------|
| 00:00 | 状态重置 | 每日初始化 |
| 14:00 | 文章发布 | 内容发布 |
| 14:10 | HEARTBEAT触发 | 补充扫描 |
| 20:00 | Git提交 | 自动备份 |
| **20:30** | **每日分析** | **自我进化：分析内容效果** |
| **周日20:30** | **周度优化** | **自我进化：优化创作策略** |
| **每月1日20:30** | **月度升级** | **自我进化：内容方向调整** |

#### 生成文件清单
```
content-creator/
├── HEARTBEAT.md              # 灵感收集指令
├── memory/
│   ├── cron-execution-state.json    # 4个时段状态
│   ├── content-calendar.md          # 发布计划
│   ├── ideas/                      # 灵感库
│   └── drafts/                     # 草稿箱
├── SOUL.md                   # 内容创作者人设
└── AGENTS.md                 # 创作指南
```

---

## 模板5: 客服监控系统 (customer-support)

### 适用场景
- 客户反馈监控
- 问题响应
- 服务质量跟踪
- 周报生成

### 用户需求示例
```
我要监控客户反馈，每30分钟检查支持邮箱和Twitter，每周一上午10点生成服务周报
```

### 自动生成的架构

#### HEARTBEAT任务
- 检查支持邮箱
- 监控Twitter @提及
- 识别紧急问题

#### CRON任务（5个）
| 时间 | 任务 | 说明 |
|------|------|------|
| 00:00 | 状态重置 | 每日初始化 |
| 09:00 | 每日汇总 | 问题统计 |
| 09:10 | HEARTBEAT触发 | 补充扫描 |
| 10:00 | 周一 | 服务周报 |
| 20:00 | Git提交 | 自动备份 |
| **20:30** | **每日分析** | **自我进化：分析响应效率** |
| **周日20:30** | **周度优化** | **自我进化：优化服务策略** |
| **每月1日20:30** | **月度升级** | **自我进化：服务质量升级** |

#### 生成文件清单
```
customer-support/
├── HEARTBEAT.md              # 反馈监控指令
├── memory/
│   ├── cron-execution-state.json    # 5个时段状态
│   ├── tickets/                    # 工单记录
│   ├── weekly-reports/             # 周报归档
│   └── issues/                     # 问题分类
├── SOUL.md                   # 客服专家人设
└── AGENTS.md                 # 服务指南
```

---

## 模板选择逻辑

Agent如何自动选择模板：

```python
def select_template(requirements):
    # 系统监控类
    if "服务器" in requirements or "CPU" in requirements or "内存" in requirements or "监控" in requirements:
        return "system-monitor"
    elif "磁盘" in requirements or "告警" in requirements:
        return "system-monitor"
    
    # 数据同步类
    elif "同步" in requirements or "数据库" in requirements or "备份" in requirements:
        return "data-sync"
    elif "API" in requirements or "数据拉取" in requirements:
        return "data-sync"
    
    # 定时任务类
    elif "定时任务" in requirements or "任务调度" in requirements or "批处理" in requirements:
        return "task-scheduler"
    elif "清理" in requirements or "脚本" in requirements:
        return "task-scheduler"
    
    # 运营类
    elif "Reddit" in requirements or "GEO" in requirements:
        return "reddit-ops"
    elif "竞品" in requirements or "价格" in requirements:
        return "competitor-monitor"
    elif "Twitter" in requirements or "LinkedIn" in requirements or "社媒" in requirements:
        return "social-media"
    elif "内容" in requirements or "创作" in requirements or "文章" in requirements:
        return "content-creator"
    elif "客服" in requirements or "支持" in requirements:
        return "customer-support"
    
    # 默认自定义
    else:
        return "custom"  # 自定义架构
```

---

## 模板扩展方法

添加新模板的步骤：

1. **定义场景**：明确适用场景和用户需求
2. **设计架构**：确定HEARTBEAT和CRON任务
3. **创建模板文件**：
   - `templates/[template-name]/HEARTBEAT.md`
   - `templates/[template-name]/SOUL.md`
   - `templates/[template-name]/AGENTS.md`
4. **更新选择逻辑**：在select_template函数中添加判断
5. **测试验证**：用示例需求测试模板生成

---

所有模板都遵循**双引擎架构**：
- HEARTBEAT = 实时响应（30分钟）
- CRON = 定时执行（按需配置）
- 状态管理 = 防重复机制
- 通知路由 = 个人+群组
