# {{subdomainName}} 应用层

**创建日期**: {{date}}  
**领域专家**: {{domainExpert}}  
**版本**: 1.0

## 概述

本文档描述 {{subdomainName}} 领域的应用层设计，包括应用层概览、设计原则与具体应用服务实现。应用层是业务用例和领域模型之间的协调层，不包含业务逻辑（业务逻辑在领域层 [[02-domain-design.md]]），负责编排、流程控制和技术关切点。

---

# 第一部分：应用层概览

## 应用层定位

### 职责范围

1. **用例编排**：将用户请求转化为对领域服务和聚合根的调用
2. **数据转换**：在 API 层（外部 DTO）和领域模型层（内部对象）之间进行转换
3. **事务管理**：确保领域操作的原子性和一致性
4. **权限检查**：执行授权检查和权限验证
5. **异常处理**：捕获和处理领域异常，转换为 API 响应
6. **跨越聚合根协调**：当业务用例需要多个聚合根参与时进行协调

### 应用层与其他层的关系

```
┌─────────────────────────────────┐
│   表现层/API层（REST、RPC等）   │  ← 外部接口，接收请求、返回响应
├─────────────────────────────────┤
│   应用层（Application Services）│  ← 协调层，编排业务流程
├─────────────────────────────────┤
│   领域层（Domain Model）        │  ← 业务逻辑层
├─────────────────────────────────┤
│   基础设施层（Infrastructure）  │  ← 技术支持层
└─────────────────────────────────┘
```

## 应用层设计原则

### 1. 单一职责原则（SRP）

每个应用服务只负责一个用例的协调。

### 2. 领域模型不渗漏

对外部（表现层）只暴露 DTO，不暴露领域对象。

### 3. 事务边界清晰

应用服务方法是事务的边界，一个方法对应一个完整业务操作。

### 4. 依赖反向

依赖抽象接口（Repository、Service 等），不依赖具体基础设施实现。

### 5. 错误处理明确

捕获领域异常和基础设施异常，转换为适当的响应。

## CQRS 设计（如适用）

### 命令处理流程

```
命令请求 → 1.参数验证 → 2.权限检查 → 3.加载聚合根 → 4.执行业务方法 → 5.保存聚合根 → 6.发布领域事件 → 7.返回结果
```

### 查询处理流程

```
查询请求 → 1.参数验证 → 2.权限检查 → 3.构建查询 → 4.执行查询 → 5.转换为 DTO → 6.返回结果
```

## 应用服务设计

### 应用服务的职责

编排业务流程、处理事务、权限检查、DTO 转换、异常处理。

### 应用服务与领域服务的区别

| 维度     | 应用服务         | 领域服务           |
| -------- | ---------------- | ------------------ |
| 层级     | 应用层           | 领域层             |
| 职责     | 编排、流程、协调 | 业务逻辑、核心概念 |
| 参数     | DTO、命令对象    | 领域对象           |
| 返回值   | DTO              | 领域对象或值对象   |
| 事务管理 | 应用服务管理     | 领域服务不管理     |

## DTO 设计（通用说明）

- **请求 DTO**：对应 API 请求体，含校验注解，无业务逻辑。
- **响应 DTO**：对应 API 响应体，只读字段，通过 fromDomain 从领域对象转换。
- **内部 DTO**：应用层内部服务间传递时使用。

## 错误处理

### 应用层错误处理策略

{{errorHandlingStrategy}}

### 异常映射表

| 领域异常             | HTTP 状态码     | 错误响应码     | 说明             |
| -------------------- | --------------- | -------------- | ---------------- |
| {{domainException1}} | {{httpStatus1}} | {{errorCode1}} | {{description1}} |
| {{domainException2}} | {{httpStatus2}} | {{errorCode2}} | {{description2}} |

## 事务管理

应用服务方法是事务的边界。在 {{frameworkName}} 中：{{transactionManagement}}

## 与领域层的协调

应用服务通过 Repository 加载/保存聚合根，调用聚合根方法执行业务逻辑，调用领域服务处理复杂逻辑，保存后发布领域事件。详见 [[02-domain-design.md]]。

---

# 第二部分：应用服务清单与实现

## 应用服务清单

| 服务名       | 职责                | 关联用例                     | 关联命令 |
| ------------ | ------------------- | ---------------------------- | -------- | ------------ |
| {{service1}} | {{responsibility1}} | [[02-domain-design.md#UC-001 | UC-001]] | {{command1}} |
| {{service2}} | {{responsibility2}} | [[02-domain-design.md#UC-002 | UC-002]] | {{command2}} |

## 应用服务详细设计

### {{service1}}

#### 服务概述

**类名**: `{{service1}}`  
**职责**: {{serviceResponsibility1}}  
**关联用例**: [[02-domain-design.md#UC-001|{{useCase1}}]]

#### 处理的命令

| 命令名       | 说明                    | 输入              | 输出               |
| ------------ | ----------------------- | ----------------- | ------------------ |
| {{command1}} | {{commandDescription1}} | {{commandInput1}} | {{commandOutput1}} |

#### 命令处理实现（命令 1：{{command1}}）

**方法签名**：

```dart
@Transactional()
Future<{{resultDTO1}}> {{methodName1}}({{commandDTO1}} request);
```

**处理流程**：见上文「CQRS 设计 - 命令处理流程」；本命令特有：检查 {{param1}}、{{param2}}，通过 {{repository}} 加载 {{aggregateRoot}}，调用 {{businessMethod}}()，保存并发布事件。

**代码示例**：

```dart
@Transactional()
Future<{{resultDTO1}}> {{methodName1}}({{commandDTO1}} request) async {
  if (request.{{property}} == null || request.{{property}}.isEmpty) {
    throw ValidationException("{{property}} is required");
  }
  final user = await currentUserProvider.getCurrentUser();
  if (!user.hasPermission('{{permission}}')) {
    throw UnauthorizedException("Permission denied");
  }
  final aggregate = await {{repository}}.findById(request.{{id}});
  if (aggregate == null) {
    throw {{aggregateNotFoundException}}(request.{{id}});
  }
  aggregate.{{businessMethod}}({{param1}}: request.{{param1}}, {{param2}}: request.{{param2}});
  await {{repository}}.save(aggregate);
  await eventPublisher.publishAll(aggregate.domainEvents);
  return {{resultDTO1}}.fromDomain(aggregate);
}
```

**错误处理**：

| 异常类型           | HTTP 状态       | 错误码         | 原因        |
| ------------------ | --------------- | -------------- | ----------- |
| {{exceptionType1}} | {{httpStatus1}} | {{errorCode1}} | {{reason1}} |
| {{exceptionType2}} | {{httpStatus2}} | {{errorCode2}} | {{reason2}} |

**业务规则**：{{businessRules1}}

#### 查询处理实现（查询 1：{{query1}}）

**方法签名**：`Future<{{queryResultDTO1}}> {{queryMethod1}}({{queryDTO1}} request);`

**流程**：见上文「查询处理流程」。代码示例略。

### {{service2}}

#### 服务概述

...（参考上述结构）

## 本领域 DTO 定义

### 请求 DTO

#### {{commandDTO1}}

**用途**: {{commandPurpose1}}

**字段**：{{property1}}、{{property2}}、{{property3}}（含校验注解）；fromJson/toJson。

### 响应 DTO

#### {{resultDTO1}}

**用途**: {{resultPurpose1}}

**字段**：id、{{property1}}、status、createdAt、updatedAt；fromDomain、toJson。

### 查询 DTO

#### {{queryDTO1}}

**用途**: {{queryPurpose1}}

**字段**：{{filter1}}、page、pageSize、sortBy、descending。

## 依赖与协作

### 依赖的其他应用服务

| 依赖服务              | 用途         | 说明             |
| --------------------- | ------------ | ---------------- |
| {{dependentService1}} | {{purpose1}} | {{description1}} |

### 依赖的领域对象

| 领域对象          | 操作           | 说明             |
| ----------------- | -------------- | ---------------- |
| {{domainObject1}} | {{operation1}} | {{description1}} |

### 依赖的基础设施组件

| 组件                         | 用途         | 说明             |
| ---------------------------- | ------------ | ---------------- |
| {{infrastructureComponent1}} | {{purpose1}} | {{description1}} |

## 相关文档

- [[01-domain-overview.md]] - 领域概览
- [[02-domain-design.md]] - 领域模型与业务用例
- [[04-domain-api-design.md]] - API 设计

## 变更记录

| 日期     | 版本 | 变更内容 | 变更人           |
| -------- | ---- | -------- | ---------------- |
| {{date}} | 1.0  | 初始版本 | {{domainExpert}} |
