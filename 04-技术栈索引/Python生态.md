# Python 生态

> 综合四位UP主内容整理
> 创建时间：2026-04-28

---

## 一、Python基础

### 推荐学习资源

| 资源 | 来源 | 说明 |
|------|------|------|
| Claude Code + Python | 小天fotos | 用AI辅助学Python |
| 技术爬爬虾项目源码 | 技术爬爬虾 | 通过阅读实际项目学Python |
| 在线教程 | 多方 | Python官方教程、菜鸟教程等 |

### Python版本选择
- **推荐版本**：Python 3.11+（兼容性最好）
- **最新版本**：Python 3.14（用户当前环境）
- **注意**：部分旧库可能不兼容3.14，遇到问题降级到3.11

---

## 二、Web开发库

### 请求和抓取

| 库 | 用途 | UP主关联 |
|----|------|----------|
| **requests** | HTTP请求 | 巡检系统核心 |
| **httpx** | 异步HTTP | 技术爬爬虾项目 |
| **BeautifulSoup4** | HTML解析 | 巡检系统核心 |
| **lxml** | 高性能XML/HTML解析 | 性能优化 |
| **Playwright** | 浏览器自动化 | 巡检系统（可选） |

### Web框架

| 框架 | 用途 | UP主关联 |
|------|------|----------|
| **Flask** | 轻量Web框架 | 技术爬爬虾项目 |
| **FastAPI** | 现代API框架 | 技术爬爬虾MCP开发 |
| **Next.js** | 全栈框架（JS） | 技术爬爬虾Gemini项目 |

---

## 三、数据处理

### 核心库

| 库 | 用途 | UP主关联 |
|----|------|----------|
| **json** | JSON数据处理 | 巡检系统数据存储 |
| **csv** | CSV文件读写 | 数据导入导出 |
| **pandas** | 数据分析 | 数据分析项目 |
| **re** | 正则表达式 | 文本提取和匹配 |
| **datetime** | 日期时间处理 | 巡检系统时间处理 |

### 数据可视化

| 库 | 用途 | UP主关联 |
|----|------|----------|
| **matplotlib** | 基础图表 | 数据可视化 |
| **plotly** | 交互式图表 | HTML报告嵌入 |
| **jinja2** | 模板引擎 | HTML报告生成 |

---

## 四、自动化与工具

### 系统自动化

| 库 | 用途 | UP主关联 |
|----|------|----------|
| **subprocess** | 调用系统命令 | 脚本编排 |
| **schedule** | 定时任务 | 本地定时巡检 |
| **pathlib** | 路径操作 | 文件管理 |
| **shutil** | 文件操作 | 文件复制移动 |

### 微信开发

| 库 | 用途 | UP主关联 |
|----|------|----------|
| **requests** | API调用 | FREEWECHATPUSH |
| **qrcode** | 二维码生成 | 微信相关 |

---

## 五、AI/ML相关

### 大模型API

| 库 | 用途 | UP主关联 |
|----|------|----------|
| **openai** | OpenAI API | AI项目开发 |
| **anthropic** | Claude API | 小天fotos方向 |
| **google-generativeai** | Gemini API | 技术爬爬虾项目 |

### AI辅助开发

| 工具 | 用途 | UP主关联 |
|------|------|----------|
| **Claude Code** | AI编程助手 | 小天fotos |
| **Cursor** | AI代码编辑器 | 通用推荐 |
| **GitHub Copilot** | AI代码补全 | 通用推荐 |

---

## 六、项目依赖管理

### pip常用命令

```bash
# 安装包
pip install package_name

# 安装指定版本
pip install package_name==1.0.0

# 从requirements.txt安装
pip install -r requirements.txt

# 导出依赖
pip freeze > requirements.txt

# 创建虚拟环境
python -m venv myenv
```

### requirements.txt 示例（巡检系统）

```
requests>=2.28.0
beautifulsoup4>=4.12.0
lxml>=4.9.0
jinja2>=3.1.0
```

---

## 七、Python项目结构推荐

### 小型脚本
```
my_script.py
requirements.txt
```

### 中型项目
```
my_project/
├── main.py
├── config.py
├── utils.py
├── requirements.txt
└── data/
```

### 大型项目
```
my_project/
├── src/
│   ├── __init__.py
│   ├── core/
│   ├── utils/
│   └── models/
├── tests/
├── requirements.txt
├── setup.py
└── README.md
```

---

*本文档将随Python生态发展持续更新。*
