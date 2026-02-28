# API 使用说明

## 健康检查

```bash
curl http://127.0.0.1:2048/health
```

## 列出模型

```bash
curl http://127.0.0.1:2048/v1/models
```

## 对话补全（非流式）

```bash
curl -X POST http://127.0.0.1:2048/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model":"gemini-2.5-pro",
    "messages":[{"role":"user","content":"请总结今天的任务"}],
    "temperature":0.8
  }'
```

## 对话补全（流式）

```bash
curl -X POST http://127.0.0.1:2048/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model":"gemini-2.5-pro",
    "stream":true,
    "messages":[{"role":"user","content":"写一段 100 字短文"}]
  }' --no-buffer
```

## API Key 鉴权

支持：

- `Authorization: Bearer <token>`（推荐）
- `X-API-Key: <token>`（兼容）

密钥与状态可通过管理路由维护（见 `api_utils/routers/api_keys.py`）。
