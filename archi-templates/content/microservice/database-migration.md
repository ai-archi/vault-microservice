# {{serviceName}} 数据库迁移机制设计

**创建日期**: {{date}}  
**架构师**: {{architect}}  
**版本**: 1.0

## 概述

本文档描述 {{serviceName}} 微服务的数据库迁移机制设计，包括迁移策略选择、抽象接口设计和成熟方案推荐。

数据库迁移机制属于**基础设施层的数据访问模块**，提供数据库结构版本管理和迁移执行能力，是纯粹的技术能力，不包含业务逻辑。

## 架构定位

### 能力归属

数据库迁移机制属于**基础设施层的数据访问模块**，是纯粹的技术能力：

- **技术导向**：纯粹的技术实现，不包含业务逻辑
- **基础设施层**：位于 DDD 分层架构的基础设施层
- **数据访问模块**：属于数据访问基础设施的一部分
- **可复用性**：可以被多个业务域复用，统一管理数据库结构变更

### 与领域层的关系

数据库迁移机制**不属于领域层**，原因如下：

- **无业务逻辑**：迁移脚本只包含数据库结构变更（CREATE TABLE、ALTER TABLE 等），不包含业务规则
- **技术实现**：迁移机制是数据库管理的技术实现，与业务概念无关
- **基础设施能力**：为领域层提供数据存储基础设施，但不参与业务逻辑

### 职责边界

**边界内**：

- 迁移脚本版本管理
- 迁移脚本执行机制
- 迁移历史记录管理
- 数据库版本追踪
- 应用启动时自动执行迁移
- 迁移脚本回滚支持（可选）

**边界外**：

- 业务数据迁移（属于应用层或领域层）
- 业务规则验证（属于领域层）
- 数据库连接管理（属于数据访问抽象）

## 设计原则

数据库迁移机制遵循以下设计原则：

1. **版本化管理**：每个迁移脚本有唯一版本号，按版本顺序执行
2. **幂等性**：迁移脚本可以安全地重复执行，不会产生副作用
3. **原子性**：每个迁移脚本在事务中执行，失败时自动回滚
4. **可追溯性**：记录所有迁移执行历史，便于问题排查
5. **自动化**：应用启动时自动检测并执行未执行的迁移脚本
6. **向前兼容**：支持数据库结构向前演进，保证数据完整性

## 成熟方案推荐

### 方案对比

| 方案             | 类型         | 优势                             | 劣势                   | 适用场景                   |
| ---------------- | ------------ | -------------------------------- | ---------------------- | -------------------------- |
| **Flyway**       | 迁移工具     | 成熟稳定、版本管理完善、支持多种数据库 | 需要额外依赖           | Java/Spring 项目           |
| **Liquibase**    | 迁移工具     | 功能强大、支持多种格式、变更日志管理 | 配置复杂               | 企业级项目                 |
| **自定义封装**   | 基于框架     | 灵活、可定制、符合项目需求       | 需要自己实现           | 需要特定功能、团队有经验   |
| **ORM 内置迁移** | ORM 功能     | 与 ORM 集成、自动生成迁移        | 依赖 ORM 框架          | 使用 ORM 的项目            |

### 推荐方案

**{{migrationTool}}**

**选型理由**：

{{migrationToolReason}}

**官方文档**：{{migrationToolDocUrl}}

**适用场景**：

{{migrationToolScenarios}}

## 抽象接口设计

### 迁移执行器接口

```{{language}}
/// 数据库迁移执行器接口
///
/// 提供数据库迁移的核心能力，包括执行迁移、版本查询等
abstract class IMigrationExecutor {
  /// 执行所有未执行的迁移脚本
  Future<void> migrate();

  /// 执行指定版本的迁移脚本
  Future<void> migrateToVersion(String version);

  /// 获取当前数据库版本
  Future<String?> getCurrentVersion();

  /// 获取所有已执行的迁移版本
  Future<List<String>> getExecutedVersions();

  /// 检查迁移脚本是否需要执行
  Future<bool> needsMigration();
}
```

### 迁移脚本加载器接口

```{{language}}
/// 迁移脚本加载器接口
///
/// 负责加载和验证迁移脚本
abstract class IMigrationScriptLoader {
  /// 加载所有迁移脚本
  Future<List<MigrationScript>> loadAllScripts();

  /// 加载指定版本的迁移脚本
  Future<MigrationScript?> loadScript(String version);

  /// 验证迁移脚本格式
  Future<bool> validateScript(MigrationScript script);
}

/// 迁移脚本模型
class MigrationScript {
  final String version;
  final String description;
  final String content;
  final String checksum;
  final DateTime createdAt;

  MigrationScript({
    required this.version,
    required this.description,
    required this.content,
    required this.checksum,
    required this.createdAt,
  });
}
```

### 迁移历史模型

```{{language}}
/// 迁移历史记录模型
class MigrationHistory {
  final String version;
  final String description;
  final DateTime executedAt;
  final int executionTimeMs;
  final String checksum;
  final bool success;

  MigrationHistory({
    required this.version,
    required this.description,
    required this.executedAt,
    required this.executionTimeMs,
    required this.checksum,
    required this.success,
  });
}
```

## 迁移脚本规范

### 命名规范

迁移脚本采用版本化命名规范：

```
V{version}__{description}.sql
```

**命名规范说明**：

- `V`：固定前缀，表示 Version
- `{version}`：版本号，格式为 `{major}.{minor}.{patch}` 或 `{timestamp}`（如 `1.0.0` 或 `20250109120000`）
- `__`：双下划线分隔符
- `{description}`：迁移描述，使用下划线分隔（如 `create_{{tableName}}_table`）

**示例**：

```
V1.0.0__create_{{tableName1}}_table.sql
V1.0.1__add_{{tableName2}}_table.sql
V1.1.0__add_{{columnName}}_column.sql
V2.0.0__add_index.sql
```

### 脚本结构规范

迁移脚本应包含以下部分：

```sql
-- Migration: V{version}__{description}
-- Description: {详细描述}
-- Author: {作者}
-- Date: {日期}

-- 迁移内容
CREATE TABLE IF NOT EXISTS {{tableName}} (
    -- 表结构定义
);

-- 索引创建
CREATE INDEX IF NOT EXISTS idx_{{indexName}} ON {{tableName}}({{columnName}});

-- 其他操作
```

**脚本要求**：

- **幂等性**：使用 `IF NOT EXISTS`、`IF EXISTS` 等语句保证可重复执行
- **事务性**：每个脚本在事务中执行，失败时自动回滚
- **注释**：包含迁移版本、描述、作者、日期等信息
- **可读性**：SQL 语句格式化，便于阅读和维护

### 迁移历史表结构

迁移历史表用于记录已执行的迁移脚本：

```sql
CREATE TABLE IF NOT EXISTS schema_migrations (
    version TEXT PRIMARY KEY,
    description TEXT NOT NULL,
    executed_at INTEGER NOT NULL,
    execution_time_ms INTEGER NOT NULL,
    checksum TEXT,
    success BOOLEAN NOT NULL DEFAULT 1
);

CREATE INDEX IF NOT EXISTS idx_schema_migrations_executed_at
ON schema_migrations(executed_at);
```

**字段说明**：

- `version`：迁移脚本版本号（主键）
- `description`：迁移描述
- `executed_at`：执行时间戳（Unix 时间戳，毫秒）
- `execution_time_ms`：执行耗时（毫秒）
- `checksum`：脚本内容校验和（用于检测脚本变更）
- `success`：执行是否成功

## 实现方案

### {{migrationTool}} 集成

{{migrationToolImplementation}}

### 应用启动集成

在应用启动时，数据库初始化流程如下：

```
1. 打开数据库连接
2. 初始化迁移历史表（如果不存在）
3. 检测未执行的迁移脚本
4. 按版本顺序执行迁移脚本
5. 记录迁移历史
6. 配置数据库选项
```

**集成示例**：

```{{language}}
/// 数据库初始化服务
class DatabaseInitializationService {
  final IMigrationExecutor _migrationExecutor;
  final ILogger _logger;

  DatabaseInitializationService({
    required IMigrationExecutor migrationExecutor,
    ILogger? logger,
  })  : _migrationExecutor = migrationExecutor,
        _logger = logger ?? LoggerAdapter();

  /// 初始化数据库（应用启动时调用）
  Future<Database> initializeDatabase() async {
    _logger.info('Initializing database...');

    // 1. 打开数据库连接
    final database = await _openDatabase();

    // 2. 执行数据库迁移
    try {
      await _migrationExecutor.migrate();
      _logger.info('Database migration completed');
    } catch (e, stackTrace) {
      _logger.error(
        'Database migration failed: $e',
        error: e,
        stackTrace: stackTrace,
      );
      // 迁移失败时阻止应用启动
      rethrow;
    }

    // 3. 配置数据库选项
    await _configureDatabase(database);

    _logger.info('Database initialization completed');
    return database;
  }

  /// 配置数据库选项
  Future<void> _configureDatabase(Database database) async {
    // 根据数据库类型配置选项
    // 例如：WAL 模式、外键约束等
  }
}
```

## 迁移脚本组织

### 目录结构

迁移脚本建议的组织结构：

```
{{projectRoot}}/
├── src/main/resources/db/migration/  # 或 assets/migrations/
│   ├── V1.0.0__create_{{tableName1}}_table.sql
│   ├── V1.0.1__add_{{tableName2}}_table.sql
│   ├── V1.1.0__add_{{columnName}}_column.sql
│   └── V2.0.0__add_index.sql
└── ...
```

### 配置文件

在配置文件中指定迁移脚本位置：

{{migrationConfigExample}}

## 最佳实践

### 1. 迁移脚本编写

- **幂等性**：使用 `IF NOT EXISTS`、`IF EXISTS` 等语句
- **事务性**：每个脚本在事务中执行
- **可读性**：格式化 SQL，添加注释
- **版本化**：遵循版本命名规范

### 2. 迁移执行策略

- **自动执行**：应用启动时自动执行未执行的迁移
- **失败处理**：迁移失败时阻止应用启动，记录错误日志
- **版本检查**：执行前检查版本顺序，防止跳过版本

### 3. 数据迁移

- **结构迁移**：迁移脚本只包含结构变更（CREATE、ALTER、DROP）
- **数据迁移**：数据迁移属于应用层，通过应用服务实现
- **回滚支持**：可选支持回滚脚本（R 前缀）

### 4. 性能优化

- **批量执行**：多个迁移脚本在单个事务中执行（可选）
- **索引优化**：迁移后重建索引，优化查询性能
- **统计信息更新**：迁移后更新数据库统计信息

## 代码位置

### 接口定义

- **迁移执行器接口**：`{{packagePath}}/infrastructure/data/migrations/interfaces/imigration_executor.{{extension}}`
- **脚本加载器接口**：`{{packagePath}}/infrastructure/data/migrations/interfaces/imigration_script_loader.{{extension}}`

### 具体实现

- **迁移执行器实现**：`{{packagePath}}/infrastructure/data/migrations/implementations/`
- **脚本加载器实现**：`{{packagePath}}/infrastructure/data/migrations/implementations/`

### 迁移脚本

- **迁移脚本目录**：`{{migrationScriptPath}}`

## 相关文档

- [[../data-access/01-data-access-abstraction.md]] - 数据访问抽象设计
- [[../../05-storage/02-migration-history.md]] - 数据库迁移历史
- [[../../05-storage/01-schema.md]] - 数据库结构文档
- [[../01-infrastructure-overview.md]] - 基础设施层概览

## 变更记录

| 日期     | 版本 | 变更内容 | 变更人     |
| -------- | ---- | -------- | ---------- |
| {{date}} | 1.0  | 初始版本 | {{architect}} |

