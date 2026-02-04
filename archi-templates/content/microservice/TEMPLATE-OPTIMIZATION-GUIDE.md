# 模板优化指南：从冗余到清晰的架构文档

**版本**: 1.0  
**日期**: 2026-01-24

## 优化概述

本指南说明微服务知识库模板结构的优化，旨在解决文档间的冗余问题，建立清晰的职责边界，提高文档的可维护性和可用性。

## 核心优化原则

### 1. 单一真实来源（SSOT）

每个概念应该在一个地方定义，其他地方只通过链接引用。

**问题**: 之前领域事件既在 `domain-model.md` 中定义，也在 `use-cases.md` 中重复定义，导致两个地方需要同时修改。

**解决方案**:
- 领域事件定义**唯一来源**：`01-domain-model.md`
- `02-use-cases.md` 中只说明"此用例涉及哪些事件"，通过链接指向 `domain-model.md`
- `04-apis/01-api-design.md` 中也通过链接指向 `domain-model.md`

### 2. 清晰的层级职责

不同层级（系统级 vs 领域级）应该有清晰的职责划分，避免重复。

**问题**:
- 系统级 `domains-overview.md` 和领域级 `domain-overview.md` 都描述"领域交互关系"
- 系统级 `bounded-context.md` 和领域级 `bounded-context.md`（现已删除）重复定义上下文映射

**解决方案**:
- **系统级**：全局视图（所有领域、全局依赖、全局上下文映射）
- **领域级**：本领域视图（本领域职责、本领域依赖、本领域接口）
- 领域级通过链接指向系统级文档

### 3. 信息分层

同一个概念在不同层级可以有不同的详细程度，但要避免内容重复。

**问题**: `01-domain-overview.md` 和 `02-domain-structure.md` 都描述"目录结构"

**解决方案**:
- `01-domain-overview.md` 包含"简要"目录结构（树形图）
- `02-domain-structure.md` **可选**，仅当需要超详细的结构说明时使用
- 两个文件互补而非重复

## 重点优化项

### 优化 1：API 层合并（REST + Event + Contract）

**之前**:
```
04-apis/
├── 01-rest-api.md        # REST API 定义
├── 02-event-api.md       # 事件 API
└── 03-api-contract.md    # API 契约（数据格式、错误码等）
```

**问题**:
- 三个文件职责交叉，都在定义 API
- 用户需要查看三个地方才能理解完整的 API 设计
- REST API、Event API、API Contract 本质上是同一个 API 的不同方面

**优化后**:
```
04-apis/
└── 01-api-design.md      # 统一的 API 设计文档（包含 REST、Event、Contract）
```

**优势**:
- 单一的 API 设计文档
- 用户只需查看一个文件
- 便于维护一致性
- 清晰的结构：API 设计原则 → REST API → 事件 API → 契约规范

### 优化 2：应用层分层

**之前**:
- `01-application-overview.md`：不存在或不清晰
- `02-application-services.md`：内容过大（既包含总体设计也包含具体实现）

**问题**:
- 应用层职责不清晰
- 不知道哪些是总体设计，哪些是具体实现

**优化后**:
- `01-application-overview.md`：应用层总体设计（职责、原则、CQRS 模式、DTO 设计）
- `02-application-services.md`：具体应用服务的实现细节（每个服务的命令、查询、异常处理）

**职责划分**:

| 文件 | 职责 | 内容 |
|------|------|------|
| application-overview.md | 应用层总体设计 | 职责定位、设计原则、CQRS、DTO 总体设计、与领域层协调方式 |
| application-services.md | 具体实现细节 | 每个应用服务、具体命令处理、具体查询处理、具体 DTO、异常处理 |

### 优化 3：删除冗余的领域级 bounded-context.md

**之前**:
- 系统级 `03-domains/01-overview/03-bounded-context.md`：所有上下文映射关系
- 领域级 `03-domains/domain-xxx/02-domain/03-bounded-context.md`：本领域上下文映射（重复）

**问题**:
- 重复定义，不知道哪个是权威版本
- 修改时需要同步两个地方

**优化后**:
- **删除**领域级的 `03-bounded-context.md`
- 所有上下文映射在**系统级**统一管理（SSOT）
- 领域级通过链接指向系统级文档

### 优化 4：标记可选文件

某些文件的重要性不一样，应该明确标记。

**优化示例**:
- `02-domain-structure.md`：标记为**可选**（仅当需要超详细结构说明时使用）
- `02-use-cases.md`：标记为**可选但推荐**（很多领域都需要用例说明）

## 文档之间的链接指导

### SSOT 单一真实来源

**领域事件定义**:
- **权威来源**：`02-domain/01-domain-model.md` 中的"领域事件定义"部分
- **其他地方的引用方式**：
  - `02-domain/02-use-cases.md`：`[[01-domain-model.md#{{eventName}}|{{eventName}}]]`
  - `04-apis/01-api-design.md`：`[[../02-domain/01-domain-model.md#DomainEvents|查看详情]]`
  - 不重复定义，只说明"哪些用例/API 涉及哪些事件"

**API 设计**:
- **权威来源**：`04-apis/01-api-design.md`
- **其他地方的引用**：在 `domain-overview.md` 中链接：`[[../04-apis/01-api-design.md]]`

**上下文映射**:
- **权威来源**：系统级 `01-overview/03-bounded-context.md`
- **领域级引用**：在 `domain-overview.md` 中链接：`[[../../01-overview/03-bounded-context.md]]`

### 文档导航示例

#### 场景 1：用户想了解某个用例

1. 查看 `02-domain/02-use-cases.md` 中的用例详细说明
2. 如果想了解涉及的领域事件，点击链接到 `01-domain-model.md`
3. 如果想了解如何通过 API 触发，参考 `04-apis/01-api-design.md`

#### 场景 2：用户想实现某个 API 端点

1. 查看 `04-apis/01-api-design.md` 中的 API 设计
2. 点击链接到 `03-application/02-application-services.md` 查看应用服务实现
3. 点击链接到 `02-domain/01-domain-model.md` 查看领域模型

#### 场景 3：用户想修改某个领域事件

1. 在 `02-domain/01-domain-model.md` 中修改（SSOT）
2. 其他文档中的链接会自动指向新定义
3. 不需要同时修改 `use-cases.md` 或 `api-design.md`

## 新增模板

### 1. `application-overview.md`

**职责**: 应用层的总体设计和架构模式

**包含内容**:
- 应用层定位
- 应用层与其他层的关系
- 应用层设计原则
- CQRS 模式说明
- DTO 设计规范
- 与领域层的协调方式

**何时使用**:
- 需要理解应用层的整体设计时
- 需要学习应用服务如何协调领域对象时
- 需要了解 DTO 转换的原则时

### 2. `api-design.md`

**职责**: 统一的 API 设计文档

**包含内容**:
- API 设计原则
- REST API 端点定义
- 事件驱动 API 定义
- API 契约规范（数据格式、错误码、版本控制等）

**何时使用**:
- 需要理解完整的 API 设计时
- 需要实现前端或客户端调用时
- 需要定义新的 API 端点时

## 文件结构总结

### 必需文件

| 层级 | 文件 | 职责 |
|------|------|------|
| 系统级 | 01-domains-overview.md | 全局领域划分 |
| 系统级 | 02-subdomain-mapping.md | 子领域类型、上下文映射、基础设施工具 |
| 系统级 | 03-bounded-context.md | 上下文边界、集成策略 |
| 系统级 | 04-glossary.md | 全局术语表 |
| 领域级 | 01-domain-overview.md | 本领域职责、边界、技术栈 |
| 领域级 | 02-domain/01-domain-model.md | 领域模型、聚合、事件定义（SSOT） |
| 领域级 | 03-application/01-application-overview.md | 应用层总体设计 |
| 领域级 | 03-application/02-application-services.md | 应用服务实现细节 |
| 领域级 | 04-apis/01-api-design.md | 统一 API 设计 |

### 可选文件

| 层级 | 文件 | 职责 | 何时使用 |
|------|------|------|---------|
| 领域级 | 02-domain/02-use-cases.md | 业务用例流程 | 需要详细的用例说明时 |
| 领域级 | 01-overview/02-domain-structure.md | 详细目录结构 | 需要超详细结构说明时 |
| 领域级 | 06-presentation | 表现层设计 | 领域有特定 UI 需求时 |

## 迁移指南

如果您有旧的知识库使用了之前的模板结构，以下是迁移步骤：

1. **合并 API 文件**
   - 将 `01-rest-api.md`、`02-event-api.md`、`03-api-contract.md` 的内容合并到 `01-api-design.md`
   - 删除旧文件

2. **重构应用层**
   - 创建 `01-application-overview.md`（如果不存在）
   - 将 `application-services.md` 中的总体设计部分移到 `01-application-overview.md`
   - 更新 `application-services.md` 专注于具体实现细节

3. **删除冗余文件**
   - 删除领域级的 `03-bounded-context.md`（上下文映射统一在系统级）

4. **更新链接**
   - 将所有对旧文件的链接更新为新文件
   - 在用例、API 中使用链接引用事件定义，而非重复定义

5. **标记可选文件**
   - 在你的知识库中标记 `02-domain-structure.md` 为可选
   - 标记 `02-use-cases.md` 为"可选但推荐"

## 常见问题

### Q1：为什么要删除领域级的 bounded-context.md？

**A**: 因为上下文映射是系统级的关系，描述多个领域如何交互。每个领域单独定义上下文映射会导致：
- 信息重复
- 版本不一致（一个地方修改了，另一个忘记修改）
- 不知道哪个是权威版本

系统级的 `03-bounded-context.md` 是单一真实来源，领域级通过链接指向它。

### Q2：API 合并后，如何快速找到某个 API 端点？

**A**: `01-api-design.md` 包含所有 API 的汇总表（REST、Event、Contract），用户可以：
1. 看目录快速定位（REST API 设计、事件驱动 API、契约规范）
2. 通过搜索关键词快速找到
3. 参考 `domain-overview.md` 中的"对外提供的接口"表

### Q3：应用层为什么要分成两个文件？

**A**: 为了区分总体设计和具体实现：
- `01-application-overview.md` 回答"应用层如何设计的"，帮助新人理解架构
- `02-application-services.md` 回答"具体怎么实现的"，帮助开发人员编码

这样可以快速查找信息，而不用在一个大文档中翻找。

### Q4：可选文件要不要创建？

**A**: 这取决于你的领域复杂度：
- **简单领域**：不需要创建可选文件，`01-domain-overview.md` 的简要结构足够
- **复杂领域**：创建 `02-domain-structure.md` 提供详细的结构说明和关系解释

推荐做法是：先不创建，后续如果有需要再补充。

## 总结

通过这些优化，我们实现了：

✅ **信息不重复**：使用 SSOT（单一真实来源）原则  
✅ **职责清晰**：系统级和领域级的边界明确  
✅ **易于维护**：修改信息时知道在哪个文件修改  
✅ **易于导航**：清晰的文档链接结构  
✅ **易于扩展**：新增领域时可以复用模板  

希望这个指南能帮助您更好地使用和维护知识库！
