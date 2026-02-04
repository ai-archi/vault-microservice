# {{subdomainName}} 应用层概览

**创建日期**: {{date}}  
**领域专家**: {{domainExpert}}  
**版本**: 1.0

## 概述

本文档描述 {{subdomainName}} 领域的应用层设计，包括应用层的职责、设计原则、架构模式和与领域层的协调关系。

> **说明**：应用层是业务用例和领域模型之间的协调层。它不包含业务逻辑（业务逻辑在领域层），而是负责编排、流程控制和技术关切点。

## 应用层定位

### 职责范围

应用层的主要职责包括：

1. **用例编排**：将用户请求转化为对领域服务和聚合根的调用
2. **数据转换**：在 API 层（外部DTO）和领域模型层（内部对象）之间进行转换
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
│                                 │
│ - 用例编排                      │
│ - DTO 转换                      │
│ - 事务管理                      │
│ - 权限检查                      │
├─────────────────────────────────┤
│   领域层（Domain Model）        │  ← 业务逻辑层
│                                 │
│ - 聚合根                        │
│ - 实体                          │
│ - 值对象                        │
│ - 领域服务                      │
│ - 领域事件                      │
├─────────────────────────────────┤
│   基础设施层（Infrastructure）  │  ← 技术支持层
└─────────────────────────────────┘
```

## 应用层设计原则

### 1. 单一职责原则（SRP）

每个应用服务只负责一个用例的协调，不混淆多个业务流程。

**反例**：

```dart
// ❌ 不好的做法：一个应用服务处理多个无关用例
class UserApplicationService {
  Future<void> registerUserAndSendEmail(RegisterRequest req) {
    // 处理用户注册
    // 同时处理邮件发送
  }
  
  Future<void> updateProfileAndLogActivity(UpdateRequest req) {
    // 处理资料更新
    // 同时处理日志记录
  }
}
```

**好例子**：

```dart
// ✅ 好的做法：每个应用服务对应一个用例
class RegisterUserApplicationService {
  Future<void> execute(RegisterUserRequest req) {
    // 仅编排用户注册
  }
}

class SendRegistrationEmailApplicationService {
  Future<void> execute(SendEmailRequest req) {
    // 仅编排邮件发送
  }
}
```

### 2. 领域模型不渗漏

应用层应该封装领域模型的实现细节，对外部（表现层）只暴露 DTO，不暴露领域对象。

**反例**：

```dart
// ❌ 不好的做法：直接返回领域对象
class UserApplicationService {
  Future<User> getUserById(String userId) {
    return userRepository.findById(userId);  // 返回领域对象
  }
}
```

**好例子**：

```dart
// ✅ 好的做法：返回 DTO
class UserApplicationService {
  Future<UserDTO> getUserById(String userId) {
    final user = await userRepository.findById(userId);
    return UserDTO.fromDomain(user);  // 转换为 DTO
  }
}
```

### 3. 事务边界清晰

应用服务是事务的边界。一个应用服务方法的执行应该是一个完整的业务操作。

**反例**：

```dart
// ❌ 不好的做法：事务边界不清晰
class OrderApplicationService {
  Future<void> createOrder(CreateOrderRequest req) {
    // 创建订单
    // 但事务在何处开始和结束？
  }
}
```

**好例子**：

```dart
// ✅ 好的做法：清晰的事务边界
class CreateOrderApplicationService {
  @Transactional()  // 明确事务开始
  Future<OrderDTO> execute(CreateOrderRequest req) async {
    // 完整的业务操作
    // 事务在方法结束时提交或回滚
    return orderDTO;
  }
}
```

### 4. 依赖反向

应用层不应该依赖具体的基础设施实现，而应该依赖抽象接口（Repository、Service 等）。

### 5. 错误处理明确

应用层负责捕获领域异常和基础设施异常，转换为适当的响应。

## CQRS 设计（如适用）

### 命令处理流程

如果应用层采用 CQRS（命令查询职责分离）模式，命令处理流程如下：

```
命令请求
  ↓
1. 参数验证 (Validation)
  ↓
2. 权限检查 (Authorization)
  ↓
3. 加载聚合根 (Load Aggregate)
  ↓
4. 执行业务方法 (Execute Business Logic)
  ↓
5. 聚合根状态变化 → 领域事件
  ↓
6. 保存聚合根 (Save Aggregate)
  ↓
7. 发布领域事件 (Publish Domain Events)
  ↓
8. 返回结果 (Return Result)
```

### 查询处理流程

```
查询请求
  ↓
1. 参数验证 (Validation)
  ↓
2. 权限检查 (Authorization)
  ↓
3. 构建查询 (Build Query)
  ↓
4. 执行查询 (Execute Query)
  ↓
5. 转换为 DTO (Convert to DTO)
  ↓
6. 返回结果 (Return Result)
```

## 应用服务设计

### 应用服务的职责

**应用服务**是 DDD 中应用层的核心组件。每个应用服务对应一个用例的编排。

#### 主要职责

1. **编排业务流程**：组织多个领域对象的协调
2. **处理事务**：管理事务的开始、提交或回滚
3. **权限检查**：验证当前用户是否有权执行此操作
4. **DTO 转换**：将外部 DTO 转换为领域对象，以及将领域对象转换为响应 DTO
5. **异常处理**：捕获业务异常和技术异常，转换为适当的错误响应

#### 应用服务的方法签名

```dart
// 命令模式（修改操作）
@Transactional()
Future<OutputDTO> execute(CommandDTO input);

// 查询模式（读取操作）
Future<OutputDTO> query(QueryDTO input);
```

### 应用服务与领域服务的区别

| 维度 | 应用服务 | 领域服务 |
|------|---------|---------|
| 层级 | 应用层 | 领域层 |
| 职责 | 编排、流程、协调 | 业务逻辑、核心概念 |
| 状态 | 通常无状态 | 通常无状态 |
| 参数 | DTO、命令对象 | 领域对象 |
| 返回值 | DTO | 领域对象或值对象 |
| 事务管理 | 应用服务管理 | 领域服务不管理 |
| 示例 | `CreateOrderApplicationService` | `PricingDomainService` |

**反例：应用服务中实现业务逻辑**

```dart
// ❌ 不好的做法：业务逻辑在应用层
class CreateOrderApplicationService {
  Future<OrderDTO> execute(CreateOrderRequest req) async {
    // ❌ 这个逻辑应该在 Order 聚合根中
    if (req.items.isEmpty) {
      throw Exception("Order must have items");
    }
    
    // ❌ 这个逻辑应该在 PricingDomainService 中
    double totalPrice = 0;
    for (var item in req.items) {
      totalPrice += item.price * item.quantity;
    }
    
    final order = Order.create(id, req.customerId, totalPrice);
    await orderRepository.save(order);
    return OrderDTO.fromDomain(order);
  }
}
```

**好例子：应用服务进行编排**

```dart
// ✅ 好的做法：业务逻辑在领域层，应用服务进行编排
class CreateOrderApplicationService {
  @Transactional()
  Future<OrderDTO> execute(CreateOrderRequest req) async {
    // 1. 加载相关聚合根或查询信息
    final customer = await customerRepository.findById(req.customerId);
    
    // 2. 调用领域对象创建（业务逻辑在这里）
    final order = Order.create(
      id: IdGenerator.generate(),
      customerId: req.customerId,
      items: req.items.map(OrderItem.create).toList(),
    );  // Order.create 内部包含所有业务验证
    
    // 3. 调用领域服务进行复杂业务逻辑
    await pricingService.calculateAndApplyDiscount(order, customer);
    
    // 4. 保存到持久化存储
    await orderRepository.save(order);
    
    // 5. 发布领域事件
    eventPublisher.publishAll(order.domainEvents);
    
    // 6. 转换并返回
    return OrderDTO.fromDomain(order);
  }
}
```

## DTO 设计

### 请求 DTO

用于接收来自 API 层的请求数据。

**特点**：
- 对应于 API 请求体的结构
- 包含数据验证注解（如 @NotNull、@Email）
- 不包含业务逻辑

**示例**：

```dart
class CreateOrderRequest {
  @NotNull()
  final String customerId;
  
  @NotEmpty()
  final List<OrderItemRequest> items;
  
  @Range(min: 0)
  final double? discountAmount;
  
  CreateOrderRequest({
    required this.customerId,
    required this.items,
    this.discountAmount,
  });
}

class OrderItemRequest {
  @NotNull()
  final String productId;
  
  @Range(min: 1)
  final int quantity;
  
  @Range(min: 0)
  final double price;
  
  OrderItemRequest({
    required this.productId,
    required this.quantity,
    required this.price,
  });
}
```

### 响应 DTO

用于返回数据给 API 层。

**特点**：
- 对应于 API 响应体的结构
- 不包含内部实现细节
- 通常是只读的（final 字段）

**示例**：

```dart
class OrderDTO {
  final String orderId;
  final String customerId;
  final List<OrderItemDTO> items;
  final double totalPrice;
  final String status;
  final DateTime createdAt;
  
  OrderDTO({
    required this.orderId,
    required this.customerId,
    required this.items,
    required this.totalPrice,
    required this.status,
    required this.createdAt,
  });
  
  factory OrderDTO.fromDomain(Order order) {
    return OrderDTO(
      orderId: order.id.value,
      customerId: order.customerId.value,
      items: order.items.map(OrderItemDTO.fromDomain).toList(),
      totalPrice: order.totalPrice.amount,
      status: order.status.name,
      createdAt: order.createdAt,
    );
  }
}
```

### 内部 DTO

在应用层内部的不同应用服务之间传递数据时使用。

## 错误处理

### 应用层错误处理策略

{{errorHandlingStrategy}}

### 异常映射表

| 领域异常 | HTTP 状态码 | 错误响应码 | 说明 |
|---------|-----------|---------|------|
| {{domainException1}} | {{httpStatus1}} | {{errorCode1}} | {{description1}} |
| {{domainException2}} | {{httpStatus2}} | {{errorCode2}} | {{description2}} |

## 事务管理

### 事务边界

应用服务方法是事务的边界。在 {{frameworkName}} 中：

{{transactionManagement}}

## 与领域层的协调

### 应用服务如何调用领域对象

#### 1. 创建新聚合根

```dart
// 通过工厂方法创建新聚合根
final order = Order.create(
  id: IdGenerator.generate(),
  customerId: customerId,
  items: items,
);
```

#### 2. 加载现有聚合根

```dart
// 通过 Repository 获取聚合根
final order = await orderRepository.findById(orderId);
if (order == null) {
  throw OrderNotFoundException(orderId);
}
```

#### 3. 修改聚合根

```dart
// 调用聚合根的方法进行修改
order.addItem(productId, quantity, price);
order.applyDiscount(discountAmount);

// 保存修改
await orderRepository.save(order);

// 发布领域事件
eventPublisher.publishAll(order.domainEvents);
```

#### 4. 调用领域服务

```dart
// 领域服务处理复杂的业务逻辑
await pricingService.calculateAndApplyDiscount(order, customer);
```

## 相关文档

### 领域内文档

- [[01-domain-overview.md]] - 领域概览
- [[02-domain/01-domain-model.md]] - 领域模型（聚合根、领域服务等）
- [[02-domain/02-use-cases.md]] - 业务用例说明
- [[02-application-services.md]] - 应用服务实现细节
- [[04-apis/01-api-design.md]] - API 设计（应用服务的外部接口）

### 系统级文档

- [[../../01-overview/01-domains-overview.md]] - 系统级领域概览
- [[../../01-overview/03-bounded-context.md]] - 限界上下文定义

## 变更记录

| 日期 | 版本 | 变更内容 | 变更人 |
|------|------|----------|--------|
| {{date}} | 1.0 | 初始版本 | {{domainExpert}} |
