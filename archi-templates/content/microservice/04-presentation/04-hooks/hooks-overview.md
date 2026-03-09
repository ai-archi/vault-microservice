# {{serviceName}} Hooks 概览

**创建日期**: {{date}}  
**架构师**: {{architect}}  
**版本**: 1.0

## 概述

本文档描述 {{serviceName}} 表现层 Hooks（或 Composables）的分类、设计原则、开发规范以及 Hooks 清单。复杂或跨模块 Hook 可单独建立 `02-use-<name>/01-hook-design.md` 并在此处链接。

## Hooks 分类

- **状态类**：useState、useReducer 封装；业务状态如 useAuth、useWorkspace。
- **副作用类**：数据请求（useQuery、useMutation）、订阅、定时器、事件监听。
- **计算/派生类**：从状态或路由派生的派生数据（如 useMemo 封装、usePagination）。
- **DOM/ ref 类**：useRef、点击外部关闭、尺寸监听等。

## 设计原则

1. **单一职责**：每个 Hook 只做一件事，便于测试与复用。
2. **依赖明确**：参数与返回值类型清晰；依赖数组正确，避免闭包陈旧值。
3. **可组合**：Hook 之间可组合，不重复请求或重复状态。
4. **性能**：避免不必要的重算与副作用；大列表/复杂计算考虑 memo、懒加载。

## 开发规范

- 命名：`useXxx`（React）或项目约定的 Composable 命名。
- 文档：参数、返回值、使用场景与注意事项在代码注释或本文「Hooks 清单」中说明。
- 测试：核心 Hook 需单元测试（含 mock 依赖）；与 UI 强耦合的可通过集成测试覆盖。

## Hooks 清单

| Hook 名称      | 职责/场景                     | 依赖/说明           | 详细设计（按需） |
| -------------- | ----------------------------- | ------------------- | ---------------- |
| {{hook1}}      | {{hook1Description}}          | {{hook1Deps}}       | 可选 [[02-use-{{hook1Slug}}/01-hook-design.md]] |
| {{hook2}}      | {{hook2Description}}          | {{hook2Deps}}       | 可选             |
| （按实际补充） | …                             | …                   | …                |

说明：仅对逻辑复杂、跨模块或多端复用的 Hook 单独编写 02-use-xxx/01-hook-design.md。

## 相关文档

- [[../../01-overview/01-presentation-overview.md]] - 表现层概览（含状态管理章节）
- [[../../02-components/01-overview/01-components-overview.md]] - 组件概览

## 变更记录

| 日期     | 版本 | 变更内容 | 变更人        |
| -------- | ---- | -------- | ------------- |
| {{date}} | 1.0  | 初始版本 | {{architect}} |
