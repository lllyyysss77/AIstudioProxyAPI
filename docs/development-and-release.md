# 开发、测试与发布

## 本地开发

```bash
poetry install --with dev
poetry run ruff check .
poetry run pyright
poetry run pytest
```

前端：

```bash
cd static/frontend
npm ci
npm run build
npm run test
```

## 推荐测试分层

- 单元与组件测试：`pytest` 默认集合
- 关键集成验证：`tests/integration/` 相关用例
- 前端构建与基础交互冒烟

## GitHub Actions

- `PR Check`：代码质量与测试检查
- `Release`：
  - tag 触发稳定版
  - main push 触发 nightly
  - 支持手动输入版本发布
- `Sync with Upstream`：从 `CJackHwang/AIstudioProxyAPI` 同步并自动建 PR

## 发布示例

```bash
git tag v0.1.0
git push origin v0.1.0
```
