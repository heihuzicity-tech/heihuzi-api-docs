# 黑胡子AI便利店 API 文档

这里是黑胡子AI便利店对外 API 的 Mintlify 文档站点。

## 本地预览

```bash
cd docs-api
npx mintlify dev
```

## 发布前校验

```bash
cd docs-api
npx mintlify validate
npx mintlify broken-links
```

如需生成离线静态包，可执行：

```bash
cd docs-api
npx mintlify export --output /tmp/heihuzi-docs-export.zip
```

## 设计目标

- 使用 Mintlify `mint` 主题。
- 对齐 APIMart 风格的顶部标签、左侧能力导航、API 方法标识、请求示例、参数块和响应示例。
- 内容以黑胡子AI便利店当前真实公开 API 为准。
- 第三方文档只作为布局和阅读节奏参考，不作为接口契约来源。

## 公开 API 页面

- `POST /v1/responses`
- `POST /v1/chat/completions`
- `GET /v1/models`
- `POST /v1/messages`
- `POST /v1/images/generations`
- `POST /v1/images/edits`

## 生产 Base URL

公开示例统一使用 `https://code.heihuzi.ai`。

## 生产文档域名

已部署到 Mintlify，并绑定 `https://docs.heihuzi.ai`。

## Mintlify 部署步骤

Mintlify CLI 当前没有直接部署命令。当前线上发布采用独立 GitHub 仓库承载文档站：

```text
heihuzicity-tech/heihuzi-api-docs
```

正确流程：

1. 在主项目 `docs-api` 目录修改文档。
2. 运行 `npx mintlify@latest validate` 和 `npx mintlify@latest broken-links`。
3. 将 `docs-api` 内容同步到 `heihuzicity-tech/heihuzi-api-docs` 仓库根目录。
4. 在 Mintlify Git settings 中选择 `heihuzicity-tech / heihuzi-api-docs`、分支 `main`。
5. 确认 `docs.json is in a subdirectory` 关闭，因为部署仓库的 `docs.json` 位于根目录。
6. 确认 Authentication method 为 `Public`。
7. 验证 `https://heihuzi-ai.mintlify.app/cn` 和 `https://docs.heihuzi.ai/cn` 返回 200。

完整部署和 DNS 操作流程见：`../docs/API文档站部署与域名配置流程.md`。

## 范围说明

- Responses 是推荐的 OpenAI-compatible 入口。
- Chat Completions 作为旧客户端兼容入口公开。
- Claude Code 使用 Messages-compatible 入口。
- GPT Image 2.5 包含 `gpt-image-2.5-flare` 和 `gpt-image-2.5-sunburst`，保留 `gpt-image-2`；默认 Flare。
- 当前 2.5 官方绘图渠道使用 Images 生成和编辑入口。源码中的异步任务扩展当前未启用，不作为已开放 API 展示；该绘图渠道也不满足原生 Responses 生图条件。
- 参数接收、上游校验与生产配置必须分别核对。不能由路由注册、模型可见、单元测试通过或网页功能反推公共 API 已开放。
- 发布前按部署版本复核路由、权限、参数转换和返回分支，另查实时功能开关；本地测试不代替真实上游调用验证。
- 保留现有 `cn/api-reference/images/gpt-image-2/*` 和 `cn/user-guide/gpt-image-2` 页面路径，避免已有链接失效；页面内容已涵盖 2.5。
- 2026-09-10 已恢复此前被删除的独立发布仓库，Mintlify 已重新读取到 `main` 分支。发布后须核对部署成功状态和线上正文，不能将本地文档更新视为线上发布完成。
- 内部接口或未来接口在正式公开前，不写入对外 API 文档。
