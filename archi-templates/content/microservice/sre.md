# {{serviceName}} SLA/SLO/SLI 设计

**创建日期**: {{date}}  
**SRE工程师**: {{sre}}  
**版本**: 1.0

## 概述

本文档定义 {{serviceName}} 微服务的服务级别协议（SLA）、服务级别目标（SLO）和服务级别指标（SLI）。

## SLA（Service Level Agreement）

### SLA 定义

{{slaDefinition}}

### SLA 承诺

| 指标 | 目标值 | 测量周期 | 描述 |
|------|--------|---------|------|
| {{slaMetric1}} | {{targetValue1}} | {{measurementPeriod1}} | {{description1}} |
| {{slaMetric2}} | {{targetValue2}} | {{measurementPeriod2}} | {{description2}} |

## SLO（Service Level Objective）

### 可用性 SLO

| SLO指标 | 目标值 | 时间窗口 | 描述 |
|---------|--------|---------|------|
| 可用性 | {{availabilityTarget}} | {{timeWindow}} | {{description}} |

### 延迟 SLO

| SLO指标 | 目标值 | 百分位 | 描述 |
|---------|--------|--------|------|
| API响应时间 | {{latencyTarget}} | {{percentile}} | {{description}} |

### 错误率 SLO

| SLO指标 | 目标值 | 时间窗口 | 描述 |
|---------|--------|---------|------|
| 错误率 | {{errorRateTarget}} | {{timeWindow}} | {{description}} |

## SLI（Service Level Indicator）

### 可用性 SLI

#### 指标定义

{{availabilitySliDefinition}}

#### 测量方法

{{availabilityMeasurementMethod}}

#### 计算公式

{{availabilityFormula}}

### 延迟 SLI

#### 指标定义

{{latencySliDefinition}}

#### 测量方法

{{latencyMeasurementMethod}}

#### 计算公式

{{latencyFormula}}

### 错误率 SLI

#### 指标定义

{{errorRateSliDefinition}}

#### 测量方法

{{errorRateMeasurementMethod}}

#### 计算公式

{{errorRateFormula}}

## 错误预算

### 错误预算定义

{{errorBudgetDefinition}}

### 错误预算计算

{{errorBudgetCalculation}}

### 错误预算消耗

{{errorBudgetConsumption}}

## 监控和告警

### SLI 监控

{{sliMonitoring}}

### 告警规则

{{alertRules}}

## 相关文档

- [[observability.md]] - 可观测性文档
- [[runbook.md]] - 故障处理手册
- [[deployment.md]] - 部署架构

## 变更记录

| 日期 | 版本 | 变更内容 | 变更人 |
|------|------|----------|--------|
| {{date}} | 1.0 | 初始版本 | {{sre}} |

