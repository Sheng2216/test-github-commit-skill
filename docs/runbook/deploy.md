---
title: 部署运维手册
version: 1.0.0
updated: 2026-08-04
---

# 部署运维手册

## 1. 部署步骤

1. 拉取指定版本镜像：`docker pull docs-platform:{{version}}`。
2. 执行数据库迁移：`docker compose run --rm migrate`。
3. 启动服务栈：`docker compose up -d`。
4. 确认网关健康：`curl -f http://localhost/healthz`。

## 2. 健康检查

- 网关：`GET /healthz` 返回 200 即正常。
- 内容服务：依赖的对象存储连通性，异常时日志出现 `OBJ_STORE_UNREACHABLE`。

## 3. 回滚

若新版本存在问题，执行 `docker compose up -d --scale gateway=0` 先摘流量，
再回退到上一稳定标签并重新部署。

## 4. 常见问题

- 启动后 502：多为内容服务未就绪，等待 30 秒后重试健康检查。
- 迁移失败：检查数据库账号是否有 DDL 权限。
