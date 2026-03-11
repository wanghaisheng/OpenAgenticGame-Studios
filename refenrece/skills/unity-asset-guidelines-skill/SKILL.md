---
name: unity-asset-guide
description: Use when writing Unity package code (FEEL, SOAP, DOTween), debugging package-related issues, or checking best practices before implementation.
argument-hint: "[package]"
user-invocable: true
---

# Unity Assets Guidelines

Best practices and pitfalls for Unity packages used in this project.

## Available Packages

| Package | Description | Status |
|---------|-------------|--------|
| soap | Scriptable Object Architecture | ✅ |
| feel | MMFeedbacks feedback system | ✅ |
| dotween | Tween animation | 🚧 Coming soon |

## Instructions

If argument provided (`$ARGUMENTS`):
1. Read `./docs/$ARGUMENTS/patterns.md` for usage patterns
2. Read `./docs/$ARGUMENTS/pitfalls.md` for checklist and troubleshooting
3. If debugging specific issue, check detailed files in `./docs/$ARGUMENTS/pitfalls/`

If no argument provided:
- Display available packages list above
