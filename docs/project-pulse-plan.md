# Project Pulse dashboard implementation plan

## Goal

Create a runnable, responsive Project Pulse dashboard that gives Mona a clear
at-a-glance view of every project's owner, status, priority, and recent
activity. The dashboard must load project data from JSON, present it in
accessible project cards, and run directly from VS Code.

## Implementation phases

1. **Define the contract and experience:** The Designer establishes the
   information hierarchy, visual direction, accessibility requirements, and CSS
   hooks. The Coder defines the project-data schema and launch approach.
2. **Build the dashboard assets:** The Coder creates the JSON data and
   data-driven HTML structure. The Designer implements the responsive visual
   system in the stylesheet against the agreed hooks.
3. **Integrate the runnable experience:** The Coder connects data loading,
   rendering, error handling, and the VS Code launch configuration.
4. **Validate the completed dashboard:** Verify the data and configuration,
   rendering, responsive accessibility, and launch behavior as an integrated
   application.

## Scope and file assignments

| File | Owner | Responsibility |
| --- | --- | --- |
| `app/project-data.json` | Coder | Define valid JSON with a top-level `projects` array. Each project supplies `name`, `owner`, `status`, `recentActivity`, and `priority`. |
| `app/index.html` | Coder | Build the dashboard markup, load `styles.css` and `project-data.json`, render one `.project-card` per project, and expose every required project field. |
| `app/styles.css` | Designer | Define the visual system, responsive layout, accessible contrast and focus states, project-card treatment, status badges, priority treatment, and stable CSS hooks. |
| `.vscode/launch.json` | Coder | Add a strict JSON VS Code launch configuration named `Run Project Pulse Dashboard` that serves `app/` and opens `index.html`. |

## Responsibilities

**Designer:** Establish the dashboard's information hierarchy and responsive behavior before implementation. Provide the visual and accessibility direction for cards, project status, priority, recent activity, typography, spacing, colors, keyboard focus, and small-screen layouts. Implement the approved presentation in `app/styles.css` using the CSS hooks consumed by the markup.

**Coder:** Define the data contract and populate `app/project-data.json`; implement the HTML structure and data-driven rendering in `app/index.html`; and add the launch configuration. Preserve the Designer's agreed CSS hooks, provide visible labels rather than color-only status or priority indicators, and surface fetch or parsing failures explicitly in the dashboard.

## Dependencies and sequencing

1. The Designer establishes the information hierarchy and CSS-hook requirements, while the Coder defines the JSON schema and launch configuration.
2. `app/project-data.json` must be complete before the Coder finalizes data loading and rendering in `app/index.html`.
3. The approved markup hooks from `app/index.html` must be available before the Designer finalizes `app/styles.css`.
4. Integration follows completion of the markup, data, styles, and launch configuration. Validation occurs only after the integrated dashboard is available.

## Parallel work decisions

- The Designer's design direction can proceed in parallel with the Coder's data-schema definition and `.vscode/launch.json` implementation.
- Once the data contract and CSS-hook requirements are agreed, the Coder may implement `app/project-data.json` and the HTML structure while the Designer implements visual styles.
- Data-driven rendering cannot be finalized until the data contract is complete, and final styling cannot be finalized until the markup hooks are present.
- Integration testing is sequential because it requires all four assigned files.

## Validation expectations

- Parse `app/project-data.json` and `.vscode/launch.json` as strict JSON.
- Confirm `app/index.html` references `app/styles.css` and `app/project-data.json`, creates `.project-card` elements, and visibly presents name, owner, status, recent activity, and priority for each project.
- Confirm the page handles data-fetch and JSON-parsing errors explicitly rather than silently displaying an empty dashboard.
- Review the dashboard at desktop and narrow viewport widths for readable hierarchy, usable card layout, sufficient contrast, visible keyboard focus, and text or icon labels that do not rely only on color.
- Run **Run Project Pulse Dashboard** in VS Code and confirm it serves `app/` and opens `index.html`, rather than showing a directory listing.
