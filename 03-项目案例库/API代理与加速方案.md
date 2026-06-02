# API代理与加速方案

> 来源UP主：技术爬爬虾
> 创建时间：2026-04-28
> 难度：⭐⭐⭐

---

## 项目概述

API代理和加速是开发中常见的需求，尤其是访问国外AI服务（如OpenAI、Google Gemini、Claude）时。技术爬爬虾开源了多个API代理方案，覆盖从简单的URL代理到复杂的多API负载均衡。

### 你将学到
- Cloudflare Worker 部署和使用
- Deno Deploy API代理
- Nginx反向代理配置
- HTTPS免费证书申请

### 前置要求
- 基本的编程和命令行能力
- Cloudflare 账号（免费）
- 域名（可选，部分方案不需要）

---

## 一、Cloudflare Worker 代理

### 什么是 Cloudflare Worker
Cloudflare Worker 是 Cloudflare 提供的边缘计算服务，代码运行在全球各地的CDN节点上，免费额度为每天10万次请求。

### 项目：GEMINI-PLAYGROUND（⭐5k）

#### 功能
- 一键部署Google Gemini对话网站
- 国内通过Cloudflare代理访问Gemini API
- 支持流式响应

#### 部署步骤

1. **Fork仓库**
   ```
   https://github.com/tech-shrimp/gemini-playground
   ```

2. **获取Gemini API Key**
   - 访问 Google AI Studio
   - 创建API Key

3. **Vercel部署**
   - 登录 Vercel
   - Import Git Repository
   - 配置环境变量 `GEMINI_API_KEY`
   - Deploy

### 项目：DENO-API-PROXY（⭐448）

#### 功能
- 多API代理服务（支持Gemini、OpenAI、Grok等）
- 支持请求转发和响应处理
- Deno运行时，轻量高效

#### 部署步骤

1. **Fork仓库**
   ```
   https://github.com/tech-shrimp/deno-api-proxy
   ```

2. **Deno Deploy部署**
   - 登录 Deno Deploy
   - Import from GitHub
   - 配置环境变量
   - Deploy

### 自定义 Cloudflare Worker

```javascript
// worker.js - 简单的API代理
export default {
  async fetch(request) {
    const url = new URL(request.url);
    
    // 代理目标API
    const targetUrl = 'https://api.example.com' + url.pathname;
    
    // 转发请求
    const response = await fetch(targetUrl, {
      method: request.method,
      headers: request.headers,
      body: request.body,
    });
    
    return response;
  }
};
```

---

## 二、Grok3国内镜像

### 项目：GROK-PLAYGROUND（⭐528）

#### 功能
- Grok3对话界面的国内镜像
- 通过代理访问xAI API
- Next.js全栈开发

#### 部署步骤
1. Fork仓库
2. 获取xAI API Key
3. Vercel一键部署
4. 配置环境变量

---

## 三、Nginx反向代理

### 适用场景
- 自有服务器的API代理
- 需要更复杂的路由规则
- 需要缓存和负载均衡

### 基础配置

```nginx
server {
    listen 80;
    server_name proxy.example.com;
    
    # 代理到目标API
    location /api/ {
        proxy_pass https://api.target.com/;
        proxy_set_header Host api.target.com;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_ssl_server_name on;
    }
}
```

### HTTPS配置

```nginx
server {
    listen 443 ssl;
    server_name proxy.example.com;
    
    ssl_certificate /path/to/cert.pem;
    ssl_certificate_key /path/to/key.pem;
    
    location /api/ {
        proxy_pass https://api.target.com/;
        proxy_set_header Host api.target.com;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_ssl_server_name on;
    }
}
```

---

## 四、HTTPS免费证书

### Let's Encrypt + Certbot

#### 安装Certbot
```bash
# Ubuntu/Debian
sudo apt install certbot python3-certbot-nginx

# CentOS/RHEL
sudo yum install certbot python3-certbot-nginx
```

#### 获取证书
```bash
# Nginx
sudo certbot --nginx -d proxy.example.com

# 独立模式
sudo certbot certonly --standalone -d proxy.example.com
```

#### 自动续期
```bash
# 测试续期
sudo certbot renew --dry-run

# 添加定时任务
sudo crontab -e
# 添加: 0 3 * * * certbot renew --quiet
```

### Cloudflare SSL
- 在Cloudflare DNS中添加域名
- SSL/TLS设置为"Full"或"Flexible"
- 自动管理证书，无需手动续期

---

## 五、代理方案对比

| 方案 | 部署难度 | 费用 | 性能 | 适用场景 |
|------|----------|------|------|----------|
| Cloudflare Worker | ⭐⭐ | 免费 | 高 | 简单API代理 |
| Deno Deploy | ⭐⭐ | 免费 | 高 | JS/TS API服务 |
| Vercel | ⭐⭐ | 免费 | 中 | Next.js应用 |
| Nginx | ⭐⭐⭐ | 服务器费用 | 高 | 复杂代理需求 |
| Caddy | ⭐⭐ | 服务器费用 | 高 | 自动HTTPS |

---

## 六、合规与安全

### 重要提醒
- ⚠️ API代理的使用需遵守目标API的服务条款
- ⚠️ 不要用于非法目的或大规模数据抓取
- ⚠️ 注意数据安全和隐私保护
- ⚠️ API Key不要暴露在前端代码中

### 安全建议
- 使用环境变量存储API Key
- 配置访问频率限制
- 启用HTTPS加密传输
- 定期更新依赖和证书

---

## 七、参考资源

### 开源项目
- GEMINI-PLAYGROUND：https://github.com/tech-shrimp/gemini-playground
- GROK-PLAYGROUND：https://github.com/tech-shrimp/grok-playground
- DENO-API-PROXY：https://github.com/tech-shrimp/deno-api-proxy

### 文章
- 技术爬爬虾：Cloudflare中转Gemini API（CSDN 6624阅读）
- 技术爬爬虾：内网穿透工具合集（CSDN 6628阅读）
- 技术爬爬虾：HTTPS免费证书申请（CSDN 5963阅读）

### 官方文档
- Cloudflare Workers：https://developers.cloudflare.com/workers
- Deno Deploy：https://deno.com/deploy
- Let's Encrypt：https://letsencrypt.org

---

*本文档将随API代理技术的发展持续更新。*
