# {{serviceName}} 部署架构

**创建日期**: {{date}}  
**运维工程师**: {{sre}}  
**版本**: 1.0

## 概述

本文档描述 {{serviceName}} 微服务的部署架构，包括 Kubernetes 和 Service Mesh 配置。

## 部署环境

### 环境列表

| 环境名称 | 用途 | 访问地址 | 描述 |
|---------|------|---------|------|
| {{environment1}} | {{purpose1}} | {{accessUrl1}} | {{description1}} |
| {{environment2}} | {{purpose2}} | {{accessUrl2}} | {{description2}} |

## Kubernetes 部署

### 部署架构图

```mermaid
graph TB
    subgraph "Kubernetes Cluster"
        subgraph "Namespace: {{namespace}}"
            A[Deployment: {{serviceName}}]
            B[Service: {{serviceName}}]
            C[ConfigMap]
            D[Secret]
            E[Ingress]
        end
        F[(数据库)]
        G[消息队列]
    end
    
    A --> B
    A --> C
    A --> D
    E --> B
    A --> F
    A --> G
```

### Deployment 配置

{{deploymentConfig}}

### Service 配置

{{serviceConfig}}

### ConfigMap 配置

{{configMapConfig}}

### Secret 配置

{{secretConfig}}

### Ingress 配置

{{ingressConfig}}

## Service Mesh 配置

### Mesh 架构

```mermaid
graph LR
    A[客户端] --> B[Istio Gateway]
    B --> C[VirtualService]
    C --> D[DestinationRule]
    D --> E[{{serviceName}} Pod]
    E --> F[Sidecar Proxy]
```

### VirtualService

{{virtualServiceConfig}}

### DestinationRule

{{destinationRuleConfig}}

### ServiceEntry

{{serviceEntryConfig}}

## 资源配额

### CPU 和内存

| 环境 | CPU请求 | CPU限制 | 内存请求 | 内存限制 |
|------|---------|---------|---------|---------|
| {{environment1}} | {{cpuRequest1}} | {{cpuLimit1}} | {{memoryRequest1}} | {{memoryLimit1}} |
| {{environment2}} | {{cpuRequest2}} | {{cpuLimit2}} | {{memoryRequest2}} | {{memoryLimit2}} |

### 存储

{{storageQuota}}

## 扩缩容策略

### 水平扩缩容（HPA）

{{hpaConfig}}

### 垂直扩缩容（VPA）

{{vpaConfig}}

## 健康检查

### Liveness Probe

{{livenessProbe}}

### Readiness Probe

{{readinessProbe}}

## 网络策略

{{networkPolicy}}

## 安全策略

### Pod Security Policy

{{podSecurityPolicy}}

### Network Policy

{{networkPolicy}}

## 监控和日志

### 监控配置

{{monitoringConfig}}

### 日志配置

{{loggingConfig}}

## 相关文档

- [[runbook.md]] - 故障处理手册
- [[observability.md]] - 可观测性文档
- [[../08-delivery/cd.md]] - CD发布文档

## 变更记录

| 日期 | 版本 | 变更内容 | 变更人 |
|------|------|----------|--------|
| {{date}} | 1.0 | 初始版本 | {{sre}} |

