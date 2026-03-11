---
paths:
  - "src/networking/**"
  - "src/multiplayer/**"
---

# Network Code Rules - Team-Based Architecture

## 🏗️ Team Responsibilities

### **Primary Team**: Programming Team
- **Lead Agent**: `network-programmer`
- **Contributors**: `lead-programmer`, `engine-programmer`
- **QA Team**: `qa-lead`, `qa-tester`
- **Security Team**: `security-engineer`

### **Cross-Team Integration**
- **Production Team**: `producer` (network milestone coordination)
- **DevOps Team**: `devops-engineer` (network infrastructure)
- **Support Team**: `enhanced-network-engineer` (advanced networking)

## 🌐 Core Network Rules

### **Security Rules**
- Server is AUTHORITATIVE for all gameplay-critical state — never trust the client
- All network messages must be versioned for forward/backward compatibility
- Client predicts locally, reconciles with server — implement rollback for mispredictions
- Handle disconnection, reconnection, and host migration gracefully
- Rate-limit all network logging to prevent log flooding
- All networked values must specify replication strategy: reliable/unreliable, frequency, interpolation
- Bandwidth budget: define and track per-message-type bandwidth usage
- Security: validate all incoming packet sizes and field ranges

### **Team Coordination**
- Network features must be coordinated with Production Team
- Network security must be coordinated with Security Team
- Network infrastructure must be coordinated with DevOps Team
- Network performance must be coordinated with Performance Analyst
- Network testing must be coordinated with QA Team

## 🔧 Technical Rules

### **Code Organization**
- Use clear separation of concerns between network systems
- Implement proper network architecture patterns
- Use consistent naming conventions for network components
- Implement proper error handling and logging
- Use object pooling for network objects when appropriate

### **Performance Rules**
- Profile all network systems for performance
- Optimize critical network update paths
- Use efficient network algorithms and data structures
- Implement proper memory management for network systems
- Monitor network system performance in real-time

### **Security Rules**
- Validate all network inputs and data
- Implement proper network security practices
- Use secure coding practices for network code
- Implement proper network memory management
- Validate all network state changes

## 🌐 Network Architecture

### **Client-Server Architecture**
- Implement proper client-server separation
- Use authoritative server model for gameplay state
- Implement client-side prediction for responsiveness
- Use server reconciliation for consistency
- Implement proper network synchronization

### **Network Protocols**
- Use standardized network protocols
- Implement proper message serialization
- Use network compression where appropriate
- Implement proper network error handling
- Use secure network communication

### **Data Synchronization**
- Implement proper data synchronization strategies
- Use delta compression for network efficiency
- Implement proper conflict resolution
- Use interpolation for smooth network updates
- Implement proper network rollback mechanisms

## 🎮 Multi-Engine Support

### **Unity Network Rules**
- Use Unity's Netcode for GameObject synchronization
- Implement proper Unity network architecture
- Use Unity's network optimization features
- Support Unity's multiplayer services
- Optimize network performance for Unity

### **Godot Network Rules**
- Use Godot's network system for multiplayer
- Implement proper Godot network architecture
- Use Godot's RPC system for network calls
- Support Godot's network optimization features
- Optimize network performance for Godot

### **Unreal Network Rules**
- Use Unreal's replication system for network
- Implement proper Unreal network architecture
- Use Unreal's network optimization features
- Support Unreal's multiplayer services
- Optimize network performance for Unreal

### **Cocos Network Rules**
- Implement proper network architecture for web
- Use WebSocket or HTTP for network communication
- Implement proper network optimization for web
- Support web multiplayer features
- Optimize network performance for web

## 🔒 Security Integration

### **Security Requirements**
- Implement network security as specified by Security Team
- Use secure coding practices for network code
- Implement proper network authentication and authorization
- Use secure communication protocols
- Test network security with Security Team

### **Security Testing**
- Test network security vulnerabilities
- Test network attack vectors
- Test network security measures
- Test network security with Security Team
- Document network security issues

## 🧪 Testing Requirements

### **Unit Testing**
- Write unit tests for all network logic
- Test network systems with mock data
- Test network systems with different configurations
- Test edge cases and error conditions
- Test network systems in isolation

### **Integration Testing**
- Test network systems integration with other systems
- Test network systems with real data
- Test network systems under load
- Test network systems with different configurations
- Test network systems with different platforms

### **Performance Testing**
- Test network systems performance under load
- Test network systems with different player counts
- Test network systems with different network conditions
- Test network systems with different environments
- Test network systems with different platforms

## 📊 Performance Requirements

### **Performance Budgets**
- **Network Update Time**: < 5ms per frame
- **Network Memory Usage**: < 200MB for network systems
- **Network CPU Usage**: < 30% of available CPU
- **Network Bandwidth**: < 100KB/s per client

### **Performance Monitoring**
- Monitor network system performance in real-time
- Profile network systems regularly
- Log network performance violations and issues
- Alert on performance budget violations
- Generate network performance reports

## 📝 Documentation Requirements

### **Code Documentation**
- Document all network systems with examples
- Document network system interfaces
- Document network system dependencies
- Document network system limitations
- Document troubleshooting guides

### **Network Documentation**
- Document network architecture decisions
- Document network protocol specifications
- Document network security measures
- Document network performance characteristics
- Document network troubleshooting guides

## 🔄 Quality Gates

### **Pre-Implementation Gates**
- [ ] Design is reviewed and approved by `network-programmer`
- [ ] Security requirements are defined
- [ ] Performance requirements are defined
- [ ] Testing requirements are defined
- [ ] Infrastructure requirements are defined

### **Implementation Gates**
- [ ] Code follows network coding standards
- [ ] Security requirements are met
- [ ] Performance requirements are met
- [ ] Infrastructure requirements are met
- [ ] Tests are written and passing

### **Pre-Release Gates**
- [ ] All network systems are secure
- [ ] All network systems are performant
- [ ] All network systems are reliable
- [ ] All network systems are documented
- [ ] All network systems are tested

## 🚀 Examples

### **Correct** (authoritative server):

#### Server Authority Example
```gdscript
# Server authoritative state management
func _process_client_input(player_id: int, input: Dictionary) -> void:
    # Validate input
    if not _validate_input(input):
        return
    
    # Update authoritative state
    _update_player_state(player_id, input)
    
    # Broadcast state to all clients
    _broadcast_state_update()
```

#### Client Prediction Example
```gdscript
# Client prediction with reconciliation
func _process_input(input: Dictionary) -> void:
    # Predict local state
    _predicted_state = _predict_state(input)
    _apply_predicted_state(_predicted_state)
    
    # Send input to server
    _send_input_to_server(input)
    
    # Reconcile with server state
    _reconcile_with_server()
```

### **Incorrect** (client authority):

#### Client Authority Example
```gdscript
# VIOLATION: Client authoritative state
func _process_input(input: Dictionary) -> void:
    # VIOLATION: Directly update game state
    player.health = input.health
    player.score = input.score
    
    # VIOLATION: Broadcast state to other clients
    _broadcast_state_to_clients()
```

## 📋 Checklist

### **Development Checklist**
- [ ] Server is authoritative for gameplay state
- [ ] Network messages are versioned
- [ ] Client prediction is implemented
- [ ] Network security is implemented
- [ ] Performance requirements are met

### **Review Checklist**
- [ ] Code reviewed by `network-programmer`
- [ ] Security reviewed by `security-engineer`
- [ ] Performance reviewed by `performance-analyst`
- [ ] Infrastructure reviewed by `devops-engineer`
- [ ] QA reviewed by `qa-lead`

---

*Network Code Rules Updated*
*Version: 2.0.0*
*Update Date: 2026-03-10*
*Teams: Programming Team, Security Team*
*Integration: Production Team, DevOps Team, Support Team*
*Engines: Unity, Godot, Unreal, Cocos Creator*