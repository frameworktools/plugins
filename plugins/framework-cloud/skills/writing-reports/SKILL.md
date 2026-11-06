---
name: writing-reports
description: Use when the user wants to write, revise, or publish a Framework Cloud report from published results, such as a write-up of an analysis that places published figures, tables, and models between paragraphs.
---

# Writing Framework Cloud reports

A report is one page of Markdown text with published artifacts placed between
the paragraphs. It belongs to a project. Each publish adds a version at the same
stable link.

## Gather the results first

1. Find the project with `projects_list`.
2. List its artifacts with `artifacts_list` and the project slug.
3. Read the ones you will discuss with `artifacts_show`. For text content, such
   as a model's JSON or a CSV table, it returns the content.

Take every estimate, count, and name from `artifacts_show`. Never invent or
round numbers the artifact does not give. If a result you need is not
published, say so and ask the user to publish it.

To use an artifact from another project, call `artifacts_link` first so the
report's project lists it.

## Build the draft

Call `reports_create` with the project `slug`, a `title`, and `blocks`, the
page in order:

- `{"type": "text", "text": "..."}` for Markdown paragraphs and headings.
- `{"type": "artifact", "artifact": "<slug>", "caption": "..."}` for a published
  artifact. Add `version_number` to pin a version; otherwise the latest version
  is pinned when the report is published.

Give blocks an `id` if you will revise them later. For a page with no
artifacts, send `markdown` instead of `blocks`.

Write plainly. Lead each section with the finding, then the evidence. Describe
what a figure or table shows next to it.

## Revise

Read the draft with `reports_show`, then call `reports_update`. Its `blocks`
replaces the whole draft, so send every block you want to keep.

## Visibility and publishing

- Reports start private. Ask before making one `unlisted` or `public`.
- A public report may only show public artifacts.
- Publish with `reports_publish` only when the user asks. Publishing needs a
  paid plan; a 402 error means the account has none, so tell the user.
