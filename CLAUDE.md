# Memory Bank

Memory resets completely between sessions. At the start of every task, read ALL memory bank files to understand the project and continue work effectively — this is not optional.

## Memory Bank Structure

The Memory Bank consists of core files and optional context files, all in Markdown format. Files build upon each other in a clear hierarchy:

flowchart TD
PB[projectbrief.md] --> PC[productContext.md]
PB --> SP[systemPatterns.md]
PB --> TC[techContext.md]

    PC --> AC[activeContext.md]
    SP --> AC
    TC --> AC

    AC --> P[progress.md]

### Core Files (Required)
1. `projectbrief.md`
    - Foundation document that shapes all other files
    - Created at project start if it doesn't exist
    - Defines core requirements and goals
    - Source of truth for project scope

2. `productContext.md`
    - Why this project exists
    - Problems it solves
    - How it should work
    - User experience goals

3. `activeContext.md`
    - Current work focus
    - Recent changes
    - Next steps
    - Active decisions and considerations
    - Important patterns and preferences
    - Learnings and project insights

4. `systemPatterns.md`
    - System architecture
    - Key technical decisions
    - Design patterns in use
    - Component relationships
    - Critical implementation paths

5. `techContext.md`
    - Technologies used
    - Development setup
    - Technical constraints
    - Dependencies
    - Tool usage patterns

6. `progress.md`
    - What works
    - What's left to build
    - Current status
    - Known issues
    - Evolution of project decisions

### Additional Context
Create additional files/folders within memory-bank/ when they help organize:
- Complex feature documentation
- Integration specifications
- API documentation
- Testing strategies
- Deployment procedures

## Core Workflows

### Plan Mode
flowchart TD
Start[Start] --> ReadFiles[Read Memory Bank]
ReadFiles --> CheckFiles{Files Complete?}

    CheckFiles -->|No| Plan[Create Plan]
    Plan --> Document[Document in Chat]

    CheckFiles -->|Yes| Verify[Verify Context]
    Verify --> Strategy[Develop Strategy]
    Strategy --> Present[Present Approach]

### Act Mode
flowchart TD
Start[Start] --> Context[Check Memory Bank]
Context --> Update[Update Documentation]
Update --> Execute[Execute Task]
Execute --> Document[Document Changes]

## Documentation Updates

Memory Bank updates occur when:
1. Discovering new project patterns
2. After implementing significant changes
3. When user requests with **update memory bank** (MUST review ALL files)
4. When context needs clarification

flowchart TD
Start[Update Process]

    subgraph Process
        P1[Review ALL Files]
        P2[Document Current State]
        P3[Clarify Next Steps]
        P4[Document Insights & Patterns]

        P1 --> P2 --> P3 --> P4
    end

    Start --> Process

Note: When triggered by **update memory bank**, I MUST review every memory bank file, even if some don't require updates. Focus particularly on activeContext.md and progress.md as they track current state.

Memory Bank is the only link to previous work. It must be maintained with precision and clarity.

## TOON instead of JSON

From now on, we will NOT use JSON for storing structured data.

We will store all structured data in TOON format.

Rules:
- Convert any JSON structures into TOON tables
- Prefer compact tabular representations
- Use headers like: users[3]{id,name,role}
- Each following line is one record
- Avoid unnecessary text, focus on structure
- Always output valid TOON instead of JSON

If I provide JSON, first convert it to TOON. If you need to create new structured data, create it directly in TOON format.

## Screenshot folder

All screenshots are always located in the system Downloads directory.

Whenever you need to find, reference, open or analyze a screenshot:
- first look in the Downloads folder
- assume screenshots are saved there by default
- prefer the most recent files in Downloads when the exact name is not specified

If a screenshot name is ambiguous or missing, list recent screenshot files from Downloads and ask me to confirm the correct one.

## Commits

Never add any AI self-references to commits.

Do NOT include:
- "Generated with Claude"
- "Co-authored-by"
- links to AI tools
- any meta commentary

When creating commits:
- use conventional commits only
- keep messages short and professional
- DO NOT mention assistants, LLMs, AI tools, or Anthropic

## Plugins

On session start:
1. Ensure local marketplace is registered: `claude plugin marketplace add ~/.claude/plugins/local` (safe to run if already registered)
2. Check installed plugins (`claude plugin list`) against `~/.claude/required-plugins.txt`. Install any missing ones with `claude plugin install <name>`.

When installing a new plugin via `claude plugin install`, also add its name to `~/.claude/required-plugins.txt` to keep the list in sync across devices.

## Specialist Agents (yakik-dev-toolkit)

Delegate to specialist agents via Task tool proactively — not only for complex tasks, but also for medium-complexity ones (new components, multi-file changes, UI interactions, refactoring). It's better to get it right on the first iteration than to fix mistakes across multiple rounds.

**Delegate when**: new UI components, drag-and-drop or interactive features, multi-file changes, architecture decisions, research, audits, anything where domain expertise reduces iterations. **Don't delegate when**: quick one-liner fix, simple question, obvious single-file change.

| Agent | subagent_type | Use for |
|-------|---------------|---------|
| Backend Architect | `backend-architect` | API design, DB schemas, auth, reliability |
| Frontend Architect | `frontend-architect` | Components, a11y, Core Web Vitals, responsive |
| System Architect | `system-architect` | Cross-system architecture, scalability, migrations |
| Deep Research | `deep-research-agent` | Multi-source research, investigation, unknowns |
| Requirements | `requirements-analyst` | PRDs, scope, stakeholder analysis |
| Tech Stack | `tech-stack-researcher` | Technology comparisons, package selection |
| Performance | `performance-engineer` | Profiling, bottlenecks, optimization |
| Refactoring | `refactoring-expert` | Large-scale code quality, tech debt, SOLID |
| Security | `security-engineer` | Vulnerability audit, threat modeling, compliance |
| Learning | `learning-guide` | Teaching concepts, tutorials, explanations |
| Docs | `technical-writer` | API docs, guides, specifications |
| QA Visual | `qa-visual-tester` | Visual verification, Playwright browser testing |

**QA Visual:** Use `qa-visual-tester` only when explicitly requested. Do NOT run it automatically after UI tasks.

## MCP

Always use Context7 MCP when I need library/API documentation, code generation, setup or configuration steps without me having to explicitly ask.

