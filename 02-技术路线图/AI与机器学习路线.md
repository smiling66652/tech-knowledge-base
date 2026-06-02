# AI与机器学习路线

> 基于GenJi是真想教会你 + 小天fotos的内容体系整理
> 创建时间：2026-04-28

---

## 路线概览

```
零基础 ──→ 入门 ──→ 进阶 ──→ 专家
  │          │         │         │
  ▼          ▼         ▼         ▼
AI认知    AI工具    AI编程    Agent系统
基础建立   实战使用   开发      设计架构
```

---

## 阶段一：零基础 → 入门（1-2周）

### 学习目标
- 理解AI的基本概念和发展历程
- 学会使用主流AI对话工具
- 建立AI学习的认知框架

### 推荐视频

| 视频 | UP主 | 难度 | 关键词 |
|------|------|------|--------|
| AI大模型原理 | GenJi | ⭐⭐ | 大模型、Transformer、原理 |
| ChatGPT深度解析 | GenJi | ⭐⭐ | ChatGPT、GPT-4、提示词 |
| AI工具使用入门 | 小in分享 | ⭐ | AI工具、效率、入门 |
| 速通Sora | GenJi | ⭐⭐ | Sora、AI视频、OpenAI |

### 必备工具
| 工具 | 用途 | 获取方式 |
|------|------|----------|
| ChatGPT | AI对话 | https://chat.openai.com |
| Claude | AI对话 | https://claude.ai |
| Kimi/通义千问 | 国产AI对话 | 免费 |
| AI工具导航 | 工具发现 | 各AI工具导航网站 |

### 实践项目
- [ ] 用ChatGPT完成一个完整的对话任务（如写作助手、翻译助手）
- [ ] 尝试GenJi的prompt方法论，写出3个高质量提示词
- [ ] 对比ChatGPT和Claude的回复质量差异

### 避坑指南
- ❌ 不要期望AI能100%准确，学会验证AI的输出
- ❌ 不要把敏感信息发给AI
- ✅ 从简单的任务开始，逐步增加复杂度
- ✅ 保存好的prompt，建立自己的prompt库

---

## 阶段二：入门 → 进阶（2-4周）

### 学习目标
- 掌握AI绘画工具的使用
- 学会AI视频/动画制作
- 理解MCP协议和AI工具调用

### 推荐视频

| 视频 | UP主 | 难度 | 关键词 |
|------|------|------|--------|
| AI动画制作课程 | GenJi | ⭐⭐⭐ | AI动画、ComfyUI |
| SD花活集 | GenJi | ⭐⭐⭐ | Stable Diffusion、创意 |
| MCP协议深度解析 | 小天fotos | ⭐⭐⭐⭐ | MCP、工具调用 |
| Claude Code入门 | 小天fotos | ⭐⭐⭐ | Claude Code、AI编程 |

### 必备工具
| 工具 | 用途 | 获取方式 |
|------|------|----------|
| Midjourney | AI绘画 | Discord Bot（付费） |
| Stable Diffusion | AI图像生成 | 本地部署（免费） |
| ComfyUI | AI工作流 | GitHub开源 |
| Claude Code | AI编程 | Claude Pro订阅 |
| n8n | AI自动化 | 本地Docker部署 |

### 实践项目
- [ ] 用Midjourney/SD生成5张高质量图像
- [ ] 用ComfyUI搭建一个简单的AI动画工作流
- [ ] 理解MCP协议，安装一个MCP Server
- [ ] 用Claude Code完成一个小型编程任务

### 避坑指南
- ❌ SD本地部署需要至少8GB显存的GPU
- ❌ Midjourney每月$10-30，先试用再决定
- ✅ ComfyUI工作流从模板开始，不要从零搭建
- ✅ Claude Code需要Claude Pro订阅，可以先免费体验

---

## 阶段三：进阶 → 专家（4-8周）

### 学习目标
- 掌握Claude Code Skill开发
- 理解多Agent系统设计
- 能独立开发AI工具链

### 推荐视频

| 视频 | UP主 | 难度 | 关键词 |
|------|------|------|--------|
| Claude Code Skill完整教程 | 小天fotos | ⭐⭐⭐⭐ | Skill开发、自动化 |
| Agent Teams蜂群模式 | 小天fotos | ⭐⭐⭐⭐⭐ | Agent协作 |
| OpenClaw工作流 | 小天fotos | ⭐⭐⭐⭐ | 工作流自动化 |
| Qwen3.5实战测评 | 小天fotos | ⭐⭐⭐ | 大模型对比 |

### 必备工具
| 工具 | 用途 | 获取方式 |
|------|------|----------|
| Claude Code | AI编程 | Anthropic |
| Claude Desktop | MCP客户端 | Anthropic |
| OpenClaw | 工作流引擎 | GitHub开源 |
| VS Code + 插件 | 开发环境 | 微软 |

### 实践项目
- [ ] 开发第一个Claude Code Skill（如自动文件整理Skill）
- [ ] 搭建一个MCP Server（如天气查询MCP）
- [ ] 用OpenClaw构建一个自动化工作流
- [ ] 测试多Agent协作模式

### 避坑指南
- ❌ Skill开发初期不要追求复杂功能，先从简单工具开始
- ❌ MCP Server调试需要耐心，善用日志
- ✅ 参考AGENT-SKILLS-EXAMPLES仓库的示例代码
- ✅ 先在测试环境验证，再应用到生产环境

---

## 阶段四：专家级（持续学习）

### 学习目标
- 构建完整的AI工具生态
- 设计复杂的Agent系统
- 将AI能力集成到实际项目中

### 学习方向

| 方向 | 内容 | UP主参考 |
|------|------|----------|
| AI Agent架构 | 多Agent系统、任务编排、记忆管理 | 小天fotos |
| AI创作全流程 | AI绘画+AI视频+AI配音 | GenJi |
| AI自动化 | 工作流编排、定时任务、事件触发 | 小天fotos + 技术爬爬虾 |
| AI应用开发 | MCP Server开发、API集成 | 小天fotos + 技术爬爬虾 |

### 实践项目
- [ ] 开发完整的AI Agent系统
- [ ] 构建AI辅助的内容创作工作流
- [ ] 将AI能力集成到现有项目中
- [ ] 贡献开源AI项目

---

## 学习资源汇总

### 按UP主分类

#### GenJi（理论基础 + AI创作）
| 阶段 | 必看视频 |
|------|----------|
| 入门 | AI大模型原理、ChatGPT深度解析 |
| 进阶 | AI动画制作课程、SD花活集 |
| 专家 | 声音克隆教程、AI视频全流程 |

#### 小天fotos（实战开发 + 前沿探索）
| 阶段 | 必看视频 |
|------|----------|
| 入门 | Claude Code入门、MCP协议解析 |
| 进阶 | Skill完整教程、OpenClaw工作流 |
| 专家 | Agent Teams、自定义MCP开发 |

### 推荐学习顺序

```
第1周：AI基础认知（GenJi原理视频）
第2周：AI工具使用（ChatGPT + Claude + AI绘画入门）
第3周：AI编程入门（Claude Code + MCP基础）
第4周：Skill开发实战（第一个Skill项目）
第5周：Agent系统探索（多Agent协作）
第6周：综合项目（将AI集成到实际项目中）
第7-8周：进阶提升（OpenClaw + 高级MCP）
持续：跟踪小天fotos的新视频，保持前沿敏感度
```

---

## 评估检查清单

### 入门级 ✅
- [ ] 能解释大模型的基本原理
- [ ] 能熟练使用ChatGPT/Claude
- [ ] 写出3个以上高质量提示词
- [ ] 了解MCP协议的基本概念

### 进阶级 ✅
- [ ] 能用AI绘画工具生成高质量图像
- [ ] 能搭建ComfyUI工作流
- [ ] 能开发简单的Claude Code Skill
- [ ] 理解Agent系统设计原则

### 专家级 ✅
- [ ] 能独立设计多Agent系统
- [ ] 能开发MCP Server
- [ ] 能构建AI自动化工作流
- [ ] 能将AI能力集成到复杂项目中

---

*本文档将随UP主的新视频和技术发展持续更新。*
