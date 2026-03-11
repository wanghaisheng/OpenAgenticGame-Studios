---
name: unity-skills
description: Unity Skills CLI自动化工具。通过HTTP API直接控制Unity编辑器，支持场景管理、节点操作、资源管理、组件操作、批量操作、工作流管理和项目自动化。从dev/Unity-Skills-main整合的Unity Skills CLI工具，提供程序化的Unity编辑器控制和开发工作流自动化支持。
---

# Unity Skills CLI

Unity Skills CLI自动化工具，通过HTTP API直接控制Unity编辑器，支持场景管理、节点操作、资源管理、组件操作、批量操作、工作流管理和项目自动化。

## Quick Start

```bash
# 检查服务状态
unity-skills health

# 查看所有可用技能
unity-skills get-skills

# 查看编辑器状态
unity-skills editor status
```

---

## 核心功能

### 场景管理
- **场景打开**: 加载和激活指定场景
- **场景保存**: 保存当前场景状态
- **场景创建**: 创建新场景
- **场景查询**: 查询场景信息和节点树
- **场景验证**: 验证场景完整性

### 节点管理
- **节点创建**: 创建新节点和GameObject
- **节点删除**: 安全删除节点
- **节点查找**: 查找指定节点
- **节点属性**: 获取和设置节点属性
- **节点批量操作**: 批量节点操作

### 组件管理
- **组件添加**: 向节点添加组件
- **组件删除**: 从节点删除组件
- **组件配置**: 配置组件属性
- **组件查找**: 查找指定组件
- **组件批量操作**: 批量组件操作

### 资源管理
- **资源创建**: 创建新资源文件
- **资源导入**: 导入外部资源
- **资源删除**: 删除指定资源
- **资源验证**: 验证资源完整性
- **资源批量操作**: 批量资源操作

### 工作流管理
- **工作流创建**: 创建自定义工作流
- **工作流执行**: 执行指定工作流
- **工作流状态**: 查看工作流状态
- **工作流历史**: 查看工作流历史

---

## 高级功能

### 批量操作优化
```bash
# 批量创建节点
unity-skills gameobject create-batch '[{"name":"Node1","primitiveType":"Cube","x":0,"y":0,"z":0},{"name":"Node2","primitiveType":"Sphere","x":10,"y":0,"z":0}]'

# 批量设置属性
unity-skills property set-batch <node-uuid> '{"x":100,"y":200,"z":0}'

# 批量添加组件
unity-skills component add-batch <node-uuid> '[{"type":"Rigidbody"},{"type":"Collider","properties":{"isTrigger":true}}]'
```

### 模板系统
```bash
# 使用节点模板
unity-skills template create-node-from-template <template-name> <parent-uuid>

# 创建自定义模板
unity-skills template create-template <template-name> <template-data>

# 应用模板到节点
unity-skills template apply-template <node-uuid> <template-name>
```

### 自动化脚本
```bash
# 执行自定义脚本
unity-skills script execute <script-file>

# 脚本验证
unity-skills script validate <script-file>

# 脚本调试
unity-skills script debug <script-file>
```

### 工作流自动化
```bash
# 创建工作流
unity-skills workflow create <workflow-name> <workflow-data>

# 执行工作流
unity-skills workflow execute <workflow-name>

# 查看工作流状态
unity-skills workflow status <workflow-name>

# 查看工作流历史
unity-skills workflow history <workflow-name>
```

---

## 开发工具集成

### VS Code集成
- **插件系统**: Unity Editor插件支持
- **命令行工具**: 命令行自动化工具
- **调试支持**: 调试和错误处理
- **自动完成**: 智能代码补全

### CI/CD集成
- **自动化测试**: 自动化测试脚本
- **构建流水线**: CI/CD流水线集成
- **部署自动化**: 自动化部署流程
- **质量检查**: 自动化质量检查

### 版本控制
- **Git集成**: Git版本控制集成
- **分支管理**: 分支管理和合并
- **标签管理**: 版本标签管理
- **冲突解决**: 合并冲突解决

---

## 性能优化

### 批处理优化
- **批量操作**: 高效的批量处理算法
- **内存管理**: 有效的内存管理机制
- **异步处理**: 异步操作处理
- **缓存机制**: 智能缓存机制

### 网络优化
- **连接池**: HTTP连接池管理
- **请求优化** - 请求优化和批处理
- **错误处理** - 网络错误处理
- **重试机制** - 智能重试机制

### 编辑器优化
- **编辑器性能** - 编辑器性能优化
- **内存管理** - 编辑器内存管理
- **响应时间** - 响应时间优化
- **稳定性** - 编辑器稳定性保证

---

## 安全考虑

### 权限控制
- **访问控制** - 基于角色的访问控制
- **操作验证** - 操作权限验证
- **安全日志** - 安全操作日志
- **审计跟踪** - 操作审计跟踪

### 数据保护
- **数据加密** - 敏感数据加密
- **备份策略** - 数据备份策略
- **恢复机制** - 数据恢复机制
- **完整性检查** - 数据完整性检查

---

## 故障排除

### 常见问题
1. **连接失败**: 检查Unity Editor HTTP Server状态
2. **权限错误**: 确认Unity Editor权限设置
3. **格式错误**: 验证JSON格式和数据类型
4. **超时错误**: 检查网络连接和超时设置
5. **编辑器状态**: 检查Unity Editor状态

### 调试工具
```bash
# 启用调试模式
unity-skills --debug

# 显示详细日志
unity-skills --verbose

# 检查系统状态
unity-skills health --detailed

# 查看编辑器状态
unity-skills editor status --detailed
```

### 错误恢复
```bash
# 自动重试失败操作
unity-skills --retry

# 重置编辑器状态
unity-skills editor reset

# 从备份恢复
unity-skills editor restore <backup-id>

# 验证编辑器状态
unity-skills editor validate
```

---

## 扩展开发

### 自定义技能
```csharp
// 创建自定义技能
[UnitySkill("custom_skill", "Custom skill description")]
public class CustomSkill
{
    public static void Execute(string[] args)
    {
        // 自定义技能逻辑
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
- **钩子机制** - 钩子机制支持

---

## 最佳实践

### 开发规范
- **代码风格**: 统一的代码风格规范
- **命名规范**: 清晰的命名规范
- **文档规范**: 完整的文档规范
- **测试规范**: 完善的测试规范

### 性能优化
- **批量处理**: 优先使用批量处理
- **异步操作** - 使用异步操作处理
- **缓存策略** - 合理的缓存策略
- **资源管理** - 有效的资源管理

### 安全实践
- **输入验证** - 严格的输入验证
- **权限检查** - 完整的权限检查
- **日志记录** - 详细的日志记录
- **审计跟踪** - 完整的审计跟踪

---

## 使用示例

### 基础场景操作
```bash
# 创建新场景
unity-skills scene create-scene "NewScene"

# 添加节点到场景
unity-skills gameobject create-node '{"name":"Player","primitiveType":"Cube","x":0,"y":0,"z":0}'

# 保存场景
unity-skills scene save-scene
```

### 批量操作示例
```bash
# 批量创建多个节点
unity-skills gameobject create-batch '[{"name":"Enemy","primitiveType":"Sphere","x":10,"y":0,"z":0},{"name":"Item","primitiveType":"Cube","x":20,"y":0,"z":0}]'

# 批量设置属性
unity-skills property set-batch <node-uuid> '{"x":100,"y":200,"z":0}'
```

### 工作流示例
```bash
# 创建自动化工作流
unity-skills workflow create "BuildScene" '{"steps":[{"name":"CreateCanvas","type":"scene","properties":{"designResolution":{"width":1920,"height":1080}},{"name":"AddCamera","type":"camera","properties":{"clearFlags":7}},{"name":"AddLighting","type":"light","properties":{"type":"Directional","intensity":1.0}}]}'

# 执行工作流
unity-skills workflow execute "BuildScene"

# 查看工作流状态
unity-skills workflow status "BuildScene"
```

---

*Unity Skills CLI*
*Version: 1.6.1*
*Last updated: 2026-03-10*
*Integration: Claude Code Game Studios*
