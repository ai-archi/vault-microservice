# {{serviceName}} 可观测性

**创建日期**: {{date}}  
**SRE工程师**: {{sre}}  
**版本**: 1.0

## 概述

本文档描述 {{serviceName}} 微服务的可观测性设计，包括 Metrics（指标）、Logs（日志）和 Tracing（追踪）。

## Metrics（指标）

### 业务指标

| 指标名称 | 类型 | 描述 | 标签 |
|---------|------|------|------|
| {{businessMetric1}} | {{metricType1}} | {{description1}} | {{labels1}} |
| {{businessMetric2}} | {{metricType2}} | {{description2}} | {{labels2}} |

### 技术指标

| 指标名称 | 类型 | 描述 | 标签 |
|---------|------|------|------|
| {{technicalMetric1}} | {{metricType1}} | {{description1}} | {{labels1}} |
| {{technicalMetric2}} | {{metricType2}} | {{description2}} | {{labels2}} |

### 指标采集

{{metricsCollection}}

### 指标存储

{{metricsStorage}}

### 指标可视化

{{metricsVisualization}}

## Logs（日志）

### 日志级别

| 级别 | 使用场景 | 示例 |
|------|---------|------|
| ERROR | {{errorScenario}} | {{errorExample}} |
| WARN | {{warnScenario}} | {{warnExample}} |
| INFO | {{infoScenario}} | {{infoExample}} |
| DEBUG | {{debugScenario}} | {{debugExample}} |

### 日志格式

{{logFormat}}

### 日志字段

| 字段名 | 类型 | 描述 | 必填 |
|--------|------|------|------|
| {{logField1}} | {{fieldType1}} | {{description1}} | {{required1}} |
| {{logField2}} | {{fieldType2}} | {{description2}} | {{required2}} |

### 日志采集

{{logCollection}}

### 日志存储

{{logStorage}}

### 日志查询

{{logQuery}}

## Tracing（追踪）

### 追踪架构

```mermaid
graph LR
    A[客户端] --> B[{{serviceName}}]
    B --> C[下游服务1]
    B --> D[下游服务2]
    B --> E[数据库]
```

### 追踪上下文

{{tracingContext}}

### 追踪采样

{{tracingSampling}}

### 追踪存储

{{tracingStorage}}

### 追踪可视化

{{tracingVisualization}}

## 可观测性工具

### Metrics 工具

{{metricsTools}}

### Logs 工具

{{logsTools}}

### Tracing 工具

{{tracingTools}}

## 可观测性最佳实践

{{observabilityBestPractices}}

## 相关文档

- [[sre.md]] - SLA/SLO/SLI设计
- [[runbook.md]] - 故障处理手册
- [[deployment.md]] - 部署架构

## 变更记录

| 日期 | 版本 | 变更内容 | 变更人 |
|------|------|----------|--------|
| {{date}} | 1.0 | 初始版本 | {{sre}} |

