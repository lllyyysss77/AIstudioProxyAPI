# 排障指南

## 1. 启动后无法连接 AI Studio

排查顺序：

1. 检查代理配置：`UNIFIED_PROXY_CONFIG`。
2. 检查认证文件是否有效：`auth_profiles/active/`。
3. 用 `--debug` 复现，确认页面可打开并正常提交。

## 2. `/v1/chat/completions` 超时

建议：

- 调整 `RESPONSE_COMPLETION_TIMEOUT` 与 `SILENCE_TIMEOUT_MS`。
- 检查模型是否可用、页面是否卡住。
- 查看 `logs/` 与 `errors_py/` 日志。

## 3. 函数调用异常

- 将 `FUNCTION_CALLING_MODE` 切换到 `auto`。
- 开启 `FUNCTION_CALLING_DEBUG=true` 与对应 `FC_DEBUG_*` 模块。
- 检查 `config/selectors.py` 是否需要更新到新 UI。

## 4. 认证轮转行为不符合预期

- 检查 `AUTO_ROTATE_AUTH_PROFILE` 与 `AUTO_AUTH_ROTATION_ON_STARTUP`。
- 检查 `QUOTA_SOFT_LIMIT` / `QUOTA_HARD_LIMIT`。
- 确保存在可轮转 profile。

## 5. GUI 启动异常

- 检查 `customtkinter`、`pillow` 是否安装。
- 通过 CLI 先验证服务可启动，再回到 GUI。
