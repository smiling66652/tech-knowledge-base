# Docker国内部署方案

> 来源UP主：技术爬爬虾 + 小in分享
> 创建时间：2026-04-28
> 难度：⭐⭐

---

## 项目概述

Docker是国内开发者最常用的容器化工具，但由于网络原因，在国内安装和使用Docker面临诸多挑战。本项目整合技术爬爬虾和小in分享的方案，提供完整的国内Docker部署指南。

### 你将学到
- Docker国内一键安装方法
- Docker镜像加速和转存
- Docker Compose基本使用
- 常用服务的Docker化部署

### 前置要求
- Windows 10/11（或Linux）
- 基本的命令行操作能力

---

## 一、国内安装 Docker

### Windows 方案

#### 方案A：Docker Desktop（推荐新手）

1. **下载安装**
   - 官网下载：https://docker.com/products/docker-desktop
   - 国内镜像：可从技术爬爬虾的DOCKER_INSTALLER项目获取

2. **配置国内镜像源**
   ```json
   // Docker Desktop → Settings → Docker Engine
   {
     "registry-mirrors": [
       "https://docker.mirrors.ustc.edu.cn",
       "https://hub-mirror.c.163.com"
     ]
   }
   ```

3. **启用WSL2后端**
   - Docker Desktop → Settings → General
   - 勾选 "Use the WSL 2 based engine"

#### 方案B：DOCKER_INSTALLER 脚本（技术爬爬虾）

- **项目地址**：https://github.com/tech-shrimp/docker_installer
- **Stars**：3.2k
- **功能**：国内一键安装Docker，自动配置镜像加速

### Linux 方案

```bash
# 一键安装脚本（Ubuntu/Debian）
curl -fsSL https://get.docker.com | sh

# 配置镜像加速
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<'EOF'
{
  "registry-mirrors": [
    "https://docker.mirrors.ustc.edu.cn",
    "https://hub-mirror.c.163.com"
  ]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

---

## 二、Docker镜像转存

### DOCKER_IMAGE_PUSHER（⭐15.9k）

这是技术爬爬虾最热门的开源项目，用于将Docker Hub上的镜像自动转存到阿里云。

#### 功能
- 自动将指定Docker Hub镜像转存到阿里云容器镜像服务
- 使用GitHub Actions定时执行
- 支持批量转存
- 转存后可从阿里云直接拉取

#### 使用步骤

1. **Fork仓库**
   ```
   https://github.com/tech-shrimp/docker_image_pusher
   ```

2. **配置阿里云**
   - 注册阿里云账号
   - 开通容器镜像服务
   - 创建命名空间
   - 获取仓库密码

3. **配置GitHub Secrets**
   ```
   ALIYUN_REGISTRY_USER=你的阿里云用户名
   ALIYUN_REGISTRY_PASSWORD=你的阿里云密码
   ALIYUN_NAMESPACE=你的命名空间
   ```

4. **配置需要转存的镜像**
   编辑仓库中的配置文件，添加需要转存的镜像列表

5. **运行GitHub Actions**
   手动触发或等待定时任务执行

#### 常用镜像转存列表
```yaml
images:
  - nginx:latest
  - redis:latest
  - mysql:8.0
  - postgres:15
  - node:18-alpine
  - python:3.11-slim
  - n8n:latest
  - ollama/ollama:latest
```

---

## 三、Docker Compose 基础

### 什么是 Docker Compose
Docker Compose 用于定义和运行多容器应用，通过一个 `docker-compose.yml` 文件管理所有服务。

### 基本使用

#### 编写 docker-compose.yml
```yaml
version: '3.8'
services:
  web:
    image: nginx:latest
    ports:
      - "80:80"
    volumes:
      - ./html:/usr/share/nginx/html
  
  db:
    image: mysql:8.0
    environment:
      MYSQL_ROOT_PASSWORD: password123
    volumes:
      - db_data:/var/lib/mysql

volumes:
  db_data:
```

#### 常用命令
```bash
# 启动所有服务
docker-compose up -d

# 查看服务状态
docker-compose ps

# 查看日志
docker-compose logs -f

# 停止所有服务
docker-compose down

# 重建并启动
docker-compose up -d --build
```

---

## 四、常用服务Docker化部署

### n8n 自动化平台

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
    restart: unless-stopped

volumes:
  n8n_data:
```

### Ollama 本地AI

```yaml
version: '3.8'
services:
  ollama:
    image: ollama/ollama:latest
    ports:
      - "11434:11434"
    volumes:
      - ollama_data:/root/.ollama
    deploy:
      resources:
        reservations:
          devices:
            - driver: nvidia
              count: all
              capabilities: [gpu]

volumes:
  ollama_data:
```

### MySQL 数据库

```yaml
version: '3.8'
services:
  mysql:
    image: mysql:8.0
    ports:
      - "3306:3306"
    environment:
      MYSQL_ROOT_PASSWORD: password123
      MYSQL_DATABASE: myapp
    volumes:
      - mysql_data:/var/lib/mysql
    restart: unless-stopped

volumes:
  mysql_data:
```

### Redis 缓存

```yaml
version: '3.8'
services:
  redis:
    image: redis:latest
    ports:
      - "6379:6379"
    volumes:
      - redis_data:/data
    restart: unless-stopped

volumes:
  redis_data:
```

---

## 五、与巡检系统的结合

### 将巡检系统Docker化

```yaml
version: '3.8'
services:
  inspector:
    build: .
    environment:
      - PYTHONUNBUFFERED=1
    volumes:
      - ./config:/app/config
      - ./output:/app/output
    restart: unless-stopped
  
  scheduler:
    image: nginx:latest
    volumes:
      - ./output:/usr/share/nginx/html
    ports:
      - "8080:80"
    restart: unless-stopped
```

### 优势
- 一键部署到任何支持Docker的环境
- 环境隔离，不污染宿主机
- 方便迁移和扩展
- 可以配合GitHub Actions实现CI/CD

---

## 六、常见问题排查

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| 镜像拉取超时 | 网络问题 | 配置镜像加速/使用转存 |
| 容器启动失败 | 端口冲突 | 修改端口映射 |
| 权限不足 | Linux文件权限 | 使用正确的用户权限 |
| 内存不足 | 容器过多 | 限制容器内存 |
| WSL2启动失败 | Windows版本 | 升级到Win10 1903+ |

---

## 七、参考资源

### 开源项目
- DOCKER_IMAGE_PUSHER：https://github.com/tech-shrimp/docker_image_pusher
- DOCKER_INSTALLER：https://github.com/tech-shrimp/docker_installer

### 视频教程
- 小in分享「WSL2/Docker Desktop入门」
- 技术爬爬虾 Docker相关视频

### 官方文档
- Docker官方文档：https://docs.docker.com
- Docker Compose文档：https://docs.docker.com/compose
- 阿里云容器镜像服务：https://cr.console.aliyun.com

---

*本文档将随Docker版本更新持续迭代。*
