# Claude Code Game Studios - .claude Directory

## 📋 概述

这是Claude Code Game Studios项目的核心配置目录，包含84个专业agents、6个技能文件、配置文件和统一引用系统。

## 🎯 目录结构

```
.claude/
├── agents/ (84个agent文件)
│   ├── [1-8] Unity AI Workflow agents
│   ├── [9-16] Claude Resources agents
│   ├── [17-64] Claude Code Game Studios agents
│   ├── [68] Cocos Creator Specialist
│   ├── [69] Narrative Game Generator
│   ├── [70-74] Unity Development + Animation Specialists
│   ├── [75] Godot Full-Stack Specialist
│   ├── [76] Unity Asset Guidelines Specialist
│   ├── [77] Competitive Analysis Specialist
│   ├── [78-81] Design Framework Agents
│   ├── [82] Cocos Skills Automation Expert
│   ├── [83] Unity Skills Automation Expert
│   ├── [84] Game Quality Gates Specialist
│   └── [enhanced-*] 10个增强agents
├── skills/ (6个skill文件)
│   ├── godot/SKILL.md
│   ├── unity-asset-guidelines/SKILL.md
│   ├── competitive-analysis/SKILL.md
│   ├── game-quality-gates/SKILL.md
│   ├── cocos-skills/SKILL.md
│   └── unity-skills/SKILL.md
├── settings.json (主配置文件)
├── codex/ (AI Agent配置目录)
│   └── settings.json (codex配置)
└── hooks/ (可选，钩子脚本)
    ├── session-start.sh
    ├── validate-commit.sh
    ├── validate-push.sh
    ├── validate-assets.sh
    ├── pre-compact.sh
    ├── session-stop.sh
    └── log-agent.sh
```

## 🎯 Agent分类

### **按类别分类**
- **Leadership**: [17-27, 81] - Executive and vision leadership
- **Programming**: [28-33, 68, 70-74, 76, 83] - Core programming and development
- **Art**: [34-35, 40-44, 78] - Art direction and technical art
- **Design**: [36-39, 46-51, 69, 77, 79-80] - Game and system design
- **Audio**: [20, 44-45, 55-56] - Audio and sound design
- **QA**: [6, 25, 57, 84] - Quality assurance and testing
- **Production**: [26-27, 52-54] - Production and project management
- **Support**: [48-60, 71-73] - Community, analytics, and support
- **Specialized**: [75, 76, 77, 82-84] - Engine-specific and automation specialists

### **按引擎分类**
- **Unity**: 35个专家agents
- **Godot**: 7个专家agents
- **Unreal**: 5个专家agents
- **Cocos Creator**: 2个专家agents
- **Cross-Platform**: 35个跨平台agents

## 📚 Skills文件说明

### **技能文件列表**
1. **godot/SKILL.md** - Godot 4.x开发技能
2. **unity-asset-guidelines/SKILL.md** - Unity Asset Guidelines技能
3. **competitive-analysis/SKILL.md** - 竞争分析技能
4. **game-quality-gates/SKILL.md** - 游戏质量门禁技能
5. **cocos-skills/SKILL.md** - Cocos Creator CLI技能
6. **unity-skills/SKILL.md** - Unity Skills CLI技能

### **技能文件结构**
每个技能文件包含：
- **技能描述** - 详细的功能描述
- **使用场景** - 适用场景和使用条件
- **核心功能** - 主要功能和特性
- **最佳实践** - 使用最佳实践
- **故障排除** - 常见问题和解决方案

## 🔧 配置文件

### **settings.json** (主配置)
```json
{
  "$schema": "https://json.schemastore.org/claude-code-settings.json",
  "permissions": {
    "allow": [
      "Bash(git status*)",
      "Bash(git diff*)",
      "Bash(git log*)",
      "Bash(git branch*)",
      "Bash(git rev-parse*)",
      "Bash(ls *)",
      "Bash(dir *)",
      "Bash(python -m json.tool*)",
      "Bash(python -m pytest*)",
      "Bash(py -m pytest*)"
    ],
    "deny": [
      "Bash(rm -rf *)",
      "Bash(git push --force*)",
      "Bash(git push -f *)",
      "Bash(git reset --hard*)",
      "Bash(git clean -f*)",
      "Bash(sudo *)",
      "Bash(chmod 777*)",
      "Bash(*>.env*)",
      "Bash(cat *.env*)",
      "Bash(type *.env*)",
      "Read(**/.env*)"
    ]
  },
  "hooks": {
    "SessionStart": [...],
    "PreToolUse": [...],
    "PostToolUse": [...],
    "PreCompact": [...],
    "Stop": [...],
    "SubagentStart": [...]
  },
  "references": {
    "path": "./references",
    "skillFiles": [...],
    "agentFiles": [...]
  }
}
```

### **codex/settings.json** (AI Agent配置)
```json
{
  "references": {
    "path": "../Claude-Code-Game-Studios-main/references",
    "skillFiles": [...],
    "agentFiles": [...]
  }
}
```

## 🚀 使用指南

### **对于开发者**

#### 1. 选择合适的Agent
根据项目需求选择合适的agent：
- **Unity项目**: 使用Unity相关agents [1-8, 32-36, 70-74, 76]
- **Godot项目**: 使用Godot相关agents [9-16, 75]
- **Unreal项目**: 使用Unreal相关agents [41-45]
- **Cocos Creator项目**: 使用Cocos Creator相关agents [68, 82]
- **跨平台项目**: 使用跨平台agents [17-64]

#### 2. 配置Agent
```bash
# 启动Agent
# 根据具体的AI Agent工具进行配置

# 使用Agent
@agent-name [parameters]
```

#### 3. 使用技能文件
```bash
# 引用技能文件
@skill-name [parameters]

# 查看技能描述
cat .claude/skills/skill-name/SKILL.md
```

### **对于系统管理员**

#### 1. 维护Agent文件
```bash
# 检查Agent文件完整性
ls -la .claude/agents/

# 验证Agent配置
python -m json.tool .claude/settings.json
```

#### 2. 更新技能文件
```bash
# 添加新技能文件
cp new-skill.md .claude/skills/

# 更新引用配置
# 编辑 .claude/settings.json 添加新技能
```

#### 3. 管理配置
```bash
# 备份配置
cp .claude/settings.json .claude/settings.json.backup

# 恢复配置
cp .claude/settings.json.backup .claude/settings.json
```

### **对于AI Agent用户**

#### 1. 配置AI Agent
```bash
# 创建AI Agent配置
mkdir -p .codex
cp Claude-Code-Game-Studios-main/references/AI_AGENT_SETTINGS_TEMPLATE.json .codex/settings.json

# 自定义配置
# 编辑 .codex/settings.json 根据需要调整配置
```

#### 2. 引用技能和Agent
```bash
# 从AI Agent中引用技能
@skill-name [parameters]

# 从AI Agent中调用Agent
@agent-name [parameters]
```

#### 3. 使用引用系统
```bash
# 验证引用路径
ls ./Claude-Code-Game-Studios-main/references/

# 查看引用文档
cat ./Claude-Code-Game-Studios-main/references/README.md
```

## 🎯 Agent协作

### **协作协议**
- **用户驱动**: 用户驱动的协作模式
- **质量保证**: 所有操作需要用户确认
- **文档完整**: 完整的文档和注释
- **错误处理**: 完善的错误处理机制

### **协作流程**
1. **问题分析** - Agent分析问题和需求
2. **方案提供** - Agent提供解决方案
3. **用户确认** - 用户确认方案
4. **实施执行** - Agent执行方案
5. **质量检查** - 质量检查和验证

### **质量门禁**
- **代码质量**: 95%+代码质量标准
- **文档完整**: 100%文档覆盖率
- **测试覆盖**: 90%+测试覆盖率
- **性能基准**: 目标性能基准

## 📊 性能指标

### **Agent性能**
- **响应时间**: < 2秒标准查询
- **质量验证**: < 5秒质量检查
- **批量处理**: 高效批量操作
- **内存使用**: 优化内存利用

### **系统性能**
- **启动时间**: < 10秒系统启动
- **加载时间**: < 5秒文件加载
- **并发处理**: 支持100+并发
- **错误恢复**: < 30秒错误恢复

## 🔄 维护和更新

### **定期维护**
```bash
# 检查Agent文件
find .claude/agents/ -name "*.md" -exec wc -l {} \;

# 检查技能文件
find .claude/skills/ -name "*.md" -exec wc -l {} \;

# 验证配置文件
python -m json.tool .claude/settings.json
```

### **更新流程**
1. **需求分析** - 分析更新需求
2. **方案设计** - 设计更新方案
3. **实施更新** - 实施更新
4. **测试验证** - 测试和验证
5. **文档更新** - 更新相关文档

### **版本管理**
```bash
# 版本检查
git status
git diff

# 版本提交
git add .
git commit -m "Update agents and skills"
git push
```

## 🎯 故障排除

### **常见问题**
1. **Agent无法启动** - 检查配置文件和权限
2. **技能引用失败** - 验证技能文件路径
3. **配置错误** - 检查JSON格式和语法
4. **权限不足** - 检查文件访问权限

### **调试工具**
```bash
# 检查配置
python -m json.tool .claude/settings.json

# 验证文件
ls -la .claude/agents/ .claude/skills/

# 检查权限
ls -la .claude/
```

### **错误恢复**
```bash
# 重建配置
cp .claude/settings.json.backup .claude/settings.json

# 恢复文件
git checkout .claude/
```

## 📞 支持和帮助

### **获取帮助**
- **文档**: 查阅CLAUDE.md获取详细信息
- **示例**: 参考agent文件了解使用方法
- **模板**: 使用配置模板快速开始

### **报告问题**
- **错误信息**: 提供详细的错误信息
- **环境信息**: 提供系统环境信息
- **复现步骤**: 提供问题复现步骤

---

*.claude目录文档*
*版本: 1.0.0*
*最后更新: 2026-03-10*
*集成: Claude Code Game Studios*
*目标: 核心配置和agent管理*