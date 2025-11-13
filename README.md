# Claude-ADB-Workspace-Template

A version-controlled workspace template for managing Android devices through ADB with Claude Code.

## Overview

This template provides a structured environment for Android device management, optimization, and forensics using ADB (Android Debug Bridge) with AI-assisted workflows through Claude Code.

## Features

- **Device Setup**: Automated device profiling and manifest creation
- **Package Management**: Track, analyze, and manage installed applications
- **Device Optimization**: Identify and remove bloatware, optimize performance
- **Diagnostics**: Comprehensive device health monitoring
- **Historical Tracking**: Version-controlled logs and package lists
- **Forensics**: Detailed logging of all operations and changes

## Quick Start

1. **Clone this template** for your Android device
2. **Connect your device** via ADB with USB debugging enabled
3. **Run setup**: `/setup` - Automatically profiles your device and creates manifest
4. **Start managing**: Use slash commands and agents to optimize and maintain your device

## Available Commands

### Slash Commands

- `/setup` - Initial device probe and configuration
- `/export-packages` - Export current package lists with timestamps
- `/diagnostics` - Run comprehensive device health diagnostics

### Agents

- **device-optimizer** - Bloatware removal and performance optimization
- **package-manager** - Detailed package analysis and management

## Repository Structure

```
├── manifest/          # Device specifications and parameters
│   └── device.json    # Auto-generated device profile
├── packages/          # Timestamped package lists
│   ├── initial-packages-*.txt
│   └── packages-*.txt
├── forensics/         # Diagnostic logs and operation records
└── .claude/           # Claude Code commands and agents
    ├── commands/      # Slash command definitions
    └── agents/        # Agent configurations
```

## Prerequisites

- ADB installed and on PATH
- USB debugging enabled on Android device
- Claude Code CLI

## Safety Features

- Risk categorization (green/yellow/red) for all operations
- Backup and documentation before changes
- Rollback instructions for all operations
- Historical tracking of all modifications

## Use Cases

- Remove manufacturer bloatware
- Optimize device performance
- Track application changes over time
- Debug device issues
- Prepare devices for specific use cases
- Security auditing and hardening
- Battery and performance optimization

## License

Private workspace template - customize as needed for your devices.