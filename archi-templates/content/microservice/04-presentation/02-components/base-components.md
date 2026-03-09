# {{serviceName}} 基础组件设计

**创建日期**: {{date}}  
**架构师**: {{architect}}  
**版本**: 1.0

## 概述

本文档描述 {{serviceName}} 表现层**基础组件**的设计，包括 Button、Input、Table 及 Modal/Dropdown/Tooltip 等通用组件的 API 要点、使用示例与样式定制。同一文档内按组件分节，便于维护与查阅。

## Button（按钮）

### 用途与分类

- 主要按钮、次要按钮、文字按钮、图标按钮等；用于提交、取消、链接等操作。
- 组件位置：`{{baseComponentsPath}}/button`（或等价路径）。

### API 要点

| 属性/事件   | 类型     | 说明 |
| ----------- | -------- | ---- |
| variant     | string   | primary / secondary / outline / ghost / link |
| size        | string   | sm / md / lg |
| disabled    | boolean  | 是否禁用 |
| loading     | boolean  | 是否加载中 |
| onClick     | function | 点击回调 |

### 使用示例

```{{language}}
<Button variant="primary" size="md" onClick={handleSubmit}>提交</Button>
<Button variant="outline" disabled>禁用</Button>
```

### 样式与主题

- 通过设计令牌（颜色、圆角、内边距）定制；支持主题切换。

---

## Input（输入框）

### 用途与分类

- 单行文本、多行、密码、数字、搜索等；可带前缀/后缀、校验与错误提示。
- 组件位置：`{{baseComponentsPath}}/input`。

### API 要点

| 属性/事件   | 类型     | 说明 |
| ----------- | -------- | ---- |
| type        | string   | text / password / number / search 等 |
| value       | string   | 受控值 |
| placeholder | string   | 占位文案 |
| disabled    | boolean  | 是否禁用 |
| error       | string   | 错误信息展示 |
| onChange    | function | 值变化回调 |

### 使用示例

```{{language}}
<Input type="text" placeholder="请输入" value={value} onChange={setValue} />
<Input type="password" error={errors.password} />
```

### 样式与主题

- 边框、焦点态、错误态使用主题变量；支持无障碍（aria-label、aria-invalid）。

---

## Table（表格）

### 用途与分类

- 数据列表展示、排序、分页、选择等；可配置列定义与行操作。
- 组件位置：`{{baseComponentsPath}}/table`。

### API 要点

| 属性/事件   | 类型     | 说明 |
| ----------- | -------- | ---- |
| columns     | array    | 列定义（key、title、render、width、sortable 等） |
| dataSource  | array    | 数据源 |
| rowKey      | string   | 行唯一键字段名 |
| pagination  | object   | 分页配置（current、pageSize、total、onChange） |
| onRow       | function | 行事件（click、selection 等） |

### 使用示例

```{{language}}
<Table columns={columns} dataSource={data} rowKey="id" pagination={{ current: 1, pageSize: 10, total: 100 }} />
```

### 样式与主题

- 表头、斑马纹、边框、悬停态使用主题变量。

---

## 其他基础组件（Modal / Dropdown / Tooltip 等）

### 说明

- **Modal**：对话框，支持标题、内容、底部按钮、关闭与遮罩；API 含 visible、onClose、footer 等。
- **Dropdown**：下拉菜单，触发方式（click/hover）、菜单项与事件；与 Popover 可复用同一基础。
- **Tooltip**：气泡提示，placement、content、trigger；可访问性需支持键盘与 aria 描述。

可根据实际技术栈（如 shadcn/ui、Ant Design、自定义）在本文档中增删具体组件小节，保持「用途 → API 要点 → 示例 → 样式」结构。

## 代码位置

- **基础组件实现**：`{{baseComponentsPath}}`
- **样式/主题**：`{{themePath}}`

## 相关文档

- [[01-overview/01-components-overview.md]] - 组件概览
- [[../01-overview/01-presentation-overview.md]] - 表现层概览

## 变更记录

| 日期     | 版本 | 变更内容 | 变更人        |
| -------- | ---- | -------- | ------------- |
| {{date}} | 1.0  | 初始版本 | {{architect}} |
