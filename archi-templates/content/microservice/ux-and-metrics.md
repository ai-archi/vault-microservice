# {{serviceName}} 用户体验设计与产品指标

**创建日期**: {{date}}  
**产品经理/UX 设计师**: {{designer}}  
**版本**: {{version}}

## 文档说明

本文档包含**用户体验设计**与**产品指标与埋点**两部分。产品愿景与成功标准见 [[../01-overview/01-service-overview.md]]，需求与功能见 [[01-prd.md]]、[[02-features.md]]。

---

# 第一部分：用户体验设计

## 设计原则

{{designPrinciples}}

## 用户角色

| 角色      | 描述             | 核心需求  |
| --------- | ---------------- | --------- |
| {{role1}} | {{description1}} | {{need1}} |
| {{role2}} | {{description2}} | {{need2}} |

## 信息架构

### 信息架构图

```mermaid
graph TD
    A[{{mainSection1}}] --> B[{{subsection1}}]
    A --> C[{{subsection2}}]
    D[{{mainSection2}}] --> E[{{subsection3}}]
    D --> F[{{subsection4}}]
```

### 导航结构

{{navigationStructure}}

## 交互流程

### 核心流程 1: {{flowName1}}

**流程描述**: {{flowDescription}}

**交互流程**:

```mermaid
flowchart TD
    A[{{step1}}] --> B{{{decision1}}}
    B -->|{{option1}}| C[{{step2}}]
    B -->|{{option2}}| D[{{step3}}]
    C --> E[{{step4}}]
    D --> E
```

**交互说明**:

- {{interaction1}}
- {{interaction2}}

### 核心流程 2: {{flowName2}}

{{flowDescription2}}

## 界面原型

### 页面 1: {{pageName1}}

**页面描述**: {{pageDescription}}

**页面功能**:

- {{function1}}
- {{function2}}

**原型链接**: {{prototypeLink}}

**关键交互**:

- {{interaction1}}
- {{interaction2}}

### 页面 2: {{pageName2}}

{{pageDescription2}}

## 设计规范

### 视觉设计

{{visualDesign}}

### 交互规范

{{interactionGuidelines}}

### 响应式设计

{{responsiveDesign}}

## 可用性测试

### 测试目标

{{testObjectives}}

### 测试结果

| 测试项        | 结果        | 改进建议        |
| ------------- | ----------- | --------------- |
| {{testItem1}} | {{result1}} | {{suggestion1}} |
| {{testItem2}} | {{result2}} | {{suggestion2}} |

## 无障碍设计

{{accessibilityDesign}}

---

# 第二部分：产品指标与埋点

## 关键指标（KPI）

### 核心指标

| 指标名称    | 指标定义        | 目标值      | 当前值       | 计算方式         |
| ----------- | --------------- | ----------- | ------------ | ---------------- |
| {{metric1}} | {{definition1}} | {{target1}} | {{current1}} | {{calculation1}} |
| {{metric2}} | {{definition2}} | {{target2}} | {{current2}} | {{calculation2}} |

### 北极星指标

{{northStarMetric}}

**定义**: {{northStarDefinition}}

**目标值**: {{northStarTarget}}

**当前值**: {{northStarCurrent}}

## 指标分类

### 用户指标

| 指标             | 定义                    | 目标值              |
| ---------------- | ----------------------- | ------------------- |
| DAU (日活跃用户) | {{dauDefinition}}       | {{dauTarget}}       |
| MAU (月活跃用户) | {{mauDefinition}}       | {{mauTarget}}       |
| 用户留存率       | {{retentionDefinition}} | {{retentionTarget}} |
| 用户增长率       | {{growthDefinition}}    | {{growthTarget}}    |

### 业务指标

| 指标                | 定义            | 目标值      |
| ------------------- | --------------- | ----------- |
| {{businessMetric1}} | {{definition1}} | {{target1}} |
| {{businessMetric2}} | {{definition2}} | {{target2}} |

### 功能指标

| 功能         | 指标        | 目标值      |
| ------------ | ----------- | ----------- |
| {{feature1}} | {{metric1}} | {{target1}} |
| {{feature2}} | {{metric2}} | {{target2}} |

## 数据埋点

### 埋点列表

| 事件 ID   | 事件名称       | 事件类型       | 触发时机     | 事件属性        |
| --------- | -------------- | -------------- | ------------ | --------------- |
| EVENT-001 | {{eventName1}} | {{eventType1}} | {{trigger1}} | {{properties1}} |
| EVENT-002 | {{eventName2}} | {{eventType2}} | {{trigger2}} | {{properties2}} |

### 埋点详细说明

#### EVENT-001: {{eventName}}

**事件描述**: {{eventDescription}}

**触发时机**: {{trigger}}

**事件属性**:

- {{property1}}: {{propertyDescription1}}
- {{property2}}: {{propertyDescription2}}

**业务价值**: {{businessValue}}

## 数据分析维度

### 用户维度

{{userDimensions}}

### 时间维度

{{timeDimensions}}

### 功能维度

{{featureDimensions}}

## 数据看板

{{dashboardDescription}}

## 指标监控

### 监控频率

{{monitoringFrequency}}

### 告警规则

| 指标        | 告警阈值       | 告警级别   |
| ----------- | -------------- | ---------- |
| {{metric1}} | {{threshold1}} | {{level1}} |
| {{metric2}} | {{threshold2}} | {{level2}} |

---

## 相关文档

- [[../01-overview/01-service-overview.md]] - 服务概览（产品定位与目标用户）
- [[01-prd.md]] - 产品需求与路线图
- [[02-features.md]] - 功能规格说明

## 变更记录

| 日期     | 版本        | 变更内容 | 变更人       |
| -------- | ----------- | -------- | ------------ |
| {{date}} | {{version}} | 初始版本 | {{designer}} |
