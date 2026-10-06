---
name: update-project
description: Update a managed second_brain project from the current Claude session
argument-hint: <existing-project-slug>
allowed-tools: [Bash, Read, Edit, Write, AskUserQuestion]
---

# Update Project

The user invoked this with: $ARGUMENTS

## Goal
Digest the current Claude session into durable project state for `~/second_brain/projects/<slug>/`.

## Expectations
Update the project based on the current session, including:
- decisions made
- tasks finished
- tasks to continue
- new tasks created
- blockers discovered
- durable resources or research references
- refreshed current state
- refreshed implementation plan copy when the session generated or revised a plan
- one new session note under `sessions/`

## Instructions
1. Determine the target project slug before reading or editing files:
   - First inspect `~/second_brain/projects/` and treat existing folder names as the source of truth.
   - If the user provided a project name or slug, match it against existing project folders.
   - If no project was provided, use current session context only to rank or suggest existing project folders.
   - Do not invent, infer, normalize, or create a new slug in this command.
   - If multiple existing projects are plausible, offer a short list and ask the user to choose.
   - If no managed projects exist, say so clearly and suggest `/start-project <project-name>`.
2. Resolve the chosen existing slug directly in the conversation. Use the exact existing folder name as the slug.
3. Read the current project files first:
   - `~/second_brain/projects/<slug>/current.md`
   - `~/second_brain/projects/<slug>/tasks.md`
   - `~/second_brain/projects/<slug>/decisions.md`
   - `~/second_brain/projects/<slug>/resources.md`
   - `~/second_brain/projects/<slug>/plans/implementation-plan.md` if it exists
4. If the project does not exist, say so clearly and suggest `/start-project <project-name>`.
5. From the current Claude session, derive durable updates in these buckets:
   - decisions made
   - tasks completed
   - tasks to continue
   - new tasks created
   - durable resources or research worth preserving
   - whether an implementation plan was generated or revised
6. Auto-apply obvious changes. Ask only targeted questions when an item is ambiguous, for example whether something should be treated as a final decision, a done task, or a durable resource.
7. Update markdown conservatively:
   - keep `current.md` short and operational
   - update `tasks.md` using the stable headings `## Todo`, `## Doing`, `## Blocked`, `## Done`
   - represent every task in `tasks.md` as a markdown checkbox item
   - use `- [ ]` in `Todo`, `Doing`, and `Blocked`
   - use `- [x]` in `Done`
   - when moving a task into `Done`, convert it to `- [x]`; when moving it back into an active section, convert it to `- [ ]`
   - normalize touched plain-bullet task items into checkbox format when editing `tasks.md`
   - append dated decisions to `decisions.md`
   - append durable references to `resources.md`
   - if the session generated or revised an implementation plan, write or refresh `~/second_brain/projects/<slug>/plans/implementation-plan.md` with the latest plan content from the session
   - create one dated note in `sessions/` summarizing the session; if the plan was updated, mention `plans/implementation-plan.md` in the note
8. Prefer section-targeted edits over rewriting whole files unless a file is missing or malformed.
9. Report what changed:
   - tasks moved or added
   - decisions captured
   - resources captured
   - implementation plan path when updated
   - session note path
10. Use Bash only for a simple read-only directory listing of `~/second_brain/projects/`. Do not use temporary JSON files or helper scripts.

Keep the final response concise and changelog-oriented.
