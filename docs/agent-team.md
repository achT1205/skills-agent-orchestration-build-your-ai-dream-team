# Agent team

Mona's Project Pulse dashboard will be built by a coordinated team of custom
agents, orchestrated through GitHub Copilot CLI in a Codespace:

| Agent | Target model | Responsibility | Definition |
| --- | --- | --- | --- |
| Orchestrator | Claude Opus 4.7 (copilot) | Breaks dashboard work into phases, delegates scoped tasks to the specialists, coordinates dependencies, and verifies the integrated result without implementing features directly. | [`.github/agents/orchestrator.agent.md`](../.github/agents/orchestrator.agent.md) |
| Planner | Claude Opus 4.7 (copilot) | Researches the repository and relevant documentation, then produces an implementation plan covering file ownership, dependencies, parallel work, risks, edge cases, validation, and open questions. | [`.github/agents/planner.agent.md`](../.github/agents/planner.agent.md) |
| Designer | Gemini 3.1 Pro (copilot) | Defines the dashboard's UI/UX, accessibility, information hierarchy, responsive behavior, and visual styling—including project cards, status badges, priority treatment, and deterministic CSS hooks. | [`.github/agents/designer.agent.md`](../.github/agents/designer.agent.md) |
| Coder | GPT-5.5 (copilot) | Implements scoped application logic and support configuration with explicit errors, predictable structure, and testable behavior; for the runnable dashboard, this can include its VS Code launch configuration. | [`.github/agents/coder.agent.md`](../.github/agents/coder.agent.md) |

The Orchestrator obtains the technical plan first, assigns non-overlapping work
in parallel where dependencies allow, sequences dependent work, and keeps file
ownership explicit so the Project Pulse dashboard comes together cleanly.
