# Coding Standards - Team-Based Architecture

## 🎯 Overview

These coding standards apply to all teams and agents in the Claude Code Game Studios architecture. Standards are organized by team responsibility and engine specialization.

## 👑 Leadership Team Standards

### **Code Architecture**
- All major architectural decisions must be documented with `/architecture-decision`
- Technical director must approve all system-level changes
- Lead programmer must review all code architecture changes

### **Quality Gates**
- All code must pass quality gates before release
- Performance requirements must be met for all systems
- Security standards must be followed for all network code

## 💻 Programming Team Standards

### **General Standards**
- **Code Style**: Follow language-specific conventions
- **Documentation**: All public APIs must be documented
- **Testing**: All code must have corresponding tests
- **Performance**: Code must meet performance benchmarks

### **Unity Standards**
- **C# Conventions**: Follow Microsoft C# coding conventions
- **Unity Patterns**: Use established Unity design patterns
- **DOTS**: Follow DOTS/ECS best practices for performance-critical code
- **Assets**: Follow Unity asset guidelines and naming conventions

### **Godot Standards**
- **GDScript**: Follow GDScript style guide
- **Node Structure**: Use proper node hierarchy and naming
- **Signals**: Use signals for loose coupling
- **Resources**: Follow Godot resource management best practices

### **Unreal Standards**
- **C++ Conventions**: Follow Epic C++ coding standards
- **Blueprint**: Follow Blueprint development standards
- **GAS**: Use Gameplay Ability System consistently
- **Performance**: Follow Unreal performance guidelines

### **Cocos Creator Standards**
- **TypeScript**: Follow TypeScript coding conventions
- **Components**: Use component-based architecture
- **Naming**: Follow Cocos Creator naming conventions
- **Performance**: Optimize for web and mobile platforms

## 🎨 Design Team Standards

### **Design Documentation**
- All design documents must be reviewed by game-designer
- Use standardized templates for design specifications
- Include performance requirements in design documents
- Document all design decisions and rationale

### **Code Implementation**
- Design code must be readable and maintainable
- Use design patterns appropriate for game systems
- Include comprehensive comments for complex algorithms
- Follow team-specific coding standards

## 🎭 Art Team Standards

### **Technical Art**
- Shaders must be optimized for target platforms
- Use consistent naming conventions for assets
- Follow art pipeline standards and workflows
- Document technical art decisions and implementations

### **UI/UX Code**
- UI code must be accessible and responsive
- Follow platform-specific UI guidelines
- Use consistent styling and theming
- Test UI across different screen sizes and devices

## 🔍 Quality Assurance Team Standards

### **Testing Standards**
- All code must have unit tests
- Integration tests must cover critical workflows
- Performance tests must validate requirements
- Security tests must cover potential vulnerabilities

### **Bug Reporting**
- Use standardized bug report templates
- Include all required information in bug reports
- Prioritize bugs based on severity and impact
- Track bugs through to resolution

## 🏭 Production Team Standards

### **Build Standards**
- All builds must be reproducible
- Use automated build pipelines where possible
- Include build artifacts in version control
- Document build processes and dependencies

### **Release Standards**
- All releases must pass quality gates
- Use semantic versioning for releases
- Include comprehensive release notes
- Test releases across all target platforms

## 🛠️ Support Team Standards

### **Code Quality**
- All code must meet quality benchmarks
- Use static analysis tools where available
- Follow security best practices
- Document all technical decisions

### **Performance Standards**
- Code must meet performance requirements
- Profile and optimize performance bottlenecks
- Monitor performance in production
- Document performance optimizations

## ⚡ Enhanced Team Standards

### **Advanced Development**
- Use advanced development patterns and practices
- Implement complex systems with proper architecture
- Follow enterprise-level coding standards
- Document advanced implementations thoroughly

## 🔄 Cross-Team Standards

### **Code Reviews**
- All code changes must be reviewed
- Use standardized code review checklists
- Include performance and security considerations
- Document all review decisions

### **Documentation**
- All code must be documented
- Use standardized documentation templates
- Include examples and usage instructions
- Keep documentation up to date

## 📊 Quality Metrics

### **Code Quality**
- **Coverage**: Minimum 80% test coverage
- **Complexity**: Maintain acceptable cyclomatic complexity
- **Performance**: Meet defined performance benchmarks
- **Security**: Pass security vulnerability scans

### **Documentation Quality**
- **Completeness**: All APIs documented
- **Accuracy**: Documentation matches implementation
- **Clarity**: Documentation is clear and understandable
- **Maintenance**: Documentation is kept current

## 🎯 Engine-Specific Guidelines

### **Unity Guidelines**
- Use Unity best practices for performance
- Follow Unity asset optimization guidelines
- Use Unity-specific design patterns
- Optimize for target platforms

### **Godot Guidelines**
- Use Godot best practices for performance
- Follow Godot asset management guidelines
- Use Godot-specific design patterns
- Optimize for web and mobile platforms

### **Unreal Guidelines**
- Use Unreal best practices for performance
- Follow Unreal asset optimization guidelines
- Use Unreal-specific design patterns
- Optimize for high-end platforms

### **Cocos Creator Guidelines**
- Use Cocos Creator best practices for performance
- Follow Cocos asset optimization guidelines
- Use Cocos-specific design patterns
- Optimize for web and mobile platforms

## 🔧 Development Tools

### **Required Tools**
- **Version Control**: Git with proper branching strategy
- **Code Editor**: IDE with appropriate plugins
- **Static Analysis**: Language-specific tools
- **Testing**: Unit testing framework

### **Recommended Tools**
- **Profiling**: Performance profiling tools
- **Documentation**: Documentation generation tools
- **Build**: Automated build systems
- **Quality**: Code quality analysis tools

## 📋 Code Review Checklist

### **General**
- [ ] Code follows team standards
- [ ] Code is properly documented
- [ ] Code has appropriate tests
- [ ] Code meets performance requirements
- [ ] Code follows security best practices

### **Team-Specific**
- [ ] Leadership: Architecture decisions documented
- [ ] Programming: Code style and conventions followed
- [ ] Design: Design patterns used appropriately
- [ ] Art: Technical art standards followed
- [ ] QA: Testing standards met
- [ ] Production: Build and release standards followed

---

*Coding Standards Updated*
*Version: 2.0.0*
*Update Date: 2026-03-10*
*Organization: Team-Based Structure*
*Total Teams: 8*