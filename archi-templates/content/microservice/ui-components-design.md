# {{serviceName}} UI 组件设计

**创建日期**: {{date}}  
**架构师**: {{architect}}  
**版本**: 1.0

## 概述

本文档描述 {{serviceName}} 的 UI 组件设计，包括组件库、组件规范、主题管理等。

UI 组件是表现层的基础，提供可复用的 UI 组件，提高开发效率和一致性。

## UI 组件架构

### 组件库

**组件库名称**：{{uiComponentLibrary}}  
**版本**：{{version}}  
**官方文档**：{{officialDoc}}

**选型理由**：

- **{{reason1}}**：{{reason1Description}}
- **{{reason2}}**：{{reason2Description}}
- **{{reason3}}**：{{reason3Description}}

### 组件分类

1. **基础组件**：按钮、输入框、卡片等基础 UI 组件
2. **业务组件**：知识节点卡片、学习路径卡片等业务相关组件
3. **布局组件**：容器、网格、列表等布局组件
4. **导航组件**：导航栏、侧边栏、标签栏等导航组件

## 组件规范

### 组件设计原则

1. **单一职责**：每个组件只负责一个功能
2. **可复用性**：组件应该可复用，支持不同场景
3. **可组合性**：组件应该可组合，支持复杂 UI 构建
4. **可访问性**：组件应该支持无障碍访问

### 组件 API 设计

```dart
// 组件API示例
class KnowledgeNodeCard extends StatelessWidget {
  final KnowledgeNodeDTO node;
  final VoidCallback? onTap;
  final VoidCallback? onEdit;
  final VoidCallback? onDelete;

  const KnowledgeNodeCard({
    required this.node,
    this.onTap,
    this.onEdit,
    this.onDelete,
  });

  @override
  Widget build(BuildContext context) {
    // 组件实现
  }
}
```

## 主题管理

### 主题系统

主题系统包括：

1. **颜色系统**：主色、辅助色、中性色等
2. **字体系统**：字体家族、字体大小、字重等
3. **间距系统**：基础间距单位、间距规范等
4. **圆角系统**：圆角大小规范
5. **阴影系统**：阴影样式规范

### 深色模式支持

支持深色模式：

1. **主题切换**：支持浅色/深色主题切换
2. **自动适配**：根据系统设置自动适配
3. **颜色映射**：浅色/深色颜色映射

## 国际化支持

### 多语言支持

1. **文本国际化**：所有文本支持多语言
2. **RTL 支持**：支持从右到左语言布局
3. **本地化格式**：日期时间、数字格式本地化

## 代码位置

### UI 组件

- **基础组件**：`apps/flutter-app/lib/presentation/widgets/base/`
- **业务组件**：`apps/flutter-app/lib/presentation/widgets/business/`
- **布局组件**：`apps/flutter-app/lib/presentation/widgets/layout/`
- **主题配置**：`apps/flutter-app/lib/presentation/theme/`

## 相关文档

- [[01-presentation-overview.md]] - 表现层概览
- [[../02-product/03-ux-and-metrics.md]] - 用户体验设计（设计规范参考）

## 变更记录

| 日期     | 版本 | 变更内容 | 变更人        |
| -------- | ---- | -------- | ------------- |
| {{date}} | 1.0  | 初始版本 | {{architect}} |
