# yakik-dev-toolkit

Specialized development agents for Claude Code organized by domain.

## Agents

### Architecture (green)
| Agent | Model | Description |
|-------|-------|-------------|
| backend-architect | sonnet | Backend systems, APIs, databases, security |
| frontend-architect | sonnet | UI, accessibility, performance, responsive design |
| system-architect | sonnet | System architecture, scalability, patterns |

### Research (yellow)
| Agent | Model | Description |
|-------|-------|-------------|
| deep-research-agent | opus | Comprehensive research, evidence synthesis |
| requirements-analyst | sonnet | Requirements discovery, PRDs, scope definition |
| tech-stack-researcher | sonnet | Technology choices, package recommendations |

### Quality (red)
| Agent | Model | Description |
|-------|-------|-------------|
| performance-engineer | sonnet | Profiling, optimization, benchmarking |
| refactoring-expert | sonnet | Code quality, technical debt, SOLID principles |
| security-engineer | sonnet | Vulnerability assessment, threat modeling |

### Communication (pink)
| Agent | Model | Description |
|-------|-------|-------------|
| learning-guide | haiku | Concept explanation, tutorials, learning paths |
| technical-writer | sonnet | API docs, user guides, specifications |

## Commands

- `/dev` — Orchestrator that analyzes tasks and delegates to the right specialist agent
