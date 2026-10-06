# second-brain-plugin

A personal Claude plugin for managing project context in `~/second_brain`, organized as one Obsidian-friendly folder per project.

## Commands
- `/start-project`
- `/load-project`
- `/update-project`
- `/recap-project`

## Managed project structure
Each project is stored under `~/second_brain/projects/<slug>/` with:
- `overview.md`
- `current.md`
- `tasks.md`
- `decisions.md`
- `resources.md`
- `plans/`
- `sessions/`

`tasks.md` uses the stable sections `Todo`, `Doing`, `Blocked`, and `Done` with markdown checkbox items: `- [ ]` for incomplete tasks and `- [x]` for completed tasks.

`plans/implementation-plan.md` stores the latest implementation plan copy for the project when a plan is generated or updated.

## Project selection
Existing folders in `~/second_brain/projects/` are the source of truth for project selection.

- `/load-project`, `/recap-project`, and `/update-project` operate only on existing managed projects.
- When no project is provided, commands should list existing projects and ask the user to choose.
- Session context may help rank likely matches, but it must not invent a new slug.
- `/start-project` is the only command that may create a new project folder.

## Architecture
This plugin is intentionally markdown-first and script-free.

The commands operate directly on markdown files in `~/second_brain/projects/<slug>/` using Claude-native file tools instead of Node or TypeScript helper scripts.
