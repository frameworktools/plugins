---
name: designing-blueprints
description: Use when the user wants a reusable Framework project setup, such as "a blueprint for Quarto and R with these settings", or wants to adapt a built-in blueprint, preview the files a project would get, or start a project from a blueprint.
---

# Designing Framework blueprints

A blueprint is a reusable project setup: a folder structure, tools, package
sets, skill sets, skills, and settings. Projects start from a blueprint.

## Propose

1. Read the parts with `blueprints_options`: structures, tools (with the
   languages each fits and what each needs), package sets, skill sets, and
   skills. Use only keys it returns.
2. To start from an existing blueprint, find it with `blueprints_list` and read
   its choices with `blueprints_show`.
3. Propose choices to the user: `language`, `structure`, `tools` (such as
   `{"quarto": true, "renv": true}`), `package_sets`, `skill_sets`, `skills`, and
   `settings` (`sensitive`, `git`, `ai`).

## Preview

Call `blueprints_preview` with the choices and a `workflow` (`quarto`,
`jupyter`, or `scripts`; Stata uses scripts). It returns the files and folders a
project would get, and saves nothing. Show the user the result. If it reports a
problem, such as a tool that needs Quarto, fix the choices and preview again.

## Save

- Call `blueprints_create` only after the user agrees. It needs `name`,
  `language`, and `structure`. New blueprints are private.
- `languages` and `workflows` limit what projects from it may use. Leave them
  out to allow all.
- To change one of the user's own blueprints, call `blueprints_update` with the
  full choices. Read them first with `blueprints_show`. Each save adds a
  version; projects already made keep theirs.
- Built-in blueprints cannot be changed. Save a copy with `blueprints_create`.

## Start a project

When the user asks, call `projects_create` with a `name` and the blueprint's
key in `blueprint`. Its files are made on the user's computer or in GitHub.
