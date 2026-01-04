# {{serviceName}} 数据库迁移历史

**创建日期**: {{date}}  
**数据库管理员**: {{dba}}  
**版本**: 1.0

## 概述

本文档记录 {{serviceName}} 微服务的数据库迁移历史，适配 Anchor Model 等数据建模方法。

## 迁移策略

### 迁移工具

{{migrationTool}}

### 迁移方式

{{migrationMethod}}

## 迁移历史记录

| 版本 | 迁移文件 | 描述 | 执行日期 | 执行人 | 回滚方案 |
|------|---------|------|---------|--------|---------|
| {{version1}} | {{migrationFile1}} | {{description1}} | {{executionDate1}} | {{executor1}} | {{rollbackPlan1}} |
| {{version2}} | {{migrationFile2}} | {{description2}} | {{executionDate2}} | {{executor2}} | {{rollbackPlan2}} |

## 迁移详细说明

### {{version1}}: {{migrationDescription1}}

#### 迁移内容

{{migrationContent1}}

#### 变更类型

{{changeType1}}（新增表/修改表/删除表/新增字段/修改字段/删除字段）

#### 影响范围

{{impactScope1}}

#### 数据迁移

{{dataMigration1}}

#### 回滚方案

{{rollbackPlan1}}

### {{version2}}: {{migrationDescription2}}

#### 迁移内容

{{migrationContent2}}

## 版本管理

### 当前版本

{{currentVersion}}

### 版本兼容性

{{versionCompatibility}}

## 迁移最佳实践

{{migrationBestPractices}}

## 相关文档

- [[schema.md]] - 数据库结构文档
- [[dataflow.md]] - 数据流说明

## 变更记录

| 日期 | 版本 | 变更内容 | 变更人 |
|------|------|----------|--------|
| {{date}} | 1.0 | 初始版本 | {{dba}} |

