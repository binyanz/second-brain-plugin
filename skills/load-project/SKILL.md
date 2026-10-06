---
name: load-project
description: Load a compact working brief for a managed second_brain project
argument-hint: <existing-project-slug>
allowed-tools: [Bash, Read]
---

# Load Project

The user invoked this with: $ARGUMENTS

## Goal
Load project context from `~/second_brain/projects/<slug>/` and produce a compact working brief.

## Instructions
1. Determine the target project slug before reading project files:
   - First inspect `~/second_brain/projects/` and treat existing folder names as the source of truth.
   - If the user provided a project name or slug, match it against existing project folders.
   - If no project was provided, use current session context only to rank or suggest existing project folders.
   - Do not invent, infer, or normalize a new slug.
   - If multiple existing projects are plausible, offer a short list and ask the user to choose.
   - If no managed projects exist, say so clearly and suggest `/start-project <project-name>`.
2. Resolve the chosen existing slug directly in the conversation. Use the exact existing folder name as the slug.
3. Read these files if they exist:
   - `~/second_brain/projects/<slug>/overview.md`
   - `~/second_brain/projects/<slug>/current.md`
   - `~/second_brain/projects/<slug>/tasks.md`
   - `~/second_brain/projects/<slug>/decisions.md`
   - `~/second_brain/projects/<slug>/plans/implementation-plan.md` when present and relevant
4. If the project folder or core files do not exist, say so clearly and suggest `/start-project <project-name>`.
5. Produce a compact working brief that covers:
   - project purpose
   - current focus
   - blockers
   - open work
   - recent decisions
   - current plan direction when available
   - recommended next steps
6. Do not dump raw file contents unless the user asks.
7. This command is read-only. You may use Bash only for a simple read-only directory listing of `~/second_brain/projects/`.

Keep the response operational and concise.
