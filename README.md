# AI Studio Proxy API

将 Google AI Studio 网页能力封装为 OpenAI 兼容 API 的代理服务。

项目通过 `Camoufox + Playwright` 驱动 AI Studio 页面，提供 `/v1/chat/completions`、`/v1/models` 等接口，并包含 Web UI、GUI 启动器、认证轮转、Cookie 刷新、函数调用（Native/Emulated）等能力。

## 核心特性

- OpenAI 兼容接口：支持流式/非流式对话。
- 函数调用三模式：`auto` / `native` / `emulated`，支持失败回退。
- 认证体系增强：支持 profile 轮转、启动时自动选取、配额阈值策略。
- Cookie 生命周期维护：周期刷新、请求后保存、退出前保存。
- 启动链路完整：CLI 启动器、内置 Web UI、桌面 GUI 启动器。
- CI/CD 工作流：PR 检查、Release、上游同步流程。

## 目录概览

- `api_utils/`：FastAPI 应用、路由、请求处理与响应生成。
- `browser_utils/`：页面初始化、交互、模型切换、函数调用 UI 自动化。
- `config/`：配置读取、默认值、选择器、超时与全局状态。
- `gui/`：桌面启动器与设置面板。
- `stream/`：流式代理服务。
- `static/frontend/`：React 前端。
- `tests/`：后端/浏览器/流式/GUI/工作流测试。

## 快速开始

### 1. 克隆与安装

```bash
git clone https://github.com/CJackHwang/AIstudioProxyAPI.git
cd AIstudioProxyAPI
poetry install --with dev
```

### 2. 配置环境变量

```bash
cp .env.example .env
```

建议最少确认以下项：

- `PORT`、`STREAM_PORT`
- `UNIFIED_PROXY_CONFIG`（需要代理时）
- `LAUNCH_MODE`
- `AUTO_SAVE_AUTH`、`AUTO_ROTATE_AUTH_PROFILE`
- `FUNCTION_CALLING_MODE`

### 3. 首次认证与启动

```bash
# 首次建议 debug 模式，完成登录并保存 auth
poetry run python launch_camoufox.py --debug

# 日常服务建议 headless
poetry run python launch_camoufox.py --headless
```

## 常用验证

```bash
# 健康检查
curl http://127.0.0.1:2048/health

# 模型列表
curl http://127.0.0.1:2048/v1/models

# 非流式对话
curl -X POST http://127.0.0.1:2048/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{"model":"gemini-2.5-pro","messages":[{"role":"user","content":"你好"}]}'

# 流式对话
curl -X POST http://127.0.0.1:2048/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{"model":"gemini-2.5-pro","stream":true,"messages":[{"role":"user","content":"写一个三行小诗"}]}' --no-buffer
```

## 文档导航

- [文档总览](docs/README.md)
- [快速开始](docs/quick-start.md)
- [配置参考](docs/configuration-reference.md)
- [认证轮转与 Cookie 刷新](docs/auth-rotation-cookie-refresh.md)
- [函数调用模式](docs/function-calling.md)
- [API 使用说明](docs/api-usage.md)
- [排障指南](docs/troubleshooting.md)
- [开发、测试与发布](docs/development-and-release.md)
- [旧文档迁移说明](docs/migration-notes.md)

## 开发检查

```bash
poetry run ruff check .
poetry run pyright
poetry run pytest
```

前端（可选）:

```bash
cd static/frontend
npm ci
npm run build
```

## 版本与发布

本仓库当前维持自有版本线（示例：`0.1.0`）。

- 稳定版发布：推送 tag，如 `v0.1.0`
- Nightly 发布：`main` 分支 push 自动触发
- 上游同步：使用 `Sync with Upstream` 工作流

## 致谢

- 原始项目与主线实现：[@CJackHwang](https://github.com/CJackHwang)
- 历史改进贡献者与社区反馈：Linux.do 社区及各位贡献者
