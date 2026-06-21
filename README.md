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

计划部署到 Mintlify，并绑定 `https://docs.heihuzi.ai`。

## Mintlify 部署步骤

Mintlify CLI 当前没有直接部署命令，线上发布需要在 Mintlify 控制台完成：

1. 在 Mintlify 控制台创建或选择文档项目。
2. 连接当前 Git 仓库。
3. 将文档根目录设置为 `docs-api`。
4. 将生产分支设置为包含本目录的发布分支。
5. 确认 Mintlify 预览页可以打开 `/cn`。
6. 在项目域名设置中添加 `docs.heihuzi.ai`。
7. 按 Mintlify 给出的 DNS 记录，在域名 DNS 面板添加 CNAME/TXT 记录。
8. 等待 DNS 验证和 HTTPS 证书签发完成。
9. 验证 `https://docs.heihuzi.ai/cn` 返回 200。

注意：不要把 Mintlify 项目根目录指向仓库根目录，否则 Mintlify 会找不到 `docs-api/docs.json`。

## 范围说明

- Responses 是推荐的 OpenAI-compatible 入口。
- Chat Completions 作为旧客户端兼容入口公开。
- Claude Code 使用 Messages-compatible 入口。
- GPT Image 2 使用 OpenAI Images-compatible 的图像生成和图像编辑入口。
- 内部接口或未来接口在正式公开前，不写入对外 API 文档。
