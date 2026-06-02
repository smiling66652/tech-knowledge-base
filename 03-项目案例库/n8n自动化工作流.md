# n8n 自动化工作流

> 来源UP主：小in分享
> 创建时间：2026-04-28
> 难度：⭐⭐

---

## 项目概述

n8n是一个开源的工作流自动化工具，通过可视化界面连接各种应用和服务，实现自动化任务。小in分享有详细的n8n本地AI部署教程，适合零基础用户学习。

### 你将学到
- n8n的安装和配置
- 可视化工作流搭建
- AI模型的本地集成
- 实际自动化场景实现

### 前置要求
- Docker已安装（参考Docker国内部署方案）
- 基本的电脑操作能力
- 不需要编程基础

---

## 一、n8n简介

### 什么是n8n
n8n（ pronounced "nodemation"）是一个开源的工作流自动化工具，类似Zapier但可自托管。

### 核心优势
- **免费开源**：可自托管，无使用限制
- **可视化**：拖拽式界面，无需编程
- **丰富集成**：400+内置应用连接器
- **AI支持**：内置AI节点，支持OpenAI/Gemini/Ollama
- **灵活扩展**：支持自定义节点和HTTP请求

### 与Zapier/Make对比

| 维度 | n8n | Zapier | Make |
|------|-----|--------|-----|
| **费用** | 免费（自托管） | $19.99/月起 | $9/月起 |
| **节点数限制** | 无限 | 按套餐 | 按套餐 |
| **自托管** | 支持 | 不支持 | 不支持 |
| **AI支持** | 内置 | 有限 | 有限 |
| **数据隐私** | 完全可控 | 数据在云端 | 数据在云端 |

---

## 二、安装部署

### Docker部署（推荐）

```yaml
version: '3.8'
services:
  n8n:
    image: n8nio/n8n:latest
    container_name: n8n
    ports:
      - "5678:5678"
    environment:
      - N8N_BASIC_AUTH_ACTIVE=true
      - N8N_BASIC_AUTH_USER=admin
      - N8N_BASIC_AUTH_PASSWORD=yourpassword
      - GENERIC_TIMEZONE=Asia/Shanghai
    volumes:
      - n8n_data:/home/node/.n8n
    restart: unless-stopped

volumes:
  n8n_data:
```

```bash
# 启动
docker-compose up -d

# 访问
# http://localhost:5678
```

### 与Ollama集成（本地AI）

```yaml
version: '3.8'
services:
  n8n:
    image: n8nio/n8n:latest
    ports:
      - "5678:5678"
    environment:
      - N8N_BASIC_AUTH_ACTIVE=true
      - N8N_BASIC_AUTH_USER=admin
      - N8N_BASIC_AUTH_PASSWORD=yourpassword
    volumes:
      - n8n_data:/home/node/.n8n
    depends_on:
      - ollama
    restart: unless-stopped

  ollama:
    image: ollama/ollama:latest
    ports:
      - "11434:11434"
    volumes:
      - ollama_data:/root/.ollama
    restart: unless-stopped

volumes:
  n8n_data:
  ollama_data:
```

```bash
# 拉取AI模型
docker exec -it ollama ollama pull qwen:7b
```

---

## 三、核心概念

### 节点（Node）
工作流中的每个步骤就是一个节点，每个节点完成一个操作。

### 触发器（Trigger）
工作流的启动方式：
- **Webhook**：HTTP请求触发
- **Cron**：定时触发
- **Manual**：手动触发
- **Event**：事件触发

### 连线（Connection）
节点之间的数据流，前一个节点的输出是后一个节点的输入。

---

## 四、实用工作流案例

### 案例1：RSS新闻聚合 + AI摘要 + 微信推送

```
[定时触发(Cron)]
    ↓
[RSS Feed] → 获取新闻列表
    ↓
[AI Agent] → 生成每条新闻的摘要
    ↓
[HTTP Request] → 企业微信API推送
```

#### 配置步骤
1. 添加 **Cron** 节点，设置每天早上8点触发
2. 添加 **RSS Feed** 节点，输入RSS源URL
3. 添加 **AI Agent** 节点，设置摘要任务prompt
4. 添加 **HTTP Request** 节点，配置企业微信Webhook

### 案例2：邮件自动化处理

```
[邮件触发(IMAP)]
    ↓
[IF条件] → 判断邮件类型
    ├── 重要 → [AI分析] → [保存到数据库]
    ├── 通知 → [AI摘要] → [微信推送]
    └── 垃圾 → [标记删除]
```

### 案例3：数据采集 + AI分析 + 报告生成

```
[定时触发]
    ↓
[HTTP Request] → 采集网页数据
    ↓
[HTML提取] → 解析关键信息
    ↓
[AI Agent] → 分析数据趋势
    ↓
[文档生成] → 创建Markdown报告
    ↓
[邮件/微信] → 发送报告
```

### 案例4：AI聊天机器人

```
[Webhook触发]
    ↓
[AI Agent] → 调用Ollama本地模型
    ↓
[HTTP Response] → 返回AI回复
```

### 案例5：社交媒体自动化

```
[定时触发]
    ↓
[RSS/数据源] → 获取内容
    ↓
[AI Agent] → 改写/翻译/配图
    ↓
[社交媒体API] → 自动发布
```

---

## 五、AI节点详解

### 内置AI节点

| 节点 | 功能 |
|------|------|
| AI Agent | 构建AI代理，支持工具调用 |
| AI Chain | 简单的AI处理链 |
| AI Text Classifier | 文本分类 |
| AI Text Transformer | 文本转换 |
| OpenAI Model | 调用OpenAI模型 |
| Ollama Chat Model | 调用本地Ollama模型 |
| Google Gemini | 调用Gemini模型 |

### 配置Ollama本地AI

1. 确保Ollama容器正在运行
2. 在n8n中添加凭证：
   - 类型：Ollama API
   - Base URL：http://ollama:11434
3. 在AI Agent节点中选择Ollama模型

---

## 六、高级技巧

### 错误处理
- 在节点之间添加 **Error Trigger**
- 配置 **Retry on Fail**
- 设置 **Error Workflow**

### 数据存储
- 使用内置的 **Postgres** 存储（n8n自带）
- 或连接外部数据库（MySQL/Postgres/MongoDB）

### 性能优化
- 使用 **Batch** 节点批量处理
- 设置合理的超时时间
- 大数据处理用 **Split** 拆分

### 工作流调试
- 点击节点可以查看输入/输出
- 使用 **Execute Node** 单步执行
- 查看执行历史和日志

---

## 七、与巡检系统的结合

### 用n8n编排巡检工作流

```
[定时触发 - 每天8:00]
    ↓
[HTTP Request] → 调用巡检脚本API
    ↓
[HTML解析] → 提取巡检结果
    ↓
[AI Agent] → 生成巡检摘要和分析
    ↓
[IF条件] → 是否有重要通知
    ├── 是 → [微信推送] → [邮件通知]
    └── 否 → [仅存档]
    ↓
[文档生成] → 更新巡检报告
    ↓
[文件写入] → 保存HTML报告
```

### 优势
- **可视化**：整个巡检流程一目了然
- **灵活**：随时调整步骤和条件
- **可靠**：内置错误处理和重试
- **扩展**：轻松添加新的处理步骤

---

## 八、参考资源

### 视频教程
- 小in分享「n8n本地AI部署教程」（2026年1月）

### 官方资源
- n8n官网：https://n8n.io
- n8n文档：https://docs.n8n.io
- n8n模板库：https://n8n.io/workflows
- n8n社区：https://community.n8n.io

### 配套项目
- Docker部署方案：参考「Docker国内部署方案」文档
- 微信推送集成：参考「微信工具开发」文档

---

*本文档将随n8n版本更新持续迭代。*
