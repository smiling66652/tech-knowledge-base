# MCP Server 开发

> 来源UP主：小天fotos + 技术爬爬虾
> 创建时间：2026-04-28
> 难度：⭐⭐⭐⭐

---

## 项目概述

MCP（Model Context Protocol）是 Anthropic 推出的标准化协议，用于AI助手与外部工具/数据的交互。技术爬爬虾推荐了15个实用MCP，小天fotos深入讲解了MCP协议原理。本案例库提供MCP Server开发的完整指南。

### 你将学到
- MCP协议的核心概念和设计理念
- 如何使用TypeScript开发MCP Server
- 如何使用Python开发MCP Server
- Claude Desktop中的MCP配置方法
- 实用MCP推荐和选择指南

### 前置要求
- TypeScript或Python基础
- Node.js 18+（TypeScript方案）
- Claude Desktop已安装
- 基本的API开发能力

---

## 一、MCP协议核心概念

### 什么是MCP
MCP（Model Context Protocol）是一个开放协议，定义了AI应用与外部数据源/工具之间的标准化交互方式。

### 架构设计

```
┌─────────────────┐     MCP协议      ┌─────────────────┐
│   AI 应用       │ ←──────────────→ │   MCP Server    │
│ (Claude Desktop) │                  │  (你的工具服务)  │
└─────────────────┘                   └─────────────────┘
                                            │
                                     ┌──────┴──────┐
                                     │  外部资源    │
                                     │  API/数据库  │
                                     │  文件系统    │
                                     └─────────────┘
```

### 核心组件

| 组件 | 说明 |
|------|------|
| **Host** | AI应用（如Claude Desktop） |
| **Client** | Host内的MCP客户端 |
| **Server** | 外部工具服务（你开发的） |
| **Transport** | 通信方式（stdio/SSE） |
| **Tools** | Server暴露的工具（函数） |
| **Resources** | Server暴露的数据资源 |

---

## 二、15个实用MCP推荐

> 来源：技术爬爬虾CSDN文章「用过上百款编程MCP，只有这15个真正好用」（6096阅读）

### 开发工具类

| MCP Server | 功能 | 推荐指数 |
|-----------|------|----------|
| **filesystem** | 文件系统读写操作 | ★★★★★ |
| **github** | GitHub API操作 | ★★★★★ |
| **git** | Git命令操作 | ★★★★★ |
| **sequential-thinking** | 结构化思考流程 | ★★★★☆ |

### 搜索和知识类

| MCP Server | 功能 | 推荐指数 |
|-----------|------|----------|
| **brave-search** | 网页搜索 | ★★★★★ |
| **fetch** | 网页内容抓取 | ★★★★★ |
| **memory** | 持久化记忆管理 | ★★★★☆ |

### 数据和API类

| MCP Server | 功能 | 推荐指数 |
|-----------|------|----------|
| **sqlite** | SQLite数据库操作 | ★★★★★ |
| **postgres** | PostgreSQL数据库操作 | ★★★★☆ |
| **puppeteer** | 浏览器自动化 | ★★★★☆ |

### 效率和通讯类

| MCP Server | 功能 | 推荐指数 |
|-----------|------|----------|
| **slack** | Slack消息操作 | ★★★★☆ |
| **google-maps** | 地图和位置服务 | ★★★☆☆ |
| **everything** | Windows文件极速搜索 | ★★★★☆ |

### 选择建议

| 使用场景 | 推荐MCP |
|----------|---------|
| 日常开发 | filesystem + git + github |
| 信息搜索 | brave-search + fetch |
| 数据分析 | sqlite + sequential-thinking |
| 自动化 | puppeteer + slack |

---

## 三、TypeScript开发MCP Server

### Step 1：初始化项目

```bash
mkdir my-mcp-server
cd my-mcp-server
npm init -y
npm install @modelcontextprotocol/sdk typescript @types/node
npm install -D typescript tsx
npx tsc --init
```

### Step 2：编写Server

```typescript
// src/index.ts
import { Server } from "@modelcontextprotocol/sdk/server/index.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";

const server = new Server(
  { name: "my-mcp-server", version: "1.0.0" },
  { capabilities: { tools: {} } }
);

// 注册工具
server.setRequestHandler(
  { method: "tools/list" },
  async () => ({
    tools: [
      {
        name: "hello_world",
        description: "简单的问候工具",
        inputSchema: {
          type: "object",
          properties: {
            name: {
              type: "string",
              description: "要问候的名字",
            },
          },
          required: ["name"],
        },
      },
      {
        name: "get_current_time",
        description: "获取当前时间",
        inputSchema: {
          type: "object",
          properties: {},
        },
      },
    ],
  })
);

// 处理工具调用
server.setRequestHandler(
  { method: "tools/call" },
  async (request) => {
    const { name, arguments: args } = request.params;

    if (name === "hello_world") {
      return {
        content: [
          {
            type: "text",
            text: `你好，${args.name}！这是来自MCP Server的问候。`,
          },
        ],
      };
    }

    if (name === "get_current_time") {
      return {
        content: [
          {
            type: "text",
            text: `当前时间：${new Date().toLocaleString("zh-CN")}`,
          },
        ],
      };
    }

    throw new Error(`未知工具: ${name}`);
  }
);

// 启动Server
async function main() {
  const transport = new StdioServerTransport();
  await server.connect(transport);
  console.error("MCP Server 已启动");
}

main().catch(console.error);
```

### Step 3：构建和配置

```json
// package.json
{
  "name": "my-mcp-server",
  "version": "1.0.0",
  "main": "dist/index.js",
  "scripts": {
    "build": "tsc",
    "start": "node dist/index.js",
    "dev": "tsx src/index.ts"
  }
}
```

```json
// Claude Desktop配置文件
// Windows: %APPDATA%\Claude\claude_desktop_config.json
// macOS: ~/Library/Application Support/Claude/claude_desktop_config.json
{
  "mcpServers": {
    "my-server": {
      "command": "node",
      "args": ["C:\\path\\to\\my-mcp-server\\dist\\index.js"]
    }
  }
}
```

---

## 四、Python开发MCP Server

### Step 1：安装依赖

```bash
pip install mcp
```

### Step 2：编写Server

```python
# server.py
from mcp.server import Server
from mcp.server.stdio import stdio_server
import datetime

server = Server("my-python-mcp")

@server.list_tools()
async def list_tools():
    return [
        {
            "name": "calculate",
            "description": "数学计算器",
            "inputSchema": {
                "type": "object",
                "properties": {
                    "expression": {
                        "type": "string",
                        "description": "数学表达式，如 '2+3*4'"
                    }
                },
                "required": ["expression"]
            }
        },
        {
            "name": "get_weather_info",
            "description": "获取天气信息（模拟）",
            "inputSchema": {
                "type": "object",
                "properties": {
                    "city": {
                        "type": "string",
                        "description": "城市名称"
                    }
                },
                "required": ["city"]
            }
        }
    ]

@server.call_tool()
async def call_tool(name, arguments):
    if name == "calculate":
        try:
            result = eval(arguments["expression"])
            return [{"type": "text", "text": f"计算结果: {result}"}]
        except Exception as e:
            return [{"type": "text", "text": f"计算错误: {str(e)}"}]
    
    if name == "get_weather_info":
        city = arguments["city"]
        return [{
            "type": "text",
            "text": f"{city}今日天气: 晴, 25°C, 湿度60%"
        }]
    
    raise ValueError(f"未知工具: {name}")

async def main():
    async with stdio_server() as (read_stream, write_stream):
        await server.run(read_stream, write_stream)

if __name__ == "__main__":
    import asyncio
    asyncio.run(main())
```

### Step 3：配置Claude Desktop

```json
{
  "mcpServers": {
    "my-python-server": {
      "command": "python",
      "args": ["C:\\path\\to\\server.py"]
    }
  }
}
```

---

## 五、实用MCP Server开发案例

### 案例1：网页内容抓取MCP

```typescript
// 功能：抓取指定URL的网页内容
server.setRequestHandler(
  { method: "tools/call" },
  async (request) => {
    if (request.params.name === "fetch_webpage") {
      const url = request.params.arguments.url;
      const response = await fetch(url);
      const html = await response.text();
      // 提取纯文本内容
      const text = html.replace(/<[^>]*>/g, " ").trim();
      return {
        content: [{ type: "text", text: text.substring(0, 5000) }]
      };
    }
  }
);
```

### 案例2：文件搜索MCP

```typescript
// 功能：搜索本地文件系统
import { exec } from "child_process";

// Windows: 使用 where 或 dir
// Linux/Mac: 使用 find 或 locate
```

### 案例3：数据库查询MCP

```typescript
// 功能：查询SQLite数据库
import Database from "better-sqlite3";

const db = new Database("mydata.db");

// 注册工具：执行SQL查询
// 安全考虑：限制为SELECT语句
```

---

## 六、调试和测试

### 本地测试

```bash
# 使用MCP Inspector调试
npx @modelcontextprotocol/inspector node dist/index.js
```

### 常见问题

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| Claude Desktop看不到MCP | 配置文件路径错误 | 检查JSON配置 |
| 工具调用失败 | inputSchema格式错误 | 检查JSON Schema |
| 启动报错 | 依赖未安装 | npm install / pip install |
| 中文乱码 | 编码问题 | 设置UTF-8编码 |

---

## 七、与巡检系统的结合

### 可开发的巡检相关MCP Server

| MCP名称 | 功能 | 工具列表 |
|---------|------|----------|
| **hfut-inspector** | 合工大官网巡检 | run_inspection, get_results, get_summary |
| **notification** | 消息推送 | send_wechat, send_email |
| **report-gen** | 报告生成 | generate_html, generate_markdown |
| **config** | 配置管理 | get_config, update_config, add_url |

### 示例：巡检MCP

```typescript
@server.list_tools()
async () => ({
  tools: [
    {
      name: "run_inspection",
      description: "执行合工大官网巡检，返回新增通知列表",
      inputSchema: {
        type: "object",
        properties: {
          mode: { type: "string", enum: ["incremental", "full"] }
        }
      }
    },
    {
      name: "get_inspection_summary",
      description: "获取最近一次巡检的摘要报告",
      inputSchema: { type: "object", properties: {} }
    }
  ]
});
```

---

## 八、参考资源

### 官方资源
- MCP协议规范：https://modelcontextprotocol.io
- MCP TypeScript SDK：https://github.com/modelcontextprotocol/typescript-sdk
- MCP Python SDK：https://github.com/modelcontextprotocol/python-sdk

### 文章和视频
- 技术爬爬虾「从零开始编写MCP Server」（CSDN 2939阅读）
- 技术爬爬虾「15个好用MCP推荐」（CSDN 6096阅读）
- 小天fotos「MCP协议深度解析」

### 开源示例
- 官方MCP Server示例仓库
- AGENT-SKILLS-EXAMPLES：https://github.com/tech-shrimp/agent-skills-examples

---

*本文档将随MCP协议的更新持续迭代。*
