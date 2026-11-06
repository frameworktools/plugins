---
name: publishing-artifacts
description: Use when the user wants to publish a saved file to Framework Cloud as an artifact, such as an HTML notebook, a PNG or SVG figure, a CSV table, a PDF, a model's JSON, or a rendered Quarto site, or wants to add a new version of an artifact or list it in another project.
---

# Publishing artifacts to Framework Cloud

An artifact is a published file with a stable link. Each publish under the same
name adds a version at that link. Artifacts start private.

## Choose how to send the file

- **Small text files** (HTML, Markdown, CSV, JSON, SVG, up to a few hundred KB):
  call `artifacts_publish` with `filename` and the text in `content`.
- **Small binary files** (PNG, PDF): call `artifacts_publish` with `filename` and
  `content_base64`.
- **Anything larger, or any file on disk:** call `artifacts_upload` with
  `filename`. It returns a one-time upload link and a `command`, a curl PUT
  that sends the file. Run the command from the folder with the file. If you
  cannot run commands, give the command to the user. The link expires in 30
  minutes and works once. Files can be up to 50 MB.

Never paste a large file into a call.

If the upload fails because your sandbox blocks the host, tell the user which
host to allow. In Claude, that is Settings, Capabilities, allowed websites; the
change applies in a new chat. Otherwise give the user the command to run.

## Name, kind, and project

- The extension in `filename` sets the kind: `.html` publishes a notebook,
  `.png` or `.svg` a figure, `.csv` a table. Set `kind` only to override it.
- A rendered Quarto site goes as a zip. Set `entrypoint` to the page to open,
  such as `index.html`.
- `artifact` is the name in the link, such as `penguin-body-mass`. It defaults to
  the file name. To add a version, reuse the existing name from `artifacts_list`.
- `project` is optional. Use a project slug from `projects_list`. Without one,
  the artifact has no project.
- Set `title` and `description` so the user can find it later.

## Visibility

New artifacts are private. Use `unlisted` or `public` only when the user asks.
Ask before choosing `public`. A `password` of at least 8 characters protects an
artifact.

## After publishing

- Give the user the link from the response.
- To show an artifact in another project's reports, call `artifacts_link` with
  the project, `artifact`, and `from_project` (leave it out for an artifact with
  no project).
- When you can run commands inside a Framework project, `fw publish` or the R,
  Python, or Stata package is better. They check the project's private folders
  before publishing.
