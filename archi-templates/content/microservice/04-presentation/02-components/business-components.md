# {{serviceName}} 业务组件设计

**创建日期**: {{date}}  
**架构师**: {{architect}}  
**版本**: 1.0

## 概述

本文档描述 {{serviceName}} 表现层**业务组件**的设计，将订单卡片、用户头像等业务相关组件在同一文档内按组件分节描述，包含 API、业务逻辑约定与使用示例。

## 组件清单

| 组件名称       | 用途说明                     | 所在模块/路由 |
| -------------- | ---------------------------- | ------------- |
| {{component1}} | {{component1Description}}     | {{component1Module}} |
| {{component2}} | {{component2Description}}     | {{component2Module}} |
| （按需补充）   | …                            | …             |

## {{component1}}（示例：订单卡片）

### 用途与业务逻辑

- {{component1Description}}
- 依赖数据：{{component1Data}}；与应用层交互方式：{{component1Integration}}。

### API 要点

| 属性/事件 | 类型     | 说明 |
| --------- | -------- | ---- |
| {{prop1}} | {{type1}}| {{description1}} |
| onAction  | function | 主要操作回调（如查看详情、编辑） |

### 使用示例

```{{language}}
<{{Component1}} {{prop1}}={data} onAction={handleAction} />
```

---

## {{component2}}（示例：用户头像）

### 用途与业务逻辑

- {{component2Description}}
- 支持头像 URL、占位图、尺寸与点击跳转等。

### API 要点

| 属性/事件 | 类型     | 说明 |
| --------- | -------- | ---- |
| src       | string   | 头像地址 |
| alt       | string   | 替代文本 |
| size      | string   | sm / md / lg |
| onClick   | function | 可选点击回调 |

### 使用示例

```{{language}}
<UserAvatar src={user.avatar} alt={user.name} size="md" />
```

---

## 其他业务组件

根据项目实际增加更多业务组件小节，保持「用途与业务逻辑 → API 要点 → 使用示例」结构。复杂业务组件可单独拆出子文档并在此处链接。

## 代码位置

- **业务组件实现**：`{{businessComponentsPath}}`

## 相关文档

- [[01-overview/01-components-overview.md]] - 组件概览
- [[../01-overview/01-presentation-overview.md]] - 表现层概览

## 变更记录

| 日期     | 版本 | 变更内容 | 变更人        |
| -------- | ---- | -------- | ------------- |
| {{date}} | 1.0  | 初始版本 | {{architect}} |
