# {{serviceName}} 布局组件设计

**创建日期**: {{date}}  
**架构师**: {{architect}}  
**版本**: 1.0

## 概述

本文档描述 {{serviceName}} 表现层**布局组件**的设计，将 Header、Sidebar、Container 及 Footer、Breadcrumb、Tabs 等布局相关组件在同一文档内按组件分节，包含 API、布局规则与使用示例。

## 组件清单

| 组件名称   | 用途说明                 |
| ---------- | ------------------------ |
| Header     | 顶栏：Logo、导航、用户区 |
| Sidebar    | 侧边栏：菜单、折叠       |
| Container  | 页面容器：最大宽度、内边距 |
| （按需）   | Footer、Breadcrumb、Tabs 等 |

## Header（头部）

### 用途与布局规则

- 固定或随滚动；通常包含 Logo、主导航、搜索、通知、用户菜单。
- 响应式：移动端可收起到抽屉或底部 Tab。

### API 要点

| 属性/事件   | 类型     | 说明 |
| ----------- | -------- | ---- |
| title       | string   | 标题/Logo 文案 |
| navItems    | array    | 导航项配置 |
| rightSlot   | node     | 右侧插槽（用户菜单、操作按钮等） |
| sticky      | boolean  | 是否吸顶 |

### 使用示例

```{{language}}
<Header title="产品名" navItems={navItems} rightSlot={<UserMenu />} sticky />
```

---

## Sidebar（侧边栏）

### 用途与布局规则

- 主导航或二级导航；可折叠（图标模式）与展开；与主内容区通过栅格或 Flex 排版。
- 移动端可 overlay 或抽屉形式。

### API 要点

| 属性/事件   | 类型     | 说明 |
| ----------- | -------- | ---- |
| menuItems  | array    | 菜单项（key、label、icon、path、children） |
| collapsed   | boolean  | 是否折叠 |
| onCollapse  | function | 折叠切换回调 |

### 使用示例

```{{language}}
<Sidebar menuItems={menuItems} collapsed={collapsed} onCollapse={toggleCollapse} />
```

---

## Container（容器）

### 用途与布局规则

- 页面主内容区域；约束最大宽度、水平居中、统一内边距；可配合 Grid/Stack 做内部排版。

### API 要点

| 属性/事件   | 类型     | 说明 |
| ----------- | -------- | ---- |
| maxWidth    | string   | 如 'xl' / '2xl' / 具体像素 |
| padding     | string   | 内边距（或使用主题 token） |
| children    | node     | 子内容 |

### 使用示例

```{{language}}
<Container maxWidth="xl" padding="md">
  {children}
</Container>
```

---

## 其他布局组件（Footer / Breadcrumb / Tabs）

- **Footer**：页脚信息、链接；API 含 links、copyright 等。
- **Breadcrumb**：面包屑；items 数组，支持点击与当前项高亮。
- **Tabs**：标签页；tabs 配置、activeKey、onChange；与路由可联动。

可根据项目实际增删小节，保持「用途与布局规则 → API 要点 → 使用示例」结构。

## 代码位置

- **布局组件实现**：`{{layoutComponentsPath}}`

## 相关文档

- [[01-overview/01-components-overview.md]] - 组件概览
- [[../01-overview/01-presentation-overview.md]] - 表现层概览

## 变更记录

| 日期     | 版本 | 变更内容 | 变更人        |
| -------- | ---- | -------- | ------------- |
| {{date}} | 1.0  | 初始版本 | {{architect}} |
