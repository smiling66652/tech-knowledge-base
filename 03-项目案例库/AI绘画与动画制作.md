# AI绘画与动画制作

> 来源UP主：GenJi是真想教会你
> 创建时间：2026-04-28
> 难度：⭐⭐⭐

---

## 项目概述

AI绘画和动画制作是当前最热门的AI应用领域之一。本项目基于GenJi的教程体系，系统学习从AI绘画到AI动画的完整创作流程。

### 你将学到
- Midjourney 和 Stable Diffusion 的使用方法
- ComfyUI 工作流搭建
- AI动画制作全流程
- AI创作技巧和创意方法

### 前置要求
- 无编程基础要求
- 需要GPU（SD本地部署，至少8GB显存）
- Midjourney需要付费订阅（$10-30/月）

---

## 一、AI绘画工具选择

### 工具对比

| 维度 | Midjourney | Stable Diffusion | DALL-E 3 |
|------|-----------|-----------------|----------|
| **画质** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ |
| **易用性** | ⭐⭐⭐⭐ | ⭐⭐ | ⭐⭐⭐⭐⭐ |
| **自由度** | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐ |
| **费用** | $10-30/月 | 免费（需硬件） | ChatGPT Plus |
| **平台** | Discord | 本地部署 | ChatGPT |
| **适合人群** | 快速出图 | 深度控制 | 简单使用 |

### 推荐选择
- **零基础/快速上手**：Midjourney
- **深度控制/免费**：Stable Diffusion
- **ChatGPT用户**：DALL-E 3

---

## 二、Midjourney 入门

### Step 1：加入和使用
1. 加入 Midjourney Discord 服务器
2. 订阅计划（Basic $10/月 起步）
3. 在频道中使用 `/imagine` 命令

### Step 2：Prompt 编写基础
```
/imagine prompt: [主体描述], [风格], [细节], [参数]
```

### Step 3：常用参数
| 参数 | 说明 | 示例 |
|------|------|------|
| --ar | 宽高比 | --ar 16:9 |
| --v | 版本 | --v 6 |
| --s | 风格化程度 | --s 250 |
| --q | 品质 | --q 2 |

### Step 4：进阶技巧
- 使用 `--sref` 参考图像风格
- 使用 `--cref` 参考角色一致性
- 多轮迭代优化prompt
- 用 `blend` 混合多张图

---

## 三、Stable Diffusion 入门

### Step 1：安装部署

#### 方案A：本地部署（推荐）
1. 安装 Python 3.10+
2. 安装 PyTorch（CUDA版本）
3. 克隆 Stable Diffusion WebUI
4. 下载模型文件
5. 运行 `webui-user.bat`

#### 方案B：云部署
- Google Colab（免费GPU）
- 阿里云/腾讯云 GPU实例

### Step 2：WebUI 基础操作

| 功能 | 说明 |
|------|------|
| txt2img | 文字生成图像 |
| img2img | 图像生成图像 |
| Inpainting | 局部重绘 |
| Extras | 图像放大/处理 |

### Step 3：模型和插件

#### 推荐模型
| 模型 | 特点 | 适用场景 |
|------|------|----------|
| SDXL Base | 官方基础模型 | 通用 |
| Realistic Vision | 写实风格 | 人物、风景 |
| DreamShaper | 多用途 | 插画、概念设计 |
| Anything V5 | 二次元 | 动漫风格 |

#### 推荐插件
| 插件 | 功能 |
|------|------|
| ControlNet | 精确控制姿势/构图 |
| LoRA | 风格/角色微调 |
| ADetailer | 面部/手部修复 |
| OpenPose | 姿势控制 |

### Step 4：Prompt 编写
```
正向提示词：[主体], [质量词], [风格], [细节], [光影]
负面提示词：[不想要的元素]

示例：
正向：masterpiece, best quality, 1girl, blue eyes, white dress, 
      garden background, soft lighting, detailed
负面：low quality, worst quality, blurry, deformed, ugly
```

---

## 四、ComfyUI 工作流

### 什么是 ComfyUI
ComfyUI 是一个基于节点的Stable Diffusion工作流编辑器，通过连接不同节点实现复杂的图像生成流程。

### 基础工作流搭建
```
加载模型 → CLIP编码 → KSampler → VAE解码 → 保存图像
```

### 进阶工作流
```
加载图像 → ControlNet → KSampler → ADetailer → 保存
```

### 学习资源
- GenJi「AI动画制作课程」
- ComfyUI 官方文档
- ComfyUI 工作流模板社区

---

## 五、AI动画制作

### 工具链

| 工具 | 用途 | 难度 |
|------|------|------|
| ComfyUI | 图生视频工作流 | ⭐⭐⭐ |
| Runway | AI视频生成 | ⭐⭐ |
| Pika | AI视频生成 | ⭐⭐ |
| Sora | AI视频生成（OpenAI） | ⭐⭐ |
| HeyGen | AI数字人视频 | ⭐ |

### 基本流程

```
1. 生成关键帧图像（Midjourney/SD）
2. 图生视频（ComfyUI/Runway）
3. AI配音（声音克隆）
4. AI字幕（自动生成）
5. 后期合成
```

### GenJi 的AI动画方法论
- 从静态图像到动态视频的过渡
- 保持角色一致性的技巧
- 控制视频节奏和镜头运动
- AI动画的商用场景

---

## 六、AI绘画实战项目

### 项目1：AI头像生成
- **步骤**：设计prompt → 生成多版本 → 选择最佳 → 后期微调
- **时间**：30分钟
- **工具**：Midjourney

### 项目2：AI产品图
- **步骤**：拍摄产品照片 → img2img重绘背景 → 添加效果
- **时间**：1小时
- **工具**：Stable Diffusion + ControlNet

### 项目3：AI插画集
- **步骤**：确定主题 → 设计系列prompt → 批量生成 → 筛选排版
- **时间**：1-2天
- **工具**：Stable Diffusion

### 项目4：AI动画短片
- **步骤**：编写剧本 → 生成关键帧 → 图生视频 → 配音字幕 → 合成
- **时间**：3-5天
- **工具**：ComfyUI + HeyGen

---

## 七、避坑指南

### 常见问题

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| 手指/眼睛变形 | 模型局限 | 使用ADetailer插件 |
| 人物不一致 | 随机性太高 | 使用LoRA/IP-Adapter |
| 生成速度慢 | 硬件不足 | 降低分辨率/使用云GPU |
| 风格不统一 | prompt差异大 | 建立prompt模板库 |
| 侵权风险 | 使用他人作品训练 | 使用合规模型和数据 |

### 注意事项
- AI生成的内容可能涉及版权问题，商用需谨慎
- 不同工具的使用条款不同，注意合规
- AI绘画是辅助工具，不是完全替代人工创作
- 持续关注AI绘画领域的新发展和新工具

---

## 八、参考资源

### 视频教程
- GenJi「AI动画制作课程」（3.7万赞）
- GenJi「SD花活集」（1.2万赞）
- GenJi「速通Sora」（2.8万赞）

### 工具网站
- Midjourney: https://midjourney.com
- Stable Diffusion WebUI: https://github.com/AUTOMATIC1111/stable-diffusion-webui
- ComfyUI: https://github.com/comfyanonymous/ComfyUI
- Civitai（模型社区）: https://civitai.com

### Prompt 资源
- PromptHero: https://prompthero.com
- Lexica: https://lexica.art

---

*本文档将随AI绘画工具的更新持续迭代。*
