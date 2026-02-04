# {{serviceName}} 领域概览

**创建日期**: {{date}}  
**架构师**: {{architect}}  
**版本**: 1.0

## 概述

本文档描述 {{serviceName}} 微服务的整体领域划分，包括所有业务领域的划分、职责边界和领域之间的依赖关系。

> **说明**：本文档是系统级的领域概览，描述整个微服务包含的所有业务领域。单个领域的详细说明请参考各领域目录下的 `01-domain-overview.md` 文档。

## 领域划分

### 领域划分图

```mermaid
graph TB
    subgraph "{{serviceName}} 微服务"
        {{domain1}}[{{domain1Name}}]
        {{domain2}}[{{domain2Name}}]
        {{domain3}}[{{domain3Name}}]
    end
    
    {{domain1}} -->|{{dependency1}}| {{domain2}}
    {{domain2}} -->|{{dependency2}}| {{domain3}}
```

### 业务领域列表

| 领域名称 | 领域标识 | 职责描述 | 重要性 | 详细文档 |
|---------|---------|---------|--------|---------|
| {{domain1Name}} | {{domain1Id}} | {{domain1Description}} | {{domain1Importance}} | [[../{{domain1Id}}/01-domain-overview.md]] |
| {{domain2Name}} | {{domain2Id}} | {{domain2Description}} | {{domain2Importance}} | [[../{{domain2Id}}/01-domain-overview.md]] |
| {{domain3Name}} | {{domain3Id}} | {{domain3Description}} | {{domain3Importance}} | [[../{{domain3Id}}/01-domain-overview.md]] |

## 领域职责划分

### {{domain1Name}}

**职责**：
- {{domain1Responsibility1}}
- {{domain1Responsibility2}}

**边界**：
- ✅ {{domain1InScope1}}
- ✅ {{domain1InScope2}}
- ❌ {{domain1OutScope1}}

### {{domain2Name}}

**职责**：
- {{domain2Responsibility1}}
- {{domain2Responsibility2}}

**边界**：
- ✅ {{domain2InScope1}}
- ✅ {{domain2InScope2}}
- ❌ {{domain2OutScope1}}

### {{domain3Name}}

**职责**：
- {{domain3Responsibility1}}
- {{domain3Responsibility2}}

**边界**：
- ✅ {{domain3InScope1}}
- ✅ {{domain3InScope2}}
- ❌ {{domain3OutScope1}}

## 领域依赖关系

### 依赖关系图

```mermaid
graph LR
    {{domain1}}[{{domain1Name}}]
    {{domain2}}[{{domain2Name}}]
    {{domain3}}[{{domain3Name}}]
    
    {{domain1}} -->|{{dependencyType1}}| {{domain2}}
    {{domain2}} -->|{{dependencyType2}}| {{domain3}}
```

### 依赖关系说明

| 源领域 | 目标领域 | 依赖类型 | 依赖原因 | 交互方式 |
|--------|---------|---------|---------|---------|
| {{sourceDomain1}} | {{targetDomain1}} | {{dependencyType1}} | {{dependencyReason1}} | {{interactionMethod1}} |
| {{sourceDomain2}} | {{targetDomain2}} | {{dependencyType2}} | {{dependencyReason2}} | {{interactionMethod2}} |

**依赖类型说明**：
- **强依赖**：源领域必须依赖目标领域才能正常工作
- **弱依赖**：源领域可以独立工作，但依赖目标领域提供增强能力
- **事件依赖**：通过领域事件进行解耦的依赖关系

## 领域交互方式

### 同步调用

| 调用方领域 | 被调用方领域 | 接口类型 | 说明 |
|-----------|------------|---------|------|
| {{caller1}} | {{callee1}} | {{interfaceType1}} | {{description1}} |

### 异步事件

| 发布方领域 | 订阅方领域 | 事件类型 | 说明 |
|-----------|-----------|---------|------|
| {{publisher1}} | {{subscriber1}} | {{eventType1}} | {{description1}} |

> 详细的事件定义请参考各领域的领域模型文档。

## 共享模块

| 模块名称 | 模块标识 | 用途 | 使用领域 | 详细文档 |
|---------|---------|------|---------|---------|
| {{sharedModule1}} | {{sharedModule1Id}} | {{sharedModule1Purpose}} | {{sharedModule1Users}} | [[../02-shared/{{sharedModule1Id}}/01-module-overview.md]] |

> **说明**：共享模块提供跨领域的技术性共享能力，不属于业务领域。业务领域之间的依赖应通过领域接口或领域事件实现。

## 相关文档

- [[02-domain-mapping.md]] - 子领域映射（核心域/支撑域/通用域划分）和上下文映射
- [[03-bounded-context.md]] - 限界上下文定义和边界
- [[04-glossary.md]] - 领域术语表（全局）
- [[../{{domain1Id}}/01-domain-overview.md]] - {{domain1Name}} 领域概览
- [[../{{domain2Id}}/01-domain-overview.md]] - {{domain2Name}} 领域概览
- [[../{{domain3Id}}/01-domain-overview.md]] - {{domain3Name}} 领域概览

## 变更记录

| 日期 | 版本 | 变更内容 | 变更人 |
|------|------|----------|--------|
| {{date}} | 1.0 | 初始版本 | {{architect}} |
