# C2L PUA — 高效激勵引擎 for Claude Code

Exhaustive problem-solving plugin with corporate PUA pressure escalation. Triggers on repeated failures, giving-up behavior, passive debugging, or user frustration.

## Features

- **Three Iron Rules** — exhaust all options, investigate before asking, proactively extend work
- **Pressure Escalation** — L1 → L4 based on failure count
- **Universal Methodology** — 5-step systematic approach for any stuck pattern
- **Auto PUA Flavor Selection** — Alibaba, ByteDance, Huawei, Tencent, Meituan, Netflix, Musk, Jobs, NEU styles
- **Proactivity Enforcement** — passive = 3.25, proactive = 3.75

## Installation

### 1. Add marketplace

```bash
claude plugins marketplace add github:hulion/nextpua
```

### 2. Install plugin

```bash
claude plugins install c2l@nextpua
```

### 3. Restart Claude Code

Restart your Claude Code session to activate the plugin.

## Usage

```
/c2l:pua
```

This activates PUA mode for the current session.

## Update

```bash
claude plugins marketplace update nextpua
claude plugins update c2l@nextpua
```

## Uninstall

```bash
claude plugins uninstall c2l@nextpua
```

## License

MIT
