# 快速开始

## 环境要求

- Python `>=3.9,<4.0`
- Poetry
- Node.js（仅前端开发/构建需要）
- 可访问 Google AI Studio 的网络环境

## 安装

```bash
git clone https://github.com/CJackHwang/AIstudioProxyAPI.git
cd AIstudioProxyAPI
poetry install --with dev
```

## 初始化配置

```bash
cp .env.example .env
```

建议先配置：

- `PORT=2048`
- `STREAM_PORT=3120`（不需要流式代理可设为 `0`）
- `UNIFIED_PROXY_CONFIG`（按需）
- `LAUNCH_MODE=debug`（首次认证）
- `AUTO_SAVE_AUTH=true`（首次认证可开启）

## 启动

首次认证：

```bash
poetry run python launch_camoufox.py --debug
```

完成认证文件保存后，日常运行：

```bash
poetry run python launch_camoufox.py --headless
```

## 最小验证

```bash
curl http://127.0.0.1:2048/health
curl http://127.0.0.1:2048/v1/models
```
