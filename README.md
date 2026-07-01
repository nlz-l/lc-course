# LangChain / LangGraph 课程练习项目

这是一个围绕 LangChain、LangGraph、Notebook 和 FastAPI 的 AI 应用练习项目。项目一方面保存课程学习笔记和实验 Notebook，另一方面实现了一个“私人厨师助手”后端，用来练习智能体、聊天接口、OSS 上传地址生成和 LangGraph 调试。

## 主要内容

- `notebooks/`：LangChain、LangGraph 课程 Notebook 和个人 Agent 练习笔记
- `app/main.py`：FastAPI 应用入口
- `app/api/v1/chat.py`：聊天接口
- `app/api/v1/oss.py`：阿里云 OSS 上传 URL 相关接口
- `app/agents/personal_chief.py`：私人厨师助手智能体逻辑
- `app/models/`：接口请求和响应模型
- `app/common/`：日志等公共工具
- `langgraph.json`：LangGraph CLI / Studio 相关配置

## 环境要求

- Python 3.13 或更高版本
- uv
- 可选：LangGraph Studio / LangSmith，用于调试智能体链路

## 安装依赖

```bash
uv sync
```

首次运行前复制环境变量文件：

```bash
copy .env.example .env
```

然后在 `.env` 中填写模型、搜索、LangSmith、阿里云 OSS 等相关配置。仓库中的真实密钥不要提交到版本控制。

## 启动服务

```bash
uv run python -m app.main
```

也可以使用 uvicorn：

```bash
uv run uvicorn app.main:app --reload
```

## 学习重点

- LangChain 工具调用与模型接入
- LangGraph 智能体状态流转和节点编排
- FastAPI 封装 AI 能力为 HTTP 接口
- OSS 上传凭证生成与前后端文件上传流程
- Notebook 中快速验证想法，再沉淀为应用代码
