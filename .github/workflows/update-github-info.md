---
name: update-github-info
description: Keep the GitHub Info page current with recent GitHub Blog and Changelog updates.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
engine:
  id: copilot
  model: gpt-4o
tools:
  edit:
  web-fetch:
  web-search:
  github:
    toolsets: [repos]
network:
  allowed:
    - github.blog
    - github.com
    - awesome-copilot.github.com
safe-outputs:
  create-pull-request:
    reviewers: [monalisa]
    draft: true
---

# Update GitHub Info

Keep `site/content/github-info.md` current for Mona's review.

1. Read `notes/mona-notes.md`.
2. Use the web-fetch tool to use the GitHub Blog and read the latest public updates from. If web-fetch is unavailable, use the native web-search tool with the exact URL:
   - https://github.blog/latest/
3. Use the web-fetch tool to use the GitHub Changelog and read the latest release and product updates from. If web-fetch is unavailable, use the native web-search tool with the exact URL:
  - https://github.blog/changelog/
4. Use the web-fetch tool to read Awesome Copilot workflows from. If web-fetch is unavailable, use the native web-search tool with the exact URL:
   - https://awesome-copilot.github.com/workflows/
5. Use the GitHub repository API tools to read repository guidance or reference files that are relevant to this update. Do not use terminal, CLI, or sandboxed shell commands for those reads.
6. Update `site/content/github-info.md` with short, practical information that helps developers learn GitHub faster. Mention the source whenever an update comes from the GitHub Blog, GitHub Changelog, or Awesome Copilot workflows.
7. Make only focused, useful edits. Preserve the existing structure and style, and do not invent facts or sources.
8. Use the `create-pull-request` safe output to create a draft pull request containing the changes for Mona to review. Summarize the updates and cite the source URLs in the pull request body.

If there is nothing useful to update, do not modify files or open a pull request.
