# {{serviceName}} 性能测试

**创建日期**: {{date}}  
**测试工程师**: {{tester}}  
**版本**: 1.0

## 概述

本文档描述 {{serviceName}} 微服务的性能测试计划和结果。

## 性能测试目标

{{performanceTestObjectives}}

## 性能指标

### 响应时间

| API端点 | P50 | P95 | P99 | 目标值 |
|---------|-----|-----|-----|--------|
| {{endpoint1}} | {{p50_1}} | {{p95_1}} | {{p99_1}} | {{target1}} |
| {{endpoint2}} | {{p50_2}} | {{p95_2}} | {{p99_2}} | {{target2}} |

### 吞吐量

| 场景 | 目标TPS | 实际TPS | 状态 |
|------|---------|---------|------|
| {{scenario1}} | {{targetTps1}} | {{actualTps1}} | {{status1}} |
| {{scenario2}} | {{targetTps2}} | {{actualTps2}} | {{status2}} |

### 资源使用

| 资源类型 | 使用率 | 目标值 | 状态 |
|---------|--------|--------|------|
| CPU | {{cpuUsage}} | {{cpuTarget}} | {{cpuStatus}} |
| 内存 | {{memoryUsage}} | {{memoryTarget}} | {{memoryStatus}} |

## 性能测试场景

### 场景1: {{scenario1}}

#### 场景描述

{{scenarioDescription1}}

#### 测试配置

{{testConfiguration1}}

#### 测试结果

{{testResults1}}

### 场景2: {{scenario2}}

#### 场景描述

{{scenarioDescription2}}

## 压力测试

### 压力测试配置

{{stressTestConfiguration}}

### 压力测试结果

{{stressTestResults}}

## 负载测试

### 负载测试配置

{{loadTestConfiguration}}

### 负载测试结果

{{loadTestResults}}

## 容量规划

### 容量评估

{{capacityAssessment}}

### 扩容建议

{{scalingRecommendations}}

## 性能优化

### 优化措施

{{optimizationMeasures}}

### 优化效果

{{optimizationResults}}

## 相关文档

- [[test-strategy.md]] - 测试策略
- [[../05-operations/sre.md]] - SLA/SLO/SLI设计

## 变更记录

| 日期 | 版本 | 变更内容 | 变更人 |
|------|------|----------|--------|
| {{date}} | 1.0 | 初始版本 | {{tester}} |

