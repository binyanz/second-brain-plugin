---
name: start-project
description: Create or complete an Obsidian-friendly project context under ~/second_brain/projects/<slug>
argument-hint: <existing-project-slug | new-project-name>
allowed-tools: [Bash, Read, Write]
---

# Start Project

The user invoked this with: $ARGUMENTS

## Goal
Create a managed project folder under `~/second_brain/projects/<slug>/` with canonical markdown files and folders:
- `overview.md`
- `current.md`
- `tasks.md`
- `decisions.md`
- `resources.md`
- `plans/`
- `sessions/`

## Instructions
1. Determine the target project before doing any file operations:
   - First inspect `~/second_brain/projects/` and treat existing folder names as the source of truth.
   - If the user provided a project name or slug, first match it against existing project folders.
   - If it matches an existing folder, use that exact folder name as the slug.
   - If it does not match an existing folder, this is the only skill that may normalize and create a new slug.
   - If no project was provided, offer a short list of existing project folders and ask the user to choose one or provide a new project name.
   - Do not derive a new slug from the active repo, working directory, or other session context.
2. Resolve the project slug directly in the conversation:
   - for an existing project, use the exact existing folder name
   - for a new project, normalize the provided name by:
     - lowercase
     - trim whitespace
     - replace spaces, underscores, and slashes with `-`
     - collapse repeated `-`
     - strip leading and trailing `-`
3. Set the project directory to `~/second_brain/projects/<slug>`.
4. Use Bash only for simple directory creation and read-only directory listing: create the project directory plus `plans/` and `sessions/` with `mkdir -p`.
5. Preserve all existing files. Create only missing canonical files and folders.
6. When creating files, write clean Obsidian-friendly markdown directly. Use these canonical shapes:

### `overview.md`
```md
# <Project Title>

## What this project is

## Goal

## Scope
- 

## Source
- Repo:
- Working path:
- Context path: [[current]]

## Key environments
- Claude Code
- Obsidian vault at `~/second_brain`

## Related notes
- [[current]]
- [[tasks]]
- [[decisions]]
- [[resources]]
```

### `current.md`
```md
# Current

## Now

## Next

## Blockers

## Open questions

## Recent updates
- <today>: Project initialized.

## Related notes
- [[overview]]
- [[tasks]]
- [[decisions]]
- [[resources]]
```

### `tasks.md`
```md
# Tasks

## Todo
- [ ]

## Doing
- [ ]

## Blocked
- [ ]

## Done
- [x]
```

### `decisions.md`
```md
# Decisions
```

### `resources.md`
```md
# Resources

## Repositories

## Docs

## Tickets

## People / channels

## Local paths
- `~/second_brain/projects/<slug>`

## Commands
```
7. Report the resolved slug, the project path, which files were created, and suggest `/load-project <slug>` next.
8. Keep the response concise and do not use Node scripts or shell substitution.
