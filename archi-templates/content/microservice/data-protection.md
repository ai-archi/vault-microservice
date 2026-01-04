# {{serviceName}} 数据保护

**创建日期**: {{date}}  
**安全工程师**: {{securityEngineer}}  
**版本**: 1.0

## 概述

本文档定义 {{serviceName}} 微服务的数据保护策略，包括加密、脱敏和数据分类。

## 数据分类

### 数据分类级别

| 级别 | 描述 | 示例 | 保护要求 |
|------|------|------|---------|
| 公开 | {{publicDescription}} | {{publicExample}} | {{publicProtection}} |
| 内部 | {{internalDescription}} | {{internalExample}} | {{internalProtection}} |
| 机密 | {{confidentialDescription}} | {{confidentialExample}} | {{confidentialProtection}} |
| 绝密 | {{topSecretDescription}} | {{topSecretExample}} | {{topSecretProtection}} |

### 敏感数据识别

| 数据类型 | 敏感级别 | 处理方式 |
|---------|---------|---------|
| {{dataType1}} | {{sensitivityLevel1}} | {{handlingMethod1}} |
| {{dataType2}} | {{sensitivityLevel2}} | {{handlingMethod2}} |

## 数据加密

### 传输加密

{{transportEncryption}}

### 存储加密

{{storageEncryption}}

### 加密算法

| 用途 | 算法 | 密钥长度 | 描述 |
|------|------|---------|------|
| {{encryptionPurpose1}} | {{algorithm1}} | {{keyLength1}} | {{description1}} |
| {{encryptionPurpose2}} | {{algorithm2}} | {{keyLength2}} | {{description2}} |

### 密钥管理

{{keyManagement}}

## 数据脱敏

### 脱敏策略

{{dataMaskingStrategy}}

### 脱敏规则

| 数据类型 | 脱敏规则 | 示例 |
|---------|---------|------|
| {{dataType1}} | {{maskingRule1}} | {{example1}} |
| {{dataType2}} | {{maskingRule2}} | {{example2}} |

### 脱敏场景

{{maskingScenarios}}

## 数据备份和恢复

### 备份策略

{{backupStrategy}}

### 恢复策略

{{recoveryStrategy}}

## 数据保留和销毁

### 数据保留策略

{{dataRetentionStrategy}}

### 数据销毁策略

{{dataDestructionStrategy}}

## 数据访问控制

{{dataAccessControl}}

## 相关文档

- [[threat-model.md]] - 威胁建模
- [[authz-authn.md]] - 鉴权认证策略
- [[audit.md]] - 审计日志规范

## 变更记录

| 日期 | 版本 | 变更内容 | 变更人 |
|------|------|----------|--------|
| {{date}} | 1.0 | 初始版本 | {{securityEngineer}} |

