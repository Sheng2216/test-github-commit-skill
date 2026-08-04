---
title: 用户接口文档
version: 1.0.0
updated: 2026-08-04
---

# 用户接口文档

本文定义文档平台对外暴露的 REST 接口，供前端与第三方集成方使用。基础路径为 `/api/v1`。

## 1. 认证接口

- `POST /api/v1/auth/login`：邮箱密码登录，返回 Access Token 与 Refresh Token。
- `POST /api/v1/auth/refresh`：使用 Refresh Token 换取新的 Access Token。
- `POST /api/v1/auth/logout`：吊销当前会话。

## 2. 文档读写接口

- `GET /api/v1/docs/{path}`：按路径读取文档当前版本。
- `PUT /api/v1/docs/{path}`：写入文档并生成新版本，需要 `write` 权限。
- `GET /api/v1/docs/{path}/history`：获取版本历史列表。

## 3. 通用约定

- 所有请求须在 `Authorization: Bearer <token>` 头中携带令牌。
- 错误统一返回 `{ "code": 0, "message": "..." }`，HTTP 状态码与业务码分离。
- 分页参数 `page`（从 1 开始）与 `size`（默认 20，上限 100）。
