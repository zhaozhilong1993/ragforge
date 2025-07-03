<div align="center">
<a href="https://demo.ragforge.io/">
<img src="conf/logo-with-text.png" width="100" alt="RAGForge logo">
</a>
</div>

<p align="center">
  <a href="./README_en.md">English</a> |
  <a href="./README.md">简体中文</a>
</p>

## 💡 RAGForge 是什么？

RAGForge 是基于 RAGForge 进行功能增强的开源 RAG（Retrieval-Augmented Generation）引擎。在保持原有 RAGForge 核心功能的基础上，新增了多项企业级功能增强，为开发人员提供更强大的 RAG 解决方案。

## 🌟 核心功能

### 🔍 **深度文档理解**
- 基于深度文档理解，从复杂格式的非结构化数据中提取知识
- 支持 Word、PPT、Excel、PDF、图片、网页等多种格式

### 🧠 **智能文本处理**
- 基于模板的智能文本切片
- 多路召回与融合重排序
- 有理有据的答案生成，最大程度降低幻觉

### 🚀 **自动化 RAG 工作流**
- 完整的 RAG 编排流程
- 可配置的 LLM 和向量模型
- 易用的 API 接口

## 📊 版本对比

| 功能特性 | 开源版 | 企业版 |
|---------|--------|--------|
| **核心 RAG 功能** | ✅ | ✅ |
| **深度文档理解** | ✅ | ✅ |
| **智能文本处理** | ✅ | ✅ |
| **自动化 RAG 工作流** | ✅ | ✅ |
| **MinerU 集成** | ✅ | ✅ |
| **国产数据库支持** | ❌ | ✅ |
| **ARM 架构支持** | ❌ | ✅ |
| **华为 910B NPU 支持** | ❌ | ✅ |

## 🌈 功能增强-企业版

- **MinerU 集成**：无缝集成 MinerU 功能，提供增强的数据挖掘和分析能力
- **国产数据库支持**：新增对达梦数据库的兼容性支持，为企业级中国数据库系统提供强大支持
- **ARM 架构支持**：完整支持基于 ARM 的系统，使其能够在更广泛的硬件平台上部署
- **华为 910B NPU 支持**：优化了对华为昇腾 910B NPU 的支持，提供加速的 AI 计算能力

## 🎬 快速开始

### 📋 系统要求
- CPU >= 4 核
- RAM >= 16 GB
- Disk >= 50 GB
- Docker >= 24.0.0 & Docker Compose >= v2.26.1

### 🚀 快速部署

1. **克隆项目**
   ```bash
   git clone https://github.com/infiniflow/ragforge.git
   cd ragforge/docker
   ```

2. **启动服务**
   ```bash
   # CPU 版本
   docker compose -f docker-compose.yml up -d
   
   # GPU 版本（加速 embedding 和 DeepDoc 任务）
   # docker compose -f docker-compose-gpu.yml up -d
   ```

3. **验证启动**
   ```bash
   docker logs -f ragforge-server
   ```

4. **访问系统**
   - 浏览器访问：`http://YOUR_SERVER_IP`
   - 配置 LLM API Key：编辑 `service_conf.yaml.template`

### ⚙️ 配置说明

- **.env**：基础环境变量（端口、密码等）
- **service_conf.yaml.template**：后端服务配置
- **docker-compose.yml**：容器编排配置

## 🔧 开发环境设置

### 🚀 快速启动开发环境

1. **启动 Docker 服务**
   ```bash
   cd docker
   ./start-dev.sh
   ```
   选择启动模式：
   - **选项 1**: 完整模式（包含 Infinity 向量数据库）
   - **选项 2**: 简化模式（推荐给 ARM64 Mac 用户）

2. **切换 API 配置**
   ```bash
   cd conf
   ./switch-to-dev.sh
   ```

3. **启动 API 服务器**
   ```bash
   # 回到项目根目录
   cd ..
   
   # 设置环境变量
   export PYTHONPATH=/Users/zhaozhilong/Desktop/cursor/Test/ragforge
   
   # 启动 API 服务器
   python api/main.py
   ```

### 🔧 服务配置详情

| 服务 | 地址 | 端口 | 用户名 | 密码 |
|------|------|------|--------|------|
| **Elasticsearch** | http://localhost | 9200 | elastic | changeme |
| **MySQL** | localhost | 3306 | root | ragforge123 |
| **MinIO** | http://localhost | 9000 | minioadmin | minioadmin |
| **MinIO Console** | http://localhost | 9001 | minioadmin | minioadmin |
| **Redis** | localhost | 6379 | - | ragforge123 |
| **Infinity** | http://localhost | 23820 | - | - |

### 🛠️ 环境变量配置

```bash
# 数据库类型
export DATABASE_TYPE=mysql  # 默认使用 MySQL
# export DATABASE_TYPE=dm   # 使用达梦数据库

# 文档引擎
export DOC_ENGINE=elasticsearch  # 默认使用 Elasticsearch
# export DOC_ENGINE=infinity     # 使用 Infinity 向量数据库

# 存储实现
export STORAGE_IMPL=MINIO  # 默认使用 MinIO
# export STORAGE_IMPL=AWS_S3  # 使用 AWS S3
```

### 📝 常用开发命令

```bash
# Docker 管理
cd docker
./start-dev.sh          # 启动服务
./stop-dev.sh           # 停止服务
docker-compose -f docker-compose-dev.yml ps  # 查看状态

# 配置管理
cd conf
./switch-to-dev.sh      # 切换到开发配置
./restore-original.sh   # 恢复原配置

# API 管理
python api/main.py      # 启动 API 服务器
nohup python api/main.py > api.log 2>&1 &  # 后台运行
```

### 🔍 故障排除

**Docker 服务启动失败**：
- Infinity 镜像不支持 ARM64：使用简化模式（选项 2）
- 端口冲突：修改 `.env` 文件中的端口配置

**API 连接失败**：
- 检查 Docker 服务状态：`docker-compose -f docker-compose-dev.yml ps`
- 重新应用配置：`cd conf && ./switch-to-dev.sh`

**Python 环境问题**：
- 设置 PYTHONPATH：`export PYTHONPATH=/Users/zhaozhilong/Desktop/cursor/Test/ragforge`
- 安装依赖：`uv sync --python 3.10 --all-extras`

## 🔧 源码编译

### 轻量版本（约 2GB）
```bash
docker build -f Dockerfile -t newragforge:slim .
```

### 完整版本（约 9GB）
```bash
docker build -f Dockerfile -t newragforge:full .
```

### ARM 架构支持
如需在 ARM64 平台运行，请参考[构建指南](https://ragforge.io/docs/dev/build_docker_image)自行编译镜像。

## 📚 文档资源

- [API 文档](https://ragforge.io/docs/dev/category/api)
- [配置指南](https://ragforge.io/docs/dev/category/configuration)
- [部署指南](https://ragforge.io/docs/dev/category/deployment)

## 🤝 商务合作

如有商务合作需求，请联系：business@infiniflow.com

---

**注意**：开发环境配置仅用于本地开发和测试，不要在生产环境中使用。
