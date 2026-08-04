---
title: 数据字典
version: 1.0.0
updated: 2026-08-04
---

# 数据字典

本文说明文档平台核心数据对象的字段含义与枚举值，供接口对接与排障参考。

## 1. Document 对象

| 字段 | 类型 | 说明 |
|------|------|------|
| id | string | 文档唯一标识，格式 `doc_<uuid>` |
| path | string | 仓库内逻辑路径，如 `docs/prd/auth.md` |
| version | string | 语义化版本，如 `1.2.0` |
| status | enum | `draft` / `published` / `archived` |
| owner | string | 文档负责人账号 |

## 2. Token 对象

| 字段 | 类型 | 说明 |
|------|------|------|
| access_token | string | 访问令牌，有效期 60 分钟 |
| refresh_token | string | 刷新令牌，有效期 30 天 |
| scope | enum | `read` / `write` / `admin` |

## 3. 状态码

- `DOC_NOT_FOUND`：路径对应的文档不存在。
- `TOKEN_EXPIRED`：访问令牌已过期，需走刷新流程。
- `PERMISSION_DENIED`：当前令牌缺少所需 scope。
