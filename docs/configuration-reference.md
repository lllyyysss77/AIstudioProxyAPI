# 配置参考

配置入口：`.env`（模板见 `.env.example`）。

## 1. 端口与代理

- `PORT`：主 API 端口。
- `STREAM_PORT`：流式代理端口，`0` 为关闭。
- `UNIFIED_PROXY_CONFIG`：统一代理配置，优先级最高。
- `HTTP_PROXY` / `HTTPS_PROXY`：兼容旧代理配置。
- `NO_PROXY`：代理绕过规则。

## 2. 日志

- `SERVER_LOG_LEVEL`：日志级别。
- `SERVER_REDIRECT_PRINT`：是否重定向 `print`。
- `JSON_LOGS`：JSON 日志输出。
- `LOG_FILE_MAX_BYTES` / `LOG_FILE_BACKUP_COUNT`：日志滚动策略。

## 3. 认证与轮转

- `AUTO_SAVE_AUTH`：debug 登录后自动保存认证。
- `AUTO_ROTATE_AUTH_PROFILE`：配额异常时自动轮转认证 profile。
- `AUTO_AUTH_ROTATION_ON_STARTUP`：启动时自动选择 profile。
- `QUOTA_SOFT_LIMIT` / `QUOTA_HARD_LIMIT`：轮转阈值。

## 4. 浏览器与模型

- `LAUNCH_MODE`：`normal` / `debug` / `headless` / `virtual_display`。
- `CAMOUFOX_WS_ENDPOINT`：连接外部浏览器实例。
- `ONLY_COLLECT_CURRENT_USER_ATTACHMENTS`：附件收集策略。

## 5. 函数调用

- `FUNCTION_CALLING_MODE`：`auto` / `native` / `emulated`。
- `FUNCTION_CALLING_NATIVE_FALLBACK`：native 失败是否回退。
- `FUNCTION_CALLING_UI_TIMEOUT`：UI 操作超时。
- `FUNCTION_CALLING_CACHE_ENABLED`：启用 FC 缓存。

## 6. Cookie 刷新

- `COOKIE_REFRESH_ENABLED`
- `COOKIE_REFRESH_INTERVAL_SECONDS`
- `COOKIE_REFRESH_ON_REQUEST_ENABLED`
- `COOKIE_REFRESH_REQUEST_INTERVAL`
- `COOKIE_REFRESH_ON_SHUTDOWN`

## 7. 超时与稳定性

- `RESPONSE_COMPLETION_TIMEOUT`
- `SILENCE_TIMEOUT_MS`
- `CLICK_TIMEOUT_MS`
- `WAIT_FOR_ELEMENT_TIMEOUT_MS`
- `STREAM_MAX_INITIAL_ERRORS` 等流式抑制参数。

## 8. GUI 与前端

- `GUI_DEFAULT_PROXY_ADDRESS`
- `GUI_DEFAULT_STREAM_PORT`
- `GUI_DEFAULT_HELPER_ENDPOINT`
- `SKIP_FRONTEND_BUILD`：无 Node 环境时可跳过构建检查。
