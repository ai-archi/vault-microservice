# {{serviceName}} 目录结构设计

**创建日期**: {{date}}  
**架构师**: {{architect}}  
**版本**: 1.0

## 概述

本文档描述 {{serviceName}} 微服务项目的目录结构设计，包括代码组织、模块划分和文件布局。

{{projectStructureDescription}}

## 根目录结构

```
{{projectRoot}}/
├── {{configDir}}/                      # 配置文件目录
│   └── {{configFiles}}                 # 配置文件
├── {{srcDir}}/                         # 源代码目录
│   ├── {{mainPackage}}/                # 主包
│   ├── {{testPackage}}/                # 测试包
│   └── {{resourcesPackage}}/           # 资源文件
├── {{docsDir}}/                        # 文档目录
│   └── {{archidocs}}/                  # 架构文档
├── {{scriptsDir}}/                     # 脚本目录
│   └── {{buildScripts}}/               # 构建脚本
├── {{configFile}}                      # 项目配置文件
├── {{readmeFile}}                      # 项目说明文件
└── {{gitignoreFile}}                   # Git 忽略配置
```

## 源代码目录结构

### {{srcDir}}/{{mainPackage}}/

主源代码目录，采用 {{architecturePattern}} 架构模式组织代码。

**目录结构**：

```
{{srcDir}}/{{mainPackage}}/
├── {{presentationLayer}}/              # 表现层
│   ├── {{controllers}}/                # 控制器
│   ├── {{dto}}/                        # DTO
│   └── {{validators}}/                 # 验证器
├── {{applicationLayer}}/               # 应用层
│   ├── {{services}}/                   # 应用服务
│   ├── {{commands}}/                   # 命令处理器（CQRS）
│   ├── {{queries}}/                    # 查询处理器（CQRS）
│   └── {{handlers}}/                   # 事件处理器
├── {{domainLayer}}/                    # 领域层
│   ├── {{coreDomain}}/                 # 核心域
│   │   ├── {{aggregates}}/             # 聚合
│   │   ├── {{entities}}/               # 实体
│   │   ├── {{valueObjects}}/           # 值对象
│   │   ├── {{domainServices}}/         # 领域服务
│   │   └── {{domainEvents}}/           # 领域事件
│   ├── {{supportingDomain}}/           # 支撑域
│   └── {{genericDomain}}/              # 通用域
└── {{infrastructureLayer}}/            # 基础设施层
    ├── {{persistence}}/                # 持久化
    ├── {{messaging}}/                  # 消息队列
    ├── {{external}}/                   # 外部服务集成
    └── {{config}}/                     # 配置管理
```

### {{srcDir}}/{{testPackage}}/

测试代码目录，与主代码目录结构保持一致。

**目录结构**：

```
{{srcDir}}/{{testPackage}}/
├── {{unitTests}}/                      # 单元测试
├── {{integrationTests}}/               # 集成测试
├── {{e2eTests}}/                       # 端到端测试
└── {{testFixtures}}/                   # 测试夹具
```

## 配置文件说明

### {{configFile}}

{{configFileDescription}}

### {{configDir}}/

{{configDirDescription}}

## 文档目录结构

### {{docsDir}}/{{archidocs}}/

架构文档目录，包含服务的所有架构设计文档。

**目录结构**：

```
{{docsDir}}/{{archidocs}}/
└── {{serviceDocs}}/
    ├── {{overviewDir}}/                # 概览文档
    ├── {{domainDir}}/                  # 领域设计文档
    ├── {{apiDir}}/                     # API 文档
    └── {{otherDocs}}/                  # 其他文档
```

**文档与代码关联**：

- 架构文档描述系统的设计理念和结构
- 代码实现遵循架构文档的设计
- 文档和代码保持同步更新

## 构建和部署目录

### {{scriptsDir}}/

开发工具、构建脚本和部署脚本。

**目录结构**：

```
{{scriptsDir}}/
├── {{buildScripts}}/                   # 构建脚本
│   ├── {{buildScript1}}                # 构建脚本1
│   └── {{buildScript2}}                # 构建脚本2
├── {{deployScripts}}/                  # 部署脚本
│   └── {{deployScript}}                # 部署脚本
└── {{testScripts}}/                    # 测试脚本
    └── {{testScript}}                  # 测试脚本
```

## 目录结构设计原则

1. **{{principle1}}**: {{principleDescription1}}
2. **{{principle2}}**: {{principleDescription2}}
3. **{{principle3}}**: {{principleDescription3}}

## 目录结构可视化

### 整体结构图

```mermaid
graph TB
    subgraph "{{projectRoot}}"
        A[{{srcDir}}/]
        B[{{docsDir}}/]
        C[{{scriptsDir}}/]
        D[{{configDir}}/]
    end

    subgraph "源代码"
        A1[{{presentationLayer}}/]
        A2[{{applicationLayer}}/]
        A3[{{domainLayer}}/]
        A4[{{infrastructureLayer}}/]
    end

    A --> A1
    A --> A2
    A --> A3
    A --> A4
```

### 分层架构图

```mermaid
graph TB
    subgraph "{{serviceName}} 分层架构"
        P[{{presentationLayer}}]
        A[{{applicationLayer}}]
        D[{{domainLayer}}]
        I[{{infrastructureLayer}}]
    end

    P -->|依赖| A
    A -->|依赖| D
    I -->|实现| D
    A -->|使用| I
```

## 相关文档

- [[service-overview.md]] - 服务概览
- [[architecture.md]] - 架构概览
- [[context-diagram.md]] - 系统上下文图
- [[../02-domain/domain-overview.md]] - 领域概览

## 变更记录

| 日期     | 版本 | 变更内容 | 变更人        |
| -------- | ---- | -------- | ------------- |
| {{date}} | 1.0  | 初始版本 | {{architect}} |
