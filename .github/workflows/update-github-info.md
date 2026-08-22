---
name: update-github-info
description: Refresh the GitHub Info content from the latest official GitHub Blog and Changelog updates.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  actions: read
tools:
  edit:
  web-fetch:
  github:
    toolsets: [repos]
network:
  allowed:
    - github.blog
    - github.com
safe-outputs:
  create-pull-request:
    base-branch: main
    title-prefix: "[mona] "
    draft: true
    labels: [content-update]
    max: 1
---

# Update GitHub Info

Refresh the website's GitHub update feed and propose the result for Mona's review.

## Required reading

1. Use the GitHub repository API tools to read `notes/mona-notes.md`.
2. Use the GitHub repository API tools to read the current `site/content/github-info.md`.
3. Use `web-fetch` to fetch and read `https://github.blog/latest/`.
4. Use `web-fetch` to fetch and read `https://github.blog/changelog/`.

## Update rules

- Keep summaries short, practical, and useful for developers learning GitHub faster.
- Prefer recent items from the GitHub Blog and GitHub Changelog.
- Attribute every selected item to its source with a source URL.
- Preserve the existing Markdown structure and editorial angle where practical.
- Update only `site/content/github-info.md`.
- Do not modify workflow files, generated files, site code, or unrelated content.
- Do not write directly to `main`.

After editing `site/content/github-info.md`, use the `create_pull_request` safe output to propose the change as a draft pull request targeting `main`. Give the pull request a concise title and explain which official sources were reviewed. The pull request is for Mona to review before publication.
