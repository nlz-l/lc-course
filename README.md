# LangChain / LangGraph 课程项目

[![Python](https://img.shields.io/badge/python-3.13+-blue)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.115+-009688)](https://fastapi.tiangolo.com/)
[![LangChain](https://img.shields.io/badge/LangChain-0.3+-1C3C3C)](https://www.langchain.com/)
[![LangGraph](https://img.shields.io/badge/LangGraph-latest-1C3C3C)](https://langchain-ai.github.io/langgraph/)

AI 应用开发练习项目，涵盖 LangChain 工具调用、LangGraph 智能体编排和 FastAPI 服务封装。包含 Jupyter Notebook 课程笔记和一个「私人厨师助手」后端。

---

## 📂 项目结构

```text
lc-course/
├── app/
│   ├── main.py                       # FastAPI 应用入口
│   ├── agents/
│   │   └── personal_chief.py         # 私人厨师助手智能体（LangGraph）
│   ├── api/v1/
│   │   ├── chat.py                   # 聊天接口
│   │   └── oss.py                    # 阿里云 OSS 上传 URL 接口
│   ├── models/schemas.py             # Pydantic 数据模型
│   ├── common/logger.py              # 日志工具
│   └── static/                       # 前端静态文件
├── notebooks/                        # 课程 Jupyter Notebook 笔记
├── langgraph.json                    # LangGraph CLI 配置
├── pyproject.toml                    # 依赖配置（uv）
├── .env.example                      # 环境变量模板
└── README.md
```

---

## 🚀 快速开始

环境要求：Python 3.13+、[uv](https://docs.astral.sh/uv/)

```bash
uv sync
cp .env.example .env                  # 编辑 .env，填入 API Key 等配置
uv run python -m app.main             # → http://localhost:8000/docs
```

或使用热重载：

```bash
uv run uvicorn app.main:app --reload
```

---

## 📡 接口列表

| 方法 | 路径 | 说明 |
|---|---|---|
| POST | `/api/v1/chat` | AI 聊天对话 |
| GET | `/api/v1/oss/upload-url` | 获取 OSS 上传凭证 |

---

## 📓 课程笔记

`notebooks/` 目录包含系统化的课程笔记：

| 章节 | 主题 |
|---|---|
| 第一章 | AI 应用基础 |
| 第二章 1–6 | LangChain：模型、消息、提示词、工具、记忆 |
| 进阶 | Runtime、Middleware、私人助手 Agent |

---

## 🛠️ 技术栈

| 组件 | 用途 |
|---|---|
| **LangChain** | 大模型应用框架（工具调用、Prompt 管理） |
| **LangGraph** | 智能体状态编排（节点、边、条件路由） |
| **FastAPI** | HTTP 接口封装 |
| **DeepSeek** | 主要大模型 |
| **DashScope** | 阿里云灵积模型服务 |
| **Tavily** | 联网搜索 API |
| **SQLite** | 本地数据存储 |
| **LangSmith** | 链路追踪与调试（可选） |

---

## 🎯 学习重点

1. **LangChain 工具调用** — 定义工具并让 LLM 自主选择调用
2. **LangGraph 状态图** — 节点编排、条件边、状态管理
3. **FastAPI 封装** — 将 AI 能力暴露为 HTTP 服务
4. **OSS 文件上传** — 临时凭证生成、前端直传
5. **Notebook → 应用** — 从实验到工程化的完整流程

---

## ⚠️ 注意事项

- `.env` 包含 API Key，**不要提交到版本控制**
- `app/static/` 为 Next.js 构建产物
