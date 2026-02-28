# 认证轮转与 Cookie 刷新

## 认证目录

- `auth_profiles/active/`：当前可用 profile。
- `auth_profiles/saved/`：历史保存 profile。
- `auth_profiles/emergency/`：应急 profile。

## 推荐流程

1. 使用 `--debug` 完成登录。
2. 将保存的 profile 放入 `active/`。
3. 生产环境使用 `--headless`。

## 自动轮转策略

相关配置：

- `AUTO_ROTATE_AUTH_PROFILE=true`
- `AUTO_AUTH_ROTATION_ON_STARTUP=true|false`
- `QUOTA_SOFT_LIMIT`：触发“当前请求完成后轮转”
- `QUOTA_HARD_LIMIT`：触发更强保护策略

## Cookie 自动刷新

建议在长期运行场景开启：

- `COOKIE_REFRESH_ENABLED=true`
- `COOKIE_REFRESH_INTERVAL_SECONDS=1800`
- `COOKIE_REFRESH_ON_REQUEST_ENABLED=true`
- `COOKIE_REFRESH_ON_SHUTDOWN=true`

作用：

- 减少认证过期导致的可用性波动。
- 关闭服务时自动持久化最新 cookie。
