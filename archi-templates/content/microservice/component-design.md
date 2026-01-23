# {{serviceName}} {{componentName}} 组件设计

**创建日期**: {{date}}  
**架构师**: {{architect}}  
**版本**: 1.0

## 概述

本文档描述 {{serviceName}} 的 {{componentName}} 组件设计，包括组件概述、API设计、使用示例等。

{{componentName}} 组件是表现层的重要组成部分，负责{{componentPurpose}}。

## 组件概述

### 组件用途

{{componentDescription}}

### 组件分类

- **组件类型**：{{componentType}}（基础组件/业务组件/布局组件）
- **组件位置**：`{{componentPath}}`
- **依赖组件**：{{dependencies}}

### 设计原则

1. **单一职责**：{{componentName}} 只负责{{singleResponsibility}}
2. **可复用性**：组件可在{{usageScenarios}}场景下复用
3. **可组合性**：组件可与{{composableComponents}}组合使用
4. **可访问性**：组件支持无障碍访问，符合WCAG标准

## 组件API

### Props/Props

| 属性名 | 类型 | 默认值 | 必填 | 描述 |
|--------|------|--------|------|------|
| {{prop1}} | {{prop1Type}} | {{prop1Default}} | {{prop1Required}} | {{prop1Description}} |
| {{prop2}} | {{prop2Type}} | {{prop2Default}} | {{prop2Required}} | {{prop2Description}} |

### Events

| 事件名 | 参数 | 描述 |
|--------|------|------|
| {{event1}} | {{event1Params}} | {{event1Description}} |
| {{event2}} | {{event2Params}} | {{event2Description}} |

### Slots（如适用）

| Slot名称 | 描述 |
|----------|------|
| {{slot1}} | {{slot1Description}} |
| {{slot2}} | {{slot2Description}} |

## 使用示例

### 基础用法

```{{language}}
// {{componentName}} 基础用法示例
<{{ComponentName}}
  {{prop1}}="{{prop1Value}}"
  {{prop2}}="{{prop2Value}}"
  on{{Event1}}={handle{{Event1}}}
/>
```

### 高级用法

```{{language}}
// {{componentName}} 高级用法示例
<{{ComponentName}}
  {{prop1}}="{{prop1Value}}"
  {{prop2}}="{{prop2Value}}"
  {{prop3}}="{{prop3Value}}"
  on{{Event1}}={handle{{Event1}}}
  on{{Event2}}={handle{{Event2}}}
>
  <{{Slot1}}>{{slot1Content}}</{{Slot1}}>
</{{ComponentName}}>
```

## 样式和主题定制

### 样式变量

| 变量名 | 默认值 | 描述 |
|--------|--------|------|
| {{styleVar1}} | {{styleVar1Default}} | {{styleVar1Description}} |
| {{styleVar2}} | {{styleVar2Default}} | {{styleVar2Description}} |

### 主题定制

{{componentName}} 支持以下主题定制：

- **颜色**：{{colorCustomization}}
- **尺寸**：{{sizeCustomization}}
- **间距**：{{spacingCustomization}}
- **圆角**：{{borderRadiusCustomization}}

## 状态管理

### 组件状态

{{componentName}} 的内部状态包括：

- {{state1}}：{{state1Description}}
- {{state2}}：{{state2Description}}

### 状态更新

组件状态通过以下方式更新：

1. **Props变化**：{{propsUpdateDescription}}
2. **用户交互**：{{interactionUpdateDescription}}
3. **外部事件**：{{externalEventUpdateDescription}}

## 可访问性支持

### ARIA属性

{{componentName}} 支持以下ARIA属性：

- `aria-label`：{{ariaLabelDescription}}
- `aria-describedby`：{{ariaDescribedByDescription}}
- `aria-expanded`：{{ariaExpandedDescription}}（如适用）

### 键盘导航

组件支持以下键盘操作：

- **{{key1}}**：{{key1Action}}
- **{{key2}}**：{{key2Action}}

## 性能优化

### 优化策略

1. **渲染优化**：{{renderingOptimization}}
2. **事件处理优化**：{{eventOptimization}}
3. **内存管理**：{{memoryOptimization}}

## 测试策略

### 单元测试

组件应包含以下单元测试：

- **渲染测试**：验证组件正确渲染
- **Props测试**：验证Props传递和更新
- **事件测试**：验证事件触发和处理
- **状态测试**：验证状态变化

### 集成测试

组件应包含以下集成测试：

- **与其他组件集成**：验证组件组合使用
- **与应用层集成**：验证组件与应用服务交互

## 代码位置

### 组件实现

- **组件文件**：`{{componentFilePath}}`
- **样式文件**：`{{styleFilePath}}`
- **测试文件**：`{{testFilePath}}`

## 相关文档

- [[../overview/01-components-overview.md]] - 组件概览
- [[../overview/04-ui-components-design.md]] - UI组件库设计
- [[../../03-domains/{{domainName}}/application/02-application-services.md]] - 应用服务设计（如适用）

## 变更记录

| 日期 | 版本 | 变更内容 | 变更人 |
|------|------|---------|--------|
| {{date}} | 1.0 | 初始版本 | {{architect}} |
