# LangChain / LangGraph 课程练习项目

![Python](https://img.shields.io/badge/python-3.13+-blue)
![FastAPI](https://img.shields.io/badge/FastAPI-0.115+-009688)
![LangChain](https://img.shields.io/badge/LangChain-0.3+-1C3C3C)
![LangGraph](https://img.shields.io/badge/LangGraph-latest-1C3C3C)
![Status](https://img.shields.io/badge/status-learning-orange)

AI 应用开发练习项目，涵盖 LangChain 工具调用、LangGraph 智能体编排、FastAPI 服务封装。项目包含 Jupyter Notebook 学习笔记和一个「私人厨师助手」后端应用。

## 项目结构

```text
lc-course/
├── app/
│   ├── main.py                       # FastAPI 应用入口
│   ├── agents/
│   │   └── personal_chief.py         # 私人厨师助手智能体（LangGraph）
│   ├── api/v1/
│   │   ├── chat.py                   # 聊天接口
│   │   └── oss.py                    # 阿里云 OSS 上传 URL 接口
│   ├── models/
│   │   └── schemas.py                # Pydantic 请求/响应模型
│   ├── db/                           # SQLite 数据库
│   ├── common/
│   │   └── logger.py                 # 日志工具
│   └── static/                       # 前端静态文件
├── notebooks/                        # 课程 Jupyter Notebook 笔记
├── langgraph.json                    # LangGraph CLI / Studio 配置
├── pyproject.toml                    # 项目依赖 (uv)
├── .env.example                      # 环境变量模板
└── README.md
```

## 快速开始

### 环境要求

- Python 3.13+
- [uv](https://docs.astral.sh/uv/)
- 可选：[LangGraph Studio](https://langchain-ai.github.io/langgraph/cloud/langgraph_studio/) 或 [LangSmith](https://smith.langchain.com/)

### 安装与配置

```bash
# 安装依赖
uv sync

# 配置环境变量
cp .env.example .env
# 编辑 .env，填入模型 API Key、LangSmith Key、OSS 配置等
```

### 启动服务

```bash
# 方式一：直接运行
uv run python -m app.main

# 方式二：使用 uvicorn（开发热重载）
uv run uvicorn app.main:app --reload
```

启动后访问：http://localhost:8000/docs

## API 端点

| 方法 | 路径 | 说明 |
|---|---|---|
| POST | `/api/v1/chat` | AI 对话接口 |
| GET | `/api/v1/oss/upload-url` | 获取阿里云 OSS 上传凭证 |

## Notebook 学习笔记

`notebooks/` 目录包含课程学习笔记：

### 第一章：AI 基础
- AI 应用开发概述

### 第二章：LangChain 入门
| Notebook | 主题 |
|---|---|
| 2.1 | 模型接入（LLM/Chat Model） |
| 2.2 | 消息与对话管理 |
| 2.3 | Prompt 模板 |
| 2.4 | 工具定义与调用 |
| 2.5 | 记忆系统（Memory） |
| 2.6 | 实战练习 |

### 进阶
- Runtime 环境配置
- Middleware 中间件
- 私人助手 Agent 实战

## 技术栈

| 组件 | 用途 |
|---|---|
| **LangChain** | LLM 应用框架（工具调用、模型接入、Prompt 管理） |
| **LangGraph** | 智能体状态编排（节点、边、条件路由） |
| **FastAPI** | HTTP API 封装 |
| **DeepSeek** | 主要使用的 LLM |
| **DashScope** | 阿里云灵积模型服务 |
| **Tavily** | 联网搜索 API |
| **SQLite** | 本地数据存储 |
| **LangSmith** | 链路追踪与调试（可选） |

## 学习重点

1. **LangChain 工具调用** — 如何定义工具、让 LLM 自主选择调用
2. **LangGraph 状态图** — 节点编排、条件边、状态管理
3. **FastAPI 封装** — 将 AI 能力暴露为 HTTP 服务
4. **OSS 文件上传** — 临时凭证生成、前端直传
5. **Notebook → 应用** — 从实验到工程化的完整流程

## 注意事项

- `.env` 文件包含 API Key，不要提交到版本控制
- `.langgraph_api/` 为 LangGraph Studio 本地调试缓存
- `app/static/` 中的前端静态文件为 Next.js 构建产物
