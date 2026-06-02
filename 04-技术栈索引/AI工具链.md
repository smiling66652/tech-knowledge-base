# AI工具链

> 综合四位UP主内容整理
> 创建时间：2026-04-28

---

## 一、AI对话工具

### 主流工具对比

| 工具 | 开发商 | 定价 | 优势 | UP主关联 |
|------|--------|------|------|----------|
| **Claude** | Anthropic | $20/月 | 长文本、编程、安全 | 小天fotos |
| **ChatGPT** | OpenAI | $20/月 | 综合能力强、插件多 | GenJi |
| **Gemini** | Google | 免费/付费 | 多模态、长上下文 | 技术爬爬虾 |
| **Grok** | xAI | 付费 | 实时信息、幽默感 | 技术爬爬虾 |
| **Kimi** | 月之暗面 | 免费 | 中文长文本 | 通用推荐 |
| **通义千问** | 阿里 | 免费 | 中文优化、多模态 | 小天fotos |

### 选择建议

| 使用场景 | 推荐工具 |
|----------|----------|
| 编程开发 | Claude (Claude Code) |
| 日常问答 | ChatGPT / Claude |
| 长文本处理 | Claude / Kimi |
| 免费使用 | Gemini / Kimi / 通义千问 |
| 中文场景 | Kimi / 通义千问 |

---

## 二、AI编程工具

### 工具对比

| 工具 | 定价 | 特点 | UP主关联 |
|------|------|------|----------|
| **Claude Code** | Claude Pro | 终端AI编程，Agent能力 | 小天fotos |
| **Cursor** | $20/月 | AI代码编辑器 | 通用推荐 |
| **GitHub Copilot** | $10/月 | 代码补全 | 通用推荐 |
| **OpenCode** | 免费 | 开源Claude Code替代 | 技术爬爬虾 |
| **Windsurf** | 免费/付费 | AI IDE | 通用推荐 |

### Claude Code 核心能力

```
功能矩阵：
├── 代码生成     → 根据需求生成代码
├── 代码审查     → 分析代码质量和安全
├── Bug修复      → 自动定位和修复问题
├── 重构         → 代码重构和优化
├── 测试生成     → 自动编写测试用例
├── 文档生成     → 自动生成代码文档
├── Skill系统    → 自定义专业能力
├── MCP集成      → 调用外部工具
└── Agent模式    → 自主执行复杂任务
```

---

## 三、AI绘画工具

### 工具对比

| 工具 | 定价 | 特点 | UP主关联 |
|------|------|------|----------|
| **Midjourney** | $10-30/月 | 画质顶级，Discord使用 | GenJi |
| **Stable Diffusion** | 免费 | 开源可控，需GPU | GenJi |
| **DALL-E 3** | ChatGPT Plus | 集成GPT，简单易用 | 通用 |
| **Ideogram** | 免费/付费 | 文字生成优秀 | 通用推荐 |

### 技术栈推荐

| 阶段 | 推荐工具 | 理由 |
|------|----------|------|
| 入门 | Midjourney | 效果好，上手快 |
| 进阶 | SD + ComfyUI | 免费且可控 |
| 专业 | SD + ControlNet + LoRA | 完全自定义 |

---

## 四、AI视频工具

### 工具对比

| 工具 | 定价 | 特点 | UP主关联 |
|------|------|------|----------|
| **Sora** | 付费 | OpenAI出品，效果好 | GenJi |
| **Runway** | 付费 | 专业视频生成 | GenJi |
| **Pika** | 免费/付费 | 简单易用 | 通用推荐 |
| **可灵AI** | 免费/付费 | 快手出品，效果好 | 通用推荐 |
| **HeyGen** | 付费 | AI数字人视频 | GenJi |
| **Remotion** | 开源 | 代码生成视频 | 小天fotos |

---

## 五、AI自动化工具

### MCP（Model Context Protocol）

| 维度 | 说明 |
|------|------|
| **定义** | AI与外部工具的标准化交互协议 |
| **开发者** | Anthropic |
| **核心功能** | 工具调用、资源访问、提示模板 |
| **适用场景** | 让AI调用你的工具和数据 |
| **UP主关联** | 小天fotos（协议讲解）、技术爬爬虾（15个MCP推荐） |

### Agent Skill

| 维度 | 说明 |
|------|------|
| **定义** | Claude Code的专业技能描述系统 |
| **核心功能** | 通过Markdown描述技能指令 |
| **适用场景** | 让AI具备专业领域能力 |
| **UP主关联** | 小天fotos（Skill开发教程）、技术爬爬虾（AGENT-SKILLS-EXAMPLES） |

### n8n

| 维度 | 说明 |
|------|------|
| **定义** | 开源工作流自动化平台 |
| **核心功能** | 可视化工作流、400+集成、内置AI节点 |
| **适用场景** | 零代码构建自动化系统 |
| **UP主关联** | 小in分享（n8n部署教程） |

---

## 六、AI辅助开发完整工具链

### 推荐配置（2026年）

```
AI编程：  Claude Code + MCP Server + Agent Skill
AI对话：  Claude + ChatGPT + Kimi（三选一）
AI绘画：  Midjourney（入门）/ SD+ComfyUI（进阶）
AI视频：  Sora / Runway / 可灵
自动化：  n8n + GitHub Actions + Docker
知识库：  Obsidian + Claude + 本地Markdown
```

### 工具获取链接

| 工具 | 链接 |
|------|------|
| Claude | https://claude.ai |
| ChatGPT | https://chat.openai.com |
| Claude Code | Anthropic CLI |
| Midjourney | https://midjourney.com |
| Stable Diffusion | https://github.com/AUTOMATIC1111/stable-diffusion-webui |
| ComfyUI | https://github.com/comfyanonymous/ComfyUI |
| n8n | https://n8n.io |
| Claude Desktop | https://claude.ai/download |

---

*本文档将随AI工具生态发展持续更新。*
