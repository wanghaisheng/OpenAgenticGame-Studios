# Settings Local Template - Team-Based Architecture

## 🎯 Overview

This template provides a standardized configuration for local Claude Code settings, optimized for the team-based architecture with 79 agents organized into 8 teams.

## 🏗️ Team-Based Configuration

### **Basic Settings**
```json
{
  "model": "claude-3-5-sonnet-20241022",
  "max_tokens": 4096,
  "temperature": 0.7,
  "top_p": 0.9,
  "timeout": 30000
}
```

### **Team Configuration**
```json
{
  "teams": {
    "leadership": {
      "agents": [
        "creative-director",
        "technical-director", 
        "producer",
        "art-director",
        "audio-director",
        "narrative-director",
        "game-vision-architect"
      ],
      "model": "claude-3-5-opus-20240229",
      "max_tokens": 8192
    },
    "programming": {
      "agents": [
        "lead-programmer",
        "gameplay-programmer",
        "engine-programmer",
        "ai-programmer",
        "network-programmer",
        "ui-programmer",
        "tools-programmer"
      ],
      "model": "claude-3-5-sonnet-20241022",
      "max_tokens": 4096
    },
    "design": {
      "agents": [
        "game-designer",
        "systems-designer",
        "level-designer",
        "economy-designer",
        "world-builder",
        "writer",
        "live-ops-designer"
      ],
      "model": "claude-3-5-sonnet-20241022",
      "max_tokens": 4096
    },
    "art": {
      "agents": [
        "technical-artist",
        "ux-designer",
        "accessibility-specialist",
        "sound-designer"
      ],
      "model": "claude-3-5-sonnet-20241022",
      "max_tokens": 4096
    },
    "qa": {
      "agents": [
        "qa-lead",
        "qa-tester",
        "performance-analyst",
        "game-quality-gates-specialist"
      ],
      "model": "claude-3-5-sonnet-20241022",
      "max_tokens": 4096
    },
    "production": {
      "agents": [
        "release-manager",
        "localization-lead",
        "community-manager",
        "analytics-engineer",
        "devops-engineer",
        "security-engineer",
        "prototyper"
      ],
      "model": "claude-3-5-sonnet-20241022",
      "max_tokens": 4096
    },
    "support": {
      "agents": [
        "enhanced-analytics-engineer",
        "enhanced-network-engineer"
      ],
      "model": "claude-3-5-sonnet-20241022",
      "max_tokens": 4096
    },
    "enhanced": {
      "agents": [
        "enhanced-game-designer",
        "enhanced-tool-developer",
        "enhanced-art-director",
        "enhanced-network-engineer"
      ],
      "model": "claude-3-5-sonnet-20241022",
      "max_tokens": 4096
    }
  }
}
```

## 🎮 Engine-Specific Configuration

### **Unity Configuration**
```json
{
  "engines": {
    "unity": {
      "agents": [
        "unity-specialist",
        "unity-dots-specialist",
        "unity-addressables-specialist",
        "unity-shader-specialist",
        "unity-ui-specialist",
        "unity-development-specialist",
        "unity-skills-automation",
        "unity-asset-guidelines-specialist"
      ],
      "model": "claude-3-5-sonnet-20241022",
      "max_tokens": 4096,
      "context": {
        "engine_version": "2022.3",
        "render_pipeline": "URP",
        "target_platforms": ["iOS", "Android", "WebGL"]
      }
    }
  }
}
```

### **Godot Configuration**
```json
{
  "engines": {
    "godot": {
      "agents": [
        "godot-specialist",
        "godot-gdscript-specialist",
        "godot-gdextension-specialist",
        "godot-shader-specialist",
        "godot-full-stack-specialist"
      ],
      "model": "claude-3-5-sonnet-20241022",
      "max_tokens": 4096,
      "context": {
        "engine_version": "4.2",
        "target_platforms": ["Windows", "Linux", "macOS", "Web"]
      }
    }
  }
}
```

### **Unreal Configuration**
```json
{
  "engines": {
    "unreal": {
      "agents": [
        "unreal-specialist",
        "ue-blueprint-specialist",
        "ue-gas-specialist",
        "ue-replication-specialist",
        "ue-umg-specialist"
      ],
      "model": "claude-3-5-sonnet-20241022",
      "max_tokens": 4096,
      "context": {
        "engine_version": "5.3",
        "target_platforms": ["Windows", "Linux", "macOS"]
      }
    }
  }
}
```

### **Cocos Creator Configuration**
```json
{
  "engines": {
    "cocos": {
      "agents": [
        "cocos-creator-specialist",
        "cocos-skills-automation"
      ],
      "model": "claude-3-5-sonnet-20241022",
      "max_tokens": 4096,
      "context": {
        "engine_version": "3.8",
        "target_platforms": ["iOS", "Android", "Web"]
      }
    }
  }
}
```

## 🔧 Skills Configuration

### **Skills Mapping**
```json
{
  "skills": {
    "leadership": [
      "/start",
      "/milestone-review",
      "/project-stage-detect",
      "/setup-engine"
    ],
    "programming": [
      "/code-review",
      "/architecture-decision",
      "/tech-debt",
      "/perf-profile"
    ],
    "design": [
      "/design-review",
      "/balance-check",
      "/brainstorm",
      "/design-systems",
      "/competitive-analysis",
      "/aesthetic-direction",
      "/core-loop-design"
    ],
    "art": [
      "/asset-audit",
      "/ui-ux-design",
      "/accessibility-review"
    ],
    "qa": [
      "/playtest-report",
      "/bug-report",
      "/gate-check",
      "/quality-gates"
    ],
    "production": [
      "/sprint-plan",
      "/prototype",
      "/release-checklist",
      "/changelog",
      "/retrospective",
      "/estimate",
      "/hotfix",
      "/scope-check",
      "/launch-checklist",
      "/patch-notes"
    ]
  }
}
```

## 🔄 Hooks Configuration

### **Hook Settings**
```json
{
  "hooks": {
    "pre-commit": [
      "leadership-validation",
      "code-quality-check",
      "design-validation",
      "asset-validation",
      "quality-gates"
    ],
    "pre-push": [
      "code-review",
      "asset-optimization",
      "automated-testing",
      "performance-checks"
    ],
    "pre-release": [
      "release-readiness",
      "quality-validation",
      "security-checks",
      "performance-validation"
    ]
  }
}
```

## 📊 Quality Gates Configuration

### **Quality Standards**
```json
{
  "quality_gates": {
    "code_quality": {
      "coverage_threshold": 80,
      "complexity_threshold": 10,
      "duplication_threshold": 3
    },
    "performance": {
      "fps_threshold": 60,
      "memory_threshold": 512,
      "load_time_threshold": 3
    },
    "security": {
      "vulnerability_threshold": 0,
      "scan_frequency": "daily"
    }
  }
}
```

## 🎯 Context Management

### **Context Settings**
```json
{
  "context": {
    "max_context_size": 200000,
    "context_retention": "7d",
    "context_compression": true,
    "context_prioritization": {
      "leadership": "high",
      "programming": "medium",
      "design": "medium",
      "art": "medium",
      "qa": "high",
      "production": "medium"
    }
  }
}
```

## 📋 References Configuration

### **Reference Paths**
```json
{
  "references": {
    "path": "./refenrece",
    "skillFiles": [
      "game-design/SKILL.md",
      "unity/SKILL.md",
      "godot/SKILL.md",
      "cocos-creator/SKILL.md",
      "quality-assurance/SKILL.md",
      "competitive-analysis/SKILL.md",
      "development-tools/SKILL.md"
    ],
    "agentFiles": [
      "leadership/creative-director.md",
      "leadership/technical-director.md",
      "leadership/producer.md",
      "programming/lead-programmer.md",
      "design/game-designer.md",
      "art/technical-artist.md",
      "qa/qa-lead.md",
      "production/release-manager.md"
    ]
  }
}
```

## 🔧 Development Environment

### **Environment Settings**
```json
{
  "environment": {
    "development_mode": true,
    "debug_mode": false,
    "logging_level": "info",
    "cache_enabled": true,
    "parallel_processing": true
  }
}
```

## 🎨 UI/UX Settings

### **Interface Configuration**
```json
{
  "ui": {
    "theme": "dark",
    "font_size": 14,
    "line_height": 1.6,
    "code_theme": "github-dark",
    "auto_save": true,
    "auto_complete": true
  }
}
```

## 📈 Analytics and Monitoring

### **Monitoring Settings**
```json
{
  "monitoring": {
    "performance_tracking": true,
    "usage_analytics": true,
    "error_reporting": true,
    "metrics_collection": true
  }
}
```

## 🔒 Security Settings

### **Security Configuration**
```json
{
  "security": {
    "encryption_enabled": true,
    "access_control": true,
    "audit_logging": true,
    "data_protection": true
  }
}
```

## 📝 Customization Guidelines

### **Team-Specific Customization**
1. **Model Selection**: Choose appropriate model for each team
2. **Token Limits**: Set appropriate token limits for team complexity
3. **Context Size**: Adjust context size based on team requirements
4. **Quality Gates**: Customize quality gates for team standards

### **Engine-Specific Customization**
1. **Engine Version**: Update engine versions as needed
2. **Target Platforms**: Adjust target platforms for project
3. **Engine Features**: Enable/disable engine-specific features
4. **Performance Requirements**: Set engine-specific performance targets

### **Project-Specific Customization**
1. **Project Scale**: Adjust settings based on project size
2. **Team Size**: Optimize settings for team size
3. **Complexity**: Adjust settings for project complexity
4. **Requirements**: Customize for specific project requirements

---

*Settings Local Template Updated*
*Version: 2.0.0*
*Update Date: 2026-03-10*
*Organization: Team-Based Structure*