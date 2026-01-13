# {{serviceName}} 数据访问抽象设计

**创建日期**: {{date}}  
**架构师**: {{architect}}  
**版本**: 1.0

## 概述

本文档描述 {{serviceName}} 微服务的数据访问抽象设计，包括 Repository 模式抽象接口、查询抽象、事务抽象等。

数据访问抽象属于**基础设施层抽象**，提供通用的数据访问抽象接口，支持 Repository 模式，实现领域层与基础设施层的解耦。数据访问抽象不包含业务逻辑，是纯粹的技术抽象，可以被多个业务领域复用。

**职责划分**：

- **数据访问抽象**：仅提供通用抽象接口（IRepository<T>、IQueryBuilder<T>、ITransactionManager），属于基础设施层抽象
- **具体业务域 Repository 接口**：定义在各业务域的领域模型文档中，属于领域层
- **Repository 实现**：在基础设施层实现领域层定义的具体 Repository 接口

## 数据访问抽象定义

### 架构定位

数据访问抽象属于**基础设施层抽象**，提供通用的数据访问抽象接口，实现领域层与基础设施层的解耦。

**重要说明**：

- 数据访问抽象**仅提供通用抽象接口**，不定义具体业务域的 Repository 接口
- 具体业务域的 Repository 接口（如 `I{{AggregateRoot1}}Repository`）定义在各自的领域模型文档中，属于领域层
- 具体 Repository 接口可能继承或使用通用抽象接口（IRepository<T>）

### 设计原则

数据访问抽象遵循以下设计原则：

- **依赖倒置**：领域层定义具体业务域 Repository 接口，基础设施层实现接口；通用抽象接口定义在基础设施层
- **接口隔离**：每个聚合根有独立的 Repository 接口
- **可替换性**：实现可以被替换，不影响业务逻辑
- **技术导向**：纯粹的技术抽象，不包含业务逻辑

### 职责边界

**边界内**：

- Repository 接口定义（通用抽象接口）
- 查询抽象定义（查询构建器、查询条件）
- 事务抽象定义（事务管理接口）
- 数据访问模式定义（Repository 模式、Unit of Work 模式）

**边界外**：

- 具体 Repository 接口定义（由各业务域的领域模型文档定义）
- 具体数据存储实现（SQLite、内存数据库等）
- 领域模型（由业务上下文定义）

## Repository 模式

### 模式概述

Repository 模式是一种数据访问抽象模式，将数据访问逻辑封装在 Repository 接口中，实现领域层与基础设施层的解耦。

### 通用抽象接口

#### IRepository<T>

通用 Repository 基接口，提供基本的 CRUD 操作：

```dart
/// 通用 Repository 接口
///
/// T: 聚合根类型
abstract class IRepository<T> {
  /// 根据ID查找聚合根
  Future<T?> findById(String id);

  /// 保存聚合根
  Future<void> save(T aggregate);

  /// 删除聚合根
  Future<void> delete(String id);

  /// 查找所有聚合根
  Future<List<T>> findAll();

  /// 检查聚合根是否存在
  Future<bool> exists(String id);
}
```

#### 接口方法说明

| 方法名称 | 参数        | 返回值          | 描述                                | 异常                |
| -------- | ----------- | --------------- | ----------------------------------- | ------------------- |
| findById | String id   | Future<T?>      | 根据 ID 查找聚合根，不存在返回 null | DataAccessException |
| save     | T aggregate | Future<void>    | 保存聚合根（新增或更新）            | DataAccessException |
| delete   | String id   | Future<void>    | 删除聚合根                          | DataAccessException |
| findAll  | void        | Future<List<T>> | 查找所有聚合根                      | DataAccessException |
| exists   | String id   | Future<bool>    | 检查聚合根是否存在                  | DataAccessException |

### 接口契约

#### 前置条件

- findById: id 不能为空
- save: aggregate 不能为空，且必须通过聚合根的业务规则验证
- delete: id 不能为空
- exists: id 不能为空

#### 后置条件

- findById: 如果聚合根存在，返回聚合根；否则返回 null
- save: 聚合根已持久化，且状态一致
- delete: 聚合根已从持久化存储中删除
- findAll: 返回所有聚合根列表
- exists: 返回聚合根是否存在

#### 不变式

- 所有方法执行后，聚合根的一致性边界保持不变
- 聚合根的状态变化必须通过聚合根的方法进行
- 保存操作必须保证聚合根内部实体的完整性

## 查询抽象

### 查询构建器

查询构建器提供类型安全的查询条件构建能力：

```dart
/// 查询构建器接口
abstract class IQueryBuilder<T> {
  /// 添加等于条件
  IQueryBuilder<T> whereEquals(String field, dynamic value);

  /// 添加不等于条件
  IQueryBuilder<T> whereNotEquals(String field, dynamic value);

  /// 添加大于条件
  IQueryBuilder<T> whereGreaterThan(String field, dynamic value);

  /// 添加小于条件
  IQueryBuilder<T> whereLessThan(String field, dynamic value);

  /// 添加范围条件
  IQueryBuilder<T> whereBetween(String field, dynamic min, dynamic max);

  /// 添加包含条件
  IQueryBuilder<T> whereIn(String field, List<dynamic> values);

  /// 添加模糊查询条件
  IQueryBuilder<T> whereLike(String field, String pattern);

  /// 添加排序
  IQueryBuilder<T> orderBy(String field, {bool ascending = true});

  /// 添加分页
  IQueryBuilder<T> limit(int count);
  IQueryBuilder<T> offset(int count);

  /// 执行查询
  Future<List<T>> execute();
}
```

### 查询条件抽象

查询条件提供查询条件的抽象表示：

```dart
/// 查询条件接口
abstract class IQueryCondition {
  /// 查询条件类型
  QueryConditionType get type;

  /// 字段名
  String get field;

  /// 条件值
  dynamic get value;
}

/// 查询条件类型
enum QueryConditionType {
  equals,
  notEquals,
  greaterThan,
  lessThan,
  between,
  inList,
  like,
}
```

## 事务抽象

### 事务管理接口

事务管理接口提供事务的创建、提交和回滚能力：

```dart
/// 事务管理接口
abstract class ITransactionManager {
  /// 开始事务
  Future<ITransaction> beginTransaction();

  /// 执行事务
  Future<T> executeInTransaction<T>(Future<T> Function(ITransaction) action);
}

/// 事务接口
abstract class ITransaction {
  /// 提交事务
  Future<void> commit();

  /// 回滚事务
  Future<void> rollback();

  /// 检查事务是否活跃
  bool get isActive;
}
```

### 事务使用模式

**模式 1：显式事务管理**

```dart
final transaction = await transactionManager.beginTransaction();
try {
  await repository1.save(entity1);
  await repository2.save(entity2);
  await transaction.commit();
} catch (e) {
  await transaction.rollback();
  rethrow;
}
```

**模式 2：自动事务管理**

```dart
await transactionManager.executeInTransaction((transaction) async {
  await repository1.save(entity1);
  await repository2.save(entity2);
});
```

## 接口定义位置

### 业务域 Repository 接口

**重要**：具体业务域的 Repository 接口**不属于数据访问抽象**，它们定义在各自的领域模型文档中，属于领域层。

各业务域的 Repository 接口定义位置：

- **{{coreDomain1}}域**：`I{{AggregateRoot1}}Repository`（见 `core-domain-{{coreDomain1}}/01-domain-model.md`）
- **{{coreDomain2}}域**：`I{{AggregateRoot2}}Repository`（见 `core-domain-{{coreDomain2}}/01-domain-model.md`）
- **其他业务域**：各自的领域模型文档中

**职责说明**：

- 具体业务域 Repository 接口定义在领域层，使用领域模型（聚合根）作为参数和返回值
- 具体 Repository 接口可能继承或使用通用抽象接口（IRepository<T>）
- 具体 Repository 接口定义具体的业务查询方法（如 `findByName`、`findByStatus` 等）

### 通用抽象接口

通用抽象接口（如 `IRepository<T>`、`IQueryBuilder<T>`、`ITransactionManager`）的定义位置：

- **代码位置**：`apps/flutter-app/lib/infrastructure/data/interfaces/`
- **文档位置**：本文档（`infrastructure/data-access/01-data-access-abstraction.md`）

## 基础设施实现

### Repository 实现

Repository 实现位于基础设施层：

- **代码位置**：`apps/flutter-app/lib/infrastructure/data/repositories/`
- **实现方式**：实现领域层定义的 Repository 接口
- **数据映射**：领域模型与数据模型的映射
- **查询优化**：数据库查询的优化和执行

### 事务实现

事务实现位于基础设施层：

- **代码位置**：`apps/flutter-app/lib/infrastructure/data/transactions/`
- **实现方式**：实现事务管理接口
- **事务边界**：事务的创建、提交和回滚

### 查询实现

查询实现位于基础设施层：

- **代码位置**：`apps/flutter-app/lib/infrastructure/data/queries/`
- **实现方式**：实现查询构建器接口
- **查询优化**：查询条件的优化和执行

## 使用场景

### 领域层使用数据访问抽象

领域层通过具体业务域的 Repository 接口访问数据。具体 Repository 接口定义在领域层，可能继承或使用通用抽象接口（IRepository<T>）：

```dart
// 在领域服务中使用具体业务域的Repository接口
// 注意：I{{AggregateRoot1}}Repository 定义在领域层，不属于数据访问抽象
class {{AggregateRoot1}}Service {
  final I{{AggregateRoot1}}Repository _repository;

  Future<void> create{{AggregateRoot1}}({{AggregateRoot1}} aggregate) async {
    // 业务逻辑验证
    if (!aggregate.isValid()) {
      throw DomainException('{{aggregateValidationRule}}');
    }

    // 通过具体Repository接口保存
    await _repository.save(aggregate);
  }
}
```

**说明**：

- `I{{AggregateRoot1}}Repository` 是具体业务域的 Repository 接口，定义在领域层
- 该接口可能继承 `IRepository<{{AggregateRoot1}}>`（通用抽象接口）
- 领域服务使用具体业务域的 Repository 接口，而不是直接使用通用抽象接口

### 应用层使用数据访问抽象

应用层通过具体业务域的 Repository 接口访问数据：

```dart
// 在应用服务中使用具体业务域的Repository接口
// 注意：I{{AggregateRoot1}}Repository 定义在领域层，不属于数据访问抽象
class Create{{AggregateRoot1}}CommandHandler {
  final I{{AggregateRoot1}}Repository _repository;

  Future<void> handle(Create{{AggregateRoot1}}Command command) async {
    final aggregate = {{AggregateRoot1}}.create(
      {{property1}}: command.{{property1}},
      {{property2}}: command.{{property2}},
    );

    await _repository.save(aggregate);
  }
}
```

**说明**：

- 应用层使用具体业务域的 Repository 接口（定义在领域层）
- 通用抽象接口（IRepository<T>）主要供基础设施层实现时使用

### 事务使用场景

多个 Repository 操作需要在同一事务中执行。事务管理接口（ITransactionManager）是数据访问抽象提供的通用抽象接口：

```dart
// 使用数据访问抽象提供的事务管理接口
await transactionManager.executeInTransaction((transaction) async {
  await {{aggregateRoot1}}Repository.save(aggregate1);
  await {{aggregateRoot2}}Repository.save(aggregate2);
});
```

**说明**：

- `ITransactionManager` 是数据访问抽象提供的通用抽象接口
- 具体业务域的 Repository 接口（如 `I{{AggregateRoot1}}Repository`）定义在领域层
- 事务管理接口可以被领域层和应用层使用，管理多个 Repository 操作的事务边界

## 代码位置

### 接口定义

- **通用抽象接口**：`apps/flutter-app/lib/infrastructure/data/interfaces/`
- **业务域 Repository 接口**：各业务域的领域模型文档中定义

### 具体实现

- **Repository 实现**：`apps/flutter-app/lib/infrastructure/data/repositories/`
- **事务实现**：`apps/flutter-app/lib/infrastructure/data/transactions/`
- **查询实现**：`apps/flutter-app/lib/infrastructure/data/queries/`

### 数据映射

- **领域模型到数据模型映射**：`apps/flutter-app/lib/infrastructure/data/mappers/`
- **数据模型到领域模型映射**：`apps/flutter-app/lib/infrastructure/data/mappers/`

## 设计模式

### Repository 模式

**目的**：将数据访问逻辑封装在 Repository 接口中，实现领域层与基础设施层的解耦。

**实现**：

- 领域层定义 Repository 接口
- 基础设施层实现 Repository 接口
- 通过依赖注入将实现注入到领域层

**优势**：

- 领域层不依赖具体的数据存储实现
- 便于测试（可以使用模拟实现）
- 便于替换数据存储实现

### Unit of Work 模式

**目的**：管理多个 Repository 操作的事务边界。

**实现**：

- 通过事务管理器管理事务
- 多个 Repository 操作在同一事务中执行
- 事务提交或回滚保证数据一致性

**优势**：

- 保证多个操作的原子性
- 简化事务管理代码
- 支持嵌套事务

## 相关文档

- [[../01-infrastructure-overview.md]] - 基础设施层概览
- [[../tools/01-tools-overview.md]] - 技术工具概览
- [[../../overview/01-domain-overview.md]] - 领域概览
- [[../../overview/02-subdomain-mapping.md]] - 子领域映射
- [[../../overview/03-bounded-context.md]] - 限界上下文

## 变更记录

| 日期     | 版本 | 变更内容 | 变更人        |
| -------- | ---- | -------- | ------------- |
| {{date}} | 1.0  | 初始版本 | {{architect}} |
