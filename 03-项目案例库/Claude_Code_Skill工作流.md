# Claude Code Skill 工作流

> 来源UP主：小天fotos + 技术爬爬虾
> 创建时间：2026-04-28
> 难度：⭐⭐⭐⭐

---

## 项目概述

Claude Code Skill 是 Anthropic 推出的 AI Agent 技能系统，允许开发者将自定义工具和工作流嵌入 Claude Code，让 AI 助手具备专业领域能力。

### 你将学到
- Skill 系统的架构和设计理念
- 如何从零开发一个实用的 Skill
- Skill 的调试、测试和部署
- Agent Skill 的最佳实践

### 前置要求
- 有 Claude Pro 订阅
- 基本的编程能力（Python 或 TypeScript）
- 了解命令行操作

---

## 一、Skill 系统架构

### 核心概念

```
Skill（技能）
├── SKILL.md          ← 技能描述文件（核心）
├── scripts/          ← 脚本文件（可选）
├── references/       ← 参考文档（可选）
└── assets/           ← 资源文件（可选）
```

### 工作原理

```
用户请求 → Claude Code → 解析SKILL.md → 加载技能指令 → 执行工具调用 → 返回结果
```

### Skill 与 MCP 的区别

| 维度 | Skill | MCP Server |
|------|-------|------------|
| **定位** | AI Agent 的技能描述 | 标准化工具接口 |
| **语言** | Markdown | TypeScript/Python |
| **复杂度** | 低（描述型） | 中高（编程型） |
| **独立性** | 依赖Claude Code | 独立进程 |
| **适用场景** | 工作流、指令模板 | API调用、数据访问 |

---

## 二、开发第一个 Skill

### Step 1：确定 Skill 功能

选择一个具体的功能场景，例如：
- 自动文件整理
- 代码审查助手
- 数据分析报告生成
- 网页内容抓取

### Step 2：创建 SKILL.md

```markdown
# 我的第一个 Skill

## 描述
这个 Skill 的功能描述

## 触发条件
当用户说"XXX"时触发此 Skill

## 指令
1. 步骤一
2. 步骤二
3. 步骤三

## 工具
- 使用 read_file 读取文件
- 使用 write_to_file 写入文件
- 使用 execute_command 执行命令

## 输出格式
- 以 Markdown 表格形式输出结果
```

### Step 3：安装 Skill

```bash
# 方法1：放到用户级 Skill 目录
~/.claude/skills/my-skill/SKILL.md

# 方法2：放到项目级 Skill 目录
./.claude/skills/my-skill/SKILL.md
```

### Step 4：测试 Skill

在 Claude Code 中输入触发语，观察是否正确加载和执行。

---

## 三、高级 Skill 开发

### 带脚本的 Skill

```
my-skill/
├── SKILL.md
└── scripts/
    ├── analyze.py      ← Python分析脚本
    └── format.sh       ← Shell格式化脚本
```

SKILL.md 中引用脚本：
```markdown
## 执行步骤
1. 运行分析脚本：`python scripts/analyze.py`
2. 运行格式化：`bash scripts/format.sh`
3. 读取输出结果
```

### 带参考文档的 Skill

```
my-skill/
├── SKILL.md
└── references/
    ├── api-docs.md     ← API文档
    └── best-practices.md ← 最佳实践
```

SKILL.md 中引用参考文档：
```markdown
## 参考资料
参考 references/api-docs.md 中的API说明
遵循 references/best-practices.md 中的最佳实践
```

---

## 四、实用 Skill 示例

### 示例1：文件管理 Skill

```markdown
# File Manager Skill

## 描述
自动化文件管理助手，用于批量文件操作、智能分类、重复文件清理。

## 触发条件
当用户需要整理文件、批量重命名、清理重复文件时使用。

## 指令
1. 先列出目标目录的文件结构
2. 分析文件类型和大小分布
3. 按用户要求执行操作（分类/重命名/清理）
4. 操作前必须确认

## 安全规则
- 绝对不删除用户未确认的文件
- 操作前必须备份
- 每批最多处理10个文件
```

### 示例2：代码审查 Skill

```markdown
# Code Review Skill

## 描述
自动代码审查助手，检查代码质量、安全问题和最佳实践。

## 触发条件
当用户说"审查代码"、"review"、"检查代码"时触发。

## 指令
1. 读取目标代码文件
2. 检查以下方面：
   - 代码风格一致性
   - 潜在的安全漏洞
   - 性能问题
   - 错误处理完整性
3. 输出审查报告（Markdown表格）

## 输出格式
| 文件 | 行号 | 严重级别 | 问题描述 | 建议修复 |
|------|------|----------|----------|----------|
```

### 示例3：数据分析 Skill

```markdown
# Data Analysis Skill

## 描述
数据分析报告生成器，读取数据文件并生成结构化分析报告。

## 触发条件
当用户提供数据文件并要求分析时触发。

## 指令
1. 读取数据文件（CSV/JSON/Excel）
2. 数据概览：行数、列数、数据类型
3. 统计分析：均值、中位数、分布
4. 异常检测：缺失值、异常值
5. 生成可视化建议
6. 输出分析报告
```

---

## 五、调试和测试

### 常见问题

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| Skill 未加载 | 文件路径错误 | 检查 SKILL.md 是否在正确目录 |
| 触发不灵敏 | 触发条件太严格 | 放宽触发关键词 |
| 执行结果不对 | 指令不够清晰 | 细化步骤，添加示例 |
| 脚本执行失败 | 环境变量缺失 | 在 SKILL.md 中指定环境要求 |

### 调试技巧
- 在 SKILL.md 中添加"调试模式"指令，让 AI 输出更多中间过程
- 用简单的测试用例验证 Skill 的每个步骤
- 逐步增加复杂度，不要一次实现所有功能

---

## 六、参考资源

### 官方资源
- Claude Code 官方文档
- Anthropic 开发者博客
- MCP 协议规范

### 开源示例
- AGENT-SKILLS-EXAMPLES：https://github.com/tech-shrimp/agent-skills-examples
- X-ARTICLE-AUTO-PUBLISHER-SKILL：https://github.com/tech-shrimp/x-article-auto-publisher-skill

### 视频教程
- 小天fotos：Claude Code Skill 完整教程
- 技术爬爬虾：15个好用MCP推荐

---

## 七、与巡检系统的结合

### 可开发的巡检相关 Skill

| Skill名称 | 功能 | 优先级 |
|-----------|------|--------|
| 巡检执行Skill | 触发巡检、运行爬虫脚本 | ★★★★★ |
| 结果分析Skill | 分析巡检结果、生成摘要 | ★★★★☆ |
| 报告生成Skill | 生成HTML可视化报告 | ★★★★☆ |
| 推送通知Skill | 微信/邮件推送巡检结果 | ★★★★★ |
| 配置管理Skill | 管理巡检配置（URL、关键词等） | ★★★☆☆ |

---

*本文档将随Claude Code的更新持续迭代。*
