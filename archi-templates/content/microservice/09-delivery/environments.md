# {{serviceName}} 环境说明

**创建日期**: {{date}}  
**DevOps工程师**: {{devops}}  
**版本**: 1.0

## 概述

本文档描述 {{serviceName}} 微服务的环境配置，包括开发、测试、预生产和生产环境。

## 环境列表

| 环境名称 | 用途 | 访问地址 | 描述 |
|---------|------|---------|------|
| dev | 开发环境 | {{devUrl}} | {{devDescription}} |
| test | 测试环境 | {{testUrl}} | {{testDescription}} |
| stage | 预生产环境 | {{stageUrl}} | {{stageDescription}} |
| prod | 生产环境 | {{prodUrl}} | {{prodDescription}} |

## 环境配置

### 开发环境（dev）

#### 配置信息

{{devConfiguration}}

#### 资源配额

{{devResourceQuota}}

#### 访问权限

{{devAccessPermissions}}

### 测试环境（test）

#### 配置信息

{{testConfiguration}}

#### 资源配额

{{testResourceQuota}}

#### 访问权限

{{testAccessPermissions}}

### 预生产环境（stage）

#### 配置信息

{{stageConfiguration}}

#### 资源配额

{{stageResourceQuota}}

#### 访问权限

{{stageAccessPermissions}}

### 生产环境（prod）

#### 配置信息

{{prodConfiguration}}

#### 资源配额

{{prodResourceQuota}}

#### 访问权限

{{prodAccessPermissions}}

## 环境差异

### 配置差异

| 配置项 | dev | test | stage | prod |
|--------|-----|------|-------|------|
| {{configItem1}} | {{devValue1}} | {{testValue1}} | {{stageValue1}} | {{prodValue1}} |
| {{configItem2}} | {{devValue2}} | {{testValue2}} | {{stageValue2}} | {{prodValue2}} |

## 环境管理

### 环境创建

{{environmentCreation}}

### 环境更新

{{environmentUpdate}}

### 环境销毁

{{environmentDestruction}}

## 环境监控

{{environmentMonitoring}}

## 相关文档

- [[ci.md]] - CI流水线配置
- [[cd.md]] - CD发布文档
- [[../05-operations/deployment.md]] - 部署架构

## 变更记录

| 日期 | 版本 | 变更内容 | 变更人 |
|------|------|----------|--------|
| {{date}} | 1.0 | 初始版本 | {{devops}} |

