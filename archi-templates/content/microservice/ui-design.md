# {{serviceName}} {{subdomainName}} UI设计

**创建日期**: {{date}}  
**架构师**: {{architect}}  
**版本**: 1.0

## 概述

本文档描述 {{serviceName}} 的 {{subdomainName}} UI设计，包括页面设计、交互流程、组件使用等。

{{subdomainName}} UI是表现层的重要组成部分，负责{{subdomainName}}相关的用户界面展示和交互处理。

## UI架构

### 页面结构

{{subdomainName}}包含以下页面：

1. **{{page1}}**：{{page1Description}}
2. **{{page2}}**：{{page2Description}}
3. **{{page3}}**：{{page3Description}}

### 页面关系

```mermaid
graph TD
    A[{{mainPage}}] --> B[{{subPage1}}]
    A --> C[{{subPage2}}]
    B --> D[{{detailPage}}]
    C --> D
```

## 页面设计

### {{page1}}

**页面描述**：{{page1Description}}

**页面功能**：

- {{function1}}
- {{function2}}
- {{function3}}

**关键交互**：

- **{{interaction1}}**：{{interaction1Description}}
- **{{interaction2}}**：{{interaction2Description}}

**设计要点**：

- {{designPoint1}}
- {{designPoint2}}

### {{page2}}

**页面描述**：{{page2Description}}

**页面功能**：

- {{function1}}
- {{function2}}

**关键交互**：

- **{{interaction1}}**：{{interaction1Description}}

## 组件使用

### 使用的组件

| 组件名称 | 用途 | 位置 |
|---------|------|------|
| {{component1}} | {{component1Usage}} | {{component1Location}} |
| {{component2}} | {{component2Usage}} | {{component2Location}} |

### 自定义组件

{{subdomainName}}自定义的组件：

1. **{{customComponent1}}**：{{customComponent1Description}}
2. **{{customComponent2}}**：{{customComponent2Description}}

## 状态管理

### 页面状态

{{subdomainName}}页面状态包括：

- {{state1}}：{{state1Description}}
- {{state2}}：{{state2Description}}

### 状态Provider

```dart
// 状态Provider示例
final {{subdomainName}}Provider = StateNotifierProvider<{{SubdomainName}}Notifier, {{SubdomainName}}State>(
  (ref) => {{SubdomainName}}Notifier(ref.read({{subdomainName}}ServiceProvider)),
);
```

## 路由配置

### 路由定义

```dart
// 路由配置示例
Route(
  path: '/{{subdomainName}}',
  name: '{{subdomainName}}',
  component: {{SubdomainName}}Page,
  children: [
    Route(
      path: '/list',
      component: {{SubdomainName}}ListPage,
    ),
    Route(
      path: '/:id',
      component: {{SubdomainName}}DetailPage,
    ),
  ],
),
```

## 与应用层集成

### 调用应用服务

{{subdomainName}} UI通过以下方式调用应用服务：

1. **命令处理**：通过命令处理器处理用户操作
2. **查询数据**：通过查询处理器获取数据
3. **状态订阅**：订阅应用层状态变化

## 代码位置

### UI实现

- **页面组件**：`apps/flutter-app/lib/presentation/pages/{{subdomainName}}/`
- **状态管理**：`apps/flutter-app/lib/presentation/state/{{subdomainName}}/`
- **自定义组件**：`apps/flutter-app/lib/presentation/widgets/{{subdomainName}}/`

## 相关文档

- [[../01-presentation-overview.md]] - 表现层概览
- [[../02-routing-design.md]] - 路由设计
- [[../03-state-management-design.md]] - 状态管理设计
- [[../04-ui-components-design.md]] - UI组件设计
- [[../../04-application/{{subdomainName}}/01-application-service.md]] - {{subdomainName}}应用服务设计
- [[../../02-product/ux-design.md]] - 用户体验设计（交互流程参考）

## 变更记录

| 日期 | 版本 | 变更内容 | 变更人 |
|------|------|---------|--------|
| {{date}} | 1.0 | 初始版本 | {{architect}} |

