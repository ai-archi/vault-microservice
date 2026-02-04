# {{subdomainName}} 应用服务

**创建日期**: {{date}}  
**领域专家**: {{domainExpert}}  
**版本**: 1.0

## 概述

本文档描述 {{subdomainName}} 领域的应用服务设计和实现细节，包括具体的服务接口、命令处理、查询处理、DTO 定义和应用用例的完整实现。

> **说明**：
> - 应用层的总体设计原则、职责定位和架构模式请参考 [[01-application-overview.md|应用层概览]]
> - 本文档专注于具体应用服务的实现细节
> - 业务逻辑在领域层（[[../02-domain/01-domain-model.md|领域模型]]），应用层只负责编排和流程控制

## 应用服务清单

| 服务名 | 职责 | 关联用例 | 关联命令 |
|--------|------|---------|---------|
| {{service1}} | {{responsibility1}} | [[../02-domain/02-use-cases.md#UC-001|UC-001]] | {{command1}} |
| {{service2}} | {{responsibility2}} | [[../02-domain/02-use-cases.md#UC-002|UC-002]] | {{command2}} |

## 应用服务详细设计

### {{service1}}

#### 服务概述

**类名**: `{{service1}}`  
**职责**: {{serviceResponsibility1}}  
**关联用例**: [[../02-domain/02-use-cases.md#UC-001|{{useCase1}}]]

#### 处理的命令

| 命令名 | 说明 | 输入 | 输出 |
|--------|------|------|------|
| {{command1}} | {{commandDescription1}} | {{commandInput1}} | {{commandOutput1}} |

#### 命令处理实现

##### 命令 1：{{command1}}

**方法签名**：

```dart
@Transactional()
Future<{{resultDTO1}}> {{methodName1}}({{commandDTO1}} request);
```

**处理流程**：

```
1. 参数验证 (Validation)
   - 检查 {{param1}} 不为空
   - 检查 {{param2}} 格式正确
   
2. 权限检查 (Authorization)
   - 检查用户是否有权限执行此操作
   - 检查资源所有权

3. 加载聚合根 (Load Aggregate)
   - 通过 {{repository}} 加载 {{aggregateRoot}}
   - 处理不存在的情况

4. 执行业务方法 (Execute Business Logic)
   - 调用 {{aggregateRoot}}.{{businessMethod}}()
   - 业务逻辑在聚合根中，应用服务只负责编排

5. 保存聚合根 (Save Aggregate)
   - 通过 {{repository}}.save() 持久化

6. 发布领域事件 (Publish Domain Events)
   - 聚合根产生的领域事件已由应用服务发布

7. 返回结果 (Return Result)
   - 转换为 DTO 并返回
```

**代码示例**：

```dart
@Transactional()
Future<{{resultDTO1}}> {{methodName1}}({{commandDTO1}} request) async {
  // 1. 参数验证
  if (request.{{property}} == null || request.{{property}}.isEmpty) {
    throw ValidationException("{{property}} is required");
  }
  
  // 2. 权限检查
  final user = await currentUserProvider.getCurrentUser();
  if (!user.hasPermission('{{permission}}')) {
    throw UnauthorizedException("Permission denied");
  }
  
  // 3. 加载聚合根
  final aggregate = await {{repository}}.findById(request.{{id}});
  if (aggregate == null) {
    throw {{aggregateNotFoundException}}(request.{{id}});
  }
  
  // 4. 执行业务方法
  aggregate.{{businessMethod}}(
    {{param1}}: request.{{param1}},
    {{param2}}: request.{{param2}},
  );
  
  // 5. 保存聚合根
  await {{repository}}.save(aggregate);
  
  // 6. 发布领域事件
  await eventPublisher.publishAll(aggregate.domainEvents);
  
  // 7. 转换并返回
  return {{resultDTO1}}.fromDomain(aggregate);
}
```

**错误处理**：

| 异常类型 | HTTP 状态 | 错误码 | 原因 |
|---------|---------|--------|------|
| {{exceptionType1}} | {{httpStatus1}} | {{errorCode1}} | {{reason1}} |
| {{exceptionType2}} | {{httpStatus2}} | {{errorCode2}} | {{reason2}} |

**业务规则**：

{{businessRules1}}

#### 查询处理实现

##### 查询 1：{{query1}}

**方法签名**：

```dart
Future<{{queryResultDTO1}}> {{queryMethod1}}({{queryDTO1}} request);
```

**查询流程**：

```
1. 参数验证
2. 权限检查
3. 构建查询
4. 执行查询
5. 转换为 DTO
6. 返回结果
```

**代码示例**：

```dart
Future<{{queryResultDTO1}}> {{queryMethod1}}({{queryDTO1}} request) async {
  // 1. 参数验证
  if (request.{{property}} != null && !{{validator}}.isValid(request.{{property}})) {
    throw ValidationException("Invalid {{property}}");
  }
  
  // 2. 权限检查
  final user = await currentUserProvider.getCurrentUser();
  if (!user.hasPermission('{{readPermission}}')) {
    throw UnauthorizedException("Permission denied");
  }
  
  // 3. 构建查询
  final query = {{queryBuilder}}
    .where('{{field}}', equals: request.{{param}})
    .orderBy('{{sortField}}', descending: request.descending)
    .limit(request.limit)
    .offset(request.offset);
  
  // 4. 执行查询
  final results = await {{repository}}.query(query);
  
  // 5. 转换为 DTO
  final dtos = results.map({{resultDTO}}.fromDomain).toList();
  
  // 6. 返回结果
  return {{queryResultDTO1}}(
    items: dtos,
    totalCount: results.totalCount,
  );
}
```

### {{service2}}

#### 服务概述

...（参考上述结构）

## DTO 定义

### 请求 DTO

#### {{commandDTO1}}

**用途**: {{commandPurpose1}}

**字段定义**：

```dart
class {{commandDTO1}} {
  @NotNull(message: "{{property1}} is required")
  final String {{property1}};
  
  @Email(message: "Invalid email format")
  final String {{property2}};
  
  @Range(min: 0, max: 100, message: "{{property3}} must be between 0 and 100")
  final int {{property3}};
  
  {{commandDTO1}}({
    required this.{{property1}},
    required this.{{property2}},
    required this.{{property3}},
  });
  
  // 工厂方法：从 JSON 反序列化
  factory {{commandDTO1}}.fromJson(Map<String, dynamic> json) {
    return {{commandDTO1}}(
      {{property1}}: json['{{jsonKey1}}'],
      {{property2}}: json['{{jsonKey2}}'],
      {{property3}}: json['{{jsonKey3}}'],
    );
  }
  
  // 序列化为 JSON
  Map<String, dynamic> toJson() {
    return {
      '{{jsonKey1}}': {{property1}},
      '{{jsonKey2}}': {{property2}},
      '{{jsonKey3}}': {{property3}},
    };
  }
}
```

### 响应 DTO

#### {{resultDTO1}}

**用途**: {{resultPurpose1}}

**字段定义**：

```dart
class {{resultDTO1}} {
  final String id;
  final String {{property1}};
  final String status;
  final DateTime createdAt;
  final DateTime updatedAt;
  
  {{resultDTO1}}({
    required this.id,
    required this.{{property1}},
    required this.status,
    required this.createdAt,
    required this.updatedAt,
  });
  
  // 工厂方法：从领域对象转换
  factory {{resultDTO1}}.fromDomain({{domainObject}}) {
    return {{resultDTO1}}(
      id: {{domainObject}}.id.value,
      {{property1}}: {{domainObject}}.{{property1}}.value,
      status: {{domainObject}}.status.name,
      createdAt: {{domainObject}}.createdAt,
      updatedAt: {{domainObject}}.updatedAt,
    );
  }
  
  // 序列化为 JSON
  Map<String, dynamic> toJson() {
    return {
      'id': id,
      '{{jsonKey1}}': {{property1}},
      'status': status,
      'createdAt': createdAt.toIso8601String(),
      'updatedAt': updatedAt.toIso8601String(),
    };
  }
}
```

### 查询 DTO

#### {{queryDTO1}}

**用途**: {{queryPurpose1}}

**字段定义**：

```dart
class {{queryDTO1}} {
  final String? {{filter1}};
  final int page;
  final int pageSize;
  final String? sortBy;
  final bool descending;
  
  {{queryDTO1}}({
    this.{{filter1}},
    this.page = 1,
    this.pageSize = 20,
    this.sortBy,
    this.descending = false,
  }) : assert(page >= 1, 'Page must be >= 1'),
       assert(pageSize > 0 && pageSize <= 100, 'PageSize must be between 1 and 100');
}
```

## 事务管理

### 事务边界

应用服务方法是事务的边界。在此框架中：

```dart
@Transactional()  // 事务自动开始
Future<ResultDTO> execute(CommandDTO request) async {
  // 业务逻辑
  // 事务在方法结束时自动提交或回滚
}
```

### 事务隔离级别

| 操作类型 | 隔离级别 | 说明 |
|---------|---------|------|
| 命令处理 | {{isolationLevel1}} | {{description1}} |
| 查询处理 | {{isolationLevel2}} | {{description2}} |

## 异常处理

### 异常映射

应用层捕获的异常需要映射为 API 错误响应：

| 异常类型 | HTTP 状态 | 错误响应 | 说明 |
|---------|---------|---------|------|
| {{exceptionType1}} | {{httpStatus1}} | {{errorResponse1}} | {{description1}} |
| {{exceptionType2}} | {{httpStatus2}} | {{errorResponse2}} | {{description2}} |

### 异常处理示例

```dart
try {
  return await {{serviceMethod}};
} on ValidationException catch (e) {
  throw ApiException(400, 'VALIDATION_ERROR', e.message);
} on UnauthorizedException catch (e) {
  throw ApiException(401, 'UNAUTHORIZED', 'Access denied');
} on ResourceNotFoundException catch (e) {
  throw ApiException(404, 'NOT_FOUND', 'Resource not found');
} on BusinessRuleViolationException catch (e) {
  throw ApiException(409, 'BUSINESS_RULE_VIOLATION', e.message);
} catch (e) {
  throw ApiException(500, 'INTERNAL_ERROR', 'Internal server error');
}
```

## 依赖与协作

### 依赖的其他应用服务

| 依赖服务 | 用途 | 说明 |
|---------|------|------|
| {{dependentService1}} | {{purpose1}} | {{description1}} |

### 依赖的领域对象

| 领域对象 | 操作 | 说明 |
|---------|------|------|
| {{domainObject1}} | {{operation1}} | {{description1}} |

### 依赖的基础设施组件

| 组件 | 用途 | 说明 |
|------|------|------|
| {{infrastructureComponent1}} | {{purpose1}} | {{description1}} |

## 相关文档

### 领域内文档

- [[01-application-overview.md]] - 应用层概览（设计原则、职责定位）
- [[../02-domain/01-domain-model.md]] - 领域模型（聚合根、领域服务等）
- [[../02-domain/02-use-cases.md]] - 业务用例（应用服务实现的用例）
- [[../04-apis/01-api-design.md]] - API 设计（应用服务的外部接口）

### 系统级文档

- [[../../01-overview/01-domains-overview.md]] - 系统级领域概览

## 变更记录

| 日期 | 版本 | 变更内容 | 变更人 |
|------|------|----------|--------|
| {{date}} | 1.0 | 初始版本 | {{domainExpert}} |
