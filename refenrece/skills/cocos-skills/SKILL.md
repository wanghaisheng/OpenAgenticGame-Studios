---
name: cocos-skills
description: Cocos Creator 命令行自动化工具。支持场景管理、资源操作、节点创建、组件绑定、属性设置等常用开发流程。从dev/cocos-skills-main整合的Cocos Creator CLI自动化工具，提供HTTP-based编辑器控制和程序化开发支持。
---

# Cocos Skills

Cocos Creator 命令行自动化工具，用于快速完成游戏开发中的重复性操作。

## 快速开始

```bash
# 检查服务状态
cocos-skills health

# 查看所有命令
cocos-skills scene -h
```

---

## 常用工作流程

### 场景编辑流程

```
打开场景 → 查询节点树 → 修改节点/组件 → 保存场景
```

```bash
# 1. 打开场景
cocos-skills scene open-scene db://assets/scenes/Main.scene

# 2. 查询节点树（获取 UUID）
cocos-skills scene query-node-tree minimal

# 3. 修改操作
#    - 创建节点、添加组件、设置属性

# 4. 保存场景
cocos-skills scene save-scene
```

### 资源操作流程

```
导入资源 → 创建预制体 → 绑定组件引用
```

```bash
# 1. 创建资源
cocos-skills asset-db create-asset db://assets/config.json

# 2. 创建预制体
cocos-skills prefab create-prefab db://assets/prefabs/Player.prefab

# 3. 绑定组件引用
cocos-skills component bind-component
```

### 组件管理流程

```
添加组件 → 设置属性 → 绑定事件 → 测试组件
```

```bash
# 1. 添加组件到节点
cocos-skills component add-component <node-uuid> <component-type>

# 2. 设置组件属性
cocos-skills property set-property <node-uuid> <component-uuid> <property-name> <value>

# 3. 绑定事件
cocos-skills event bind-event <node-uuid> <event-type> <callback>
```

---

## 核心功能

### 场景管理
- **场景打开**: 加载和激活指定场景
- **场景保存**: 保存当前场景状态
- **节点查询**: 查询场景节点树结构
- **场景验证**: 验证场景完整性

### 节点操作
- **节点创建**: 创建新节点并设置属性
- **节点删除**: 安全删除节点及其子节点
- **节点移动**: 移动节点到指定父节点
- **节点复制**: 复制节点及其组件

### 组件操作
- **组件添加**: 向节点添加指定组件
- **组件删除**: 从节点删除组件
- **组件查询**: 查询节点组件信息
- **组件配置**: 配置组件属性

### 属性操作
- **属性设置**: 设置组件属性值
- **属性获取**: 获取组件属性值
- **属性验证**: 验证属性值有效性
- **属性批量操作**: 批量设置多个属性

### 资源管理
- **资源创建**: 创建新资源文件
- **资源导入**: 导入外部资源
- **资源删除**: 删除指定资源
- **资源验证**: 验证资源完整性

---

## 高级功能

### 批量操作
```bash
# 批量创建节点
cocos-skills node create-batch '[{"name":"Node1"},{"name":"Node2"}]'

# 批量设置属性
cocos-skills property set-batch <node-uuid> '{"x":100,"y":200}'

# 批量保存场景
cocos-skills scene save-all-scenes
```

### 模板系统
```bash
# 使用节点模板
cocos-skills template create-node-from-template <template-name> <parent-uuid>

# 创建自定义模板
cocos-skills template create-template <template-name> <template-data>
```

### 自动化脚本
```bash
# 执行自动化脚本
cocos-skills script execute <script-file>

# 脚本验证
cocos-skills script validate <script-file>

# 脚本调试
cocos-skills script debug <script-file>
```

---

## 开发工具集成

### IDE集成
- **VS Code插件**: Cocos Creator VS Code扩展
- **命令行工具**: 命令行自动化工具
- **构建集成**: 与构建系统集成
- **调试支持**: 调试和错误处理

### CI/CD支持
- **自动化测试**: 自动化测试脚本
- **构建流水线**: CI/CD流水线集成
- **部署自动化**: 自动化部署流程
- **质量检查**: 代码质量检查

### 版本控制
- **Git集成**: Git版本控制集成
- **分支管理**: 分支管理和合并
- **标签管理**: 版本标签管理
- **冲突解决**: 合并冲突解决

---

## 性能优化

### 批处理优化
- **批量操作**: 高效的批量处理算法
- **内存管理**: 内存使用优化
- **缓存机制**: 智能缓存机制
- **异步处理**: 异步操作处理

### 网络优化
- **连接池**: HTTP连接池管理
- **请求优化**: 请求优化和批处理
- **错误处理**: 网络错误处理
- **重试机制**: 智能重试机制

### 数据处理
- **JSON处理**: 高效JSON处理
- **数据验证**: 数据格式验证
- **类型转换**: 类型安全转换
- **错误处理**: 错误处理和恢复

---

## 安全考虑

### 权限控制
- **访问控制**: 基于角色的访问控制
- **操作验证**: 操作权限验证
- **安全日志**: 安全操作日志
- **审计跟踪**: 操作审计跟踪

### 数据保护
- **数据加密**: 敏感数据加密
- **备份策略**: 数据备份策略
- **恢复机制**: 数据恢复机制
- **完整性检查**: 数据完整性检查

---

## 故障排除

### 常见问题
1. **连接失败**: 检查Cocos Creator HTTP Server状态
2. **权限错误**: 确认编辑器权限设置
3. **格式错误**: 验证JSON格式和数据类型
4. **超时错误**: 检查网络连接和超时设置

### 调试工具
```bash
# 启用调试模式
cocos-skills --debug

# 查看详细日志
cocos-skills --verbose

# 检查系统状态
cocos-skills health --detailed
```

### 错误恢复
- **自动重试**: 自动重试失败的请求
- **状态恢复**: 自动恢复编辑器状态
- **数据恢复**: 自动恢复丢失的数据
- **服务重启**: 自动重启相关服务

---

## 扩展开发

### 自定义命令
```typescript
// 创建自定义命令
export class CustomCommand {
    execute(params: string[]): Promise<void> {
        // 自定义命令逻辑
    }
}
```

### 插件系统
- **插件接口**: 标准插件接口
- **插件加载**: 插件加载和管理
- **插件配置**: 插件配置和设置
- **插件扩展**: 插件扩展机制

### API集成
- **REST API**: RESTful API支持
- **WebSocket**: WebSocket连接支持
- **事件系统**: 事件系统接口
- **钩子机制**: 钩子机制支持

---

## 最佳实践

### 开发规范
- **代码风格**: 统一的代码风格规范
- **命名规范**: 清晰的命名规范
- **文档规范**: 完整的文档规范
- **测试规范**: 全面的测试规范

### 性能优化
- **批量处理**: 优先使用批量操作
- **缓存策略**: 合理的缓存策略
- **异步处理**: 使用异步处理
- **错误处理**: 完善的错误处理

### 安全实践
- **输入验证**: 严格的输入验证
- **权限检查**: 完整的权限检查
- **日志记录**: 详细的日志记录
- **审计跟踪**: 完整的审计跟踪

---

*版本: 1.0.0*
*最后更新: 2026-03-10*
*集成: Claude Code Game Studios*
