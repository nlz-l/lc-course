# AI 智能体应用 · 私人厨师助手

[![Python](https://img.shields.io/badge/python-3.13+-blue)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.115+-009688)](https://fastapi.tiangolo.com/)
[![LangChain](https://img.shields.io/badge/LangChain-0.3+-1C3C3C)](https://www.langchain.com/)
[![LangGraph](https://img.shields.io/badge/LangGraph-latest-1C3C3C)](https://langchain-ai.github.io/langgraph/)
[![DeepSeek](https://img.shields.io/badge/LLM-DeepSeek-4B6BFB)](https://www.deepseek.com/)

> 基于 LangGraph 的 AI 智能体应用，实现多模型接入、工具调用、状态编排和 FastAPI 服务封装。
> 附带完整 LangChain/LangGraph 学习笔记（Jupyter Notebook）。

---

## 🏗️ 智能体架构

```text
┌─────────────────────────────────────────────────────┐
│                    FastAPI 服务层                     │
│  POST /api/v1/chat          GET /api/v1/oss/upload  │
└──────────────────────┬──────────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────────┐
│                  LangGraph Agent                      │
│                                                       │
│  ┌─────────┐    ┌──────────┐    ┌─────────────────┐  │
│  │ 用户输入 ├───→│ 意图识别  ├───→│ 工具选择与调用    │  │
│  └─────────┘    └──────────┘    └────────┬────────┘  │
│                                          │            │
│                    ┌─────────────────────┘            │
│                    ▼                                  │
│  ┌─────────────────────────────────────┐             │
│  │           工具执行层                  │             │
│  │  ┌────────┐ ┌────────┐ ┌─────────┐  │             │
│  │  │搜索工具 │ │数据库   │ │ OSS 上传 │  │             │
│  │  │(Tavily)│ │(SQLite)│ │(阿里云)  │  │             │
│  │  └────────┘ └────────┘ └─────────┘  │             │
│  └─────────────────────────────────────┘             │
│                    │                                  │
│                    ▼                                  │
│  ┌─────────────────────────────────────┐             │
│  │           结果合成 → 输出             │             │
│  └─────────────────────────────────────┘             │
└──────────────────────────────────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────────┐
│                    模型层                             │
│  DeepSeek  │  DashScope  │  OpenAI  │  其他模型      │
└──────────────────────────────────────────────────────┘
```

---

## 📂 项目结构

```text
lc-course/
├── app/
│   ├── main.py                   # FastAPI 入口：生命周期管理、路由注册
│   ├── agents/
│   │   └── personal_chief.py     # 核心：LangGraph 状态图定义与节点实现
│   ├── api/v1/
│   │   ├── chat.py               # 聊天接口：接收消息 → Agent 处理 → 流式返回
│   │   └── oss.py                # OSS 上传：生成临时凭证，前端直传阿里云
│   ├── models/schemas.py         # Pydantic 数据模型
│   ├── common/logger.py          # 日志工具
│   └── static/                   # 前端静态资源（Next.js 构建产物）
├── notebooks/                    # LangChain/LangGraph 课程笔记
│   ├── 第一章 AI 基础
│   ├── 第二章 LangChain 入门（模型、消息、提示词、工具、记忆、实战）
│   └── 进阶 Runtime & Middleware
├── langgraph.json                # LangGraph CLI 配置
├── pyproject.toml
└── .env.example
```

---

## 🔧 技术选型

| 决策点 | 选择 | 理由 |
|---|---|---|
| **Agent 框架** | LangGraph | 相比 LangChain Agent，图状态编排更灵活、可调试 |
| **LLM** | DeepSeek（主力） + DashScope + OpenAI | 多模型对比实验，DeepSeek 性价比最高 |
| **搜索工具** | Tavily API | 专为 AI Agent 设计的搜索，返回结构化结果 |
| **Web 框架** | FastAPI | 异步支持、自动文档、与 Python 生态无缝 |
| **文件上传** | 阿里云 OSS 临时凭证 | 服务端不存文件，减轻带宽压力 |
| **存储** | SQLite | 学习场景够用，零配置，方便迁移 |

---

## 🚀 快速开始

```bash
git clone https://github.com/your/lc-course.git
cd lc-course

# 安装依赖
uv sync

# 配置环境变量
cp .env.example .env
# 编辑 .env：DEEPSEEK_API_KEY, TAVILY_API_KEY, OSS 配置等

# 启动
uv run python -m app.main        # → http://localhost:8000/docs
```

---

