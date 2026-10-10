---
name: update-github-info
description: Keep Mona's GitHub Info website current with useful updates from GitHub.
on:
  schedule: daily
  workflow_dispatch:

engine: claude

permissions:
  contents: read

tools:
  github:
    toolsets: [repos]
  web-fetch: {}
  edit: true

network:
  allowed:
    - defaults
    - github.blog
    - github.com
    - awesome-copilot.github.com
safe-outputs:
  create-pull-request:
    title-prefix: "[mona] "
    draft: false
---

# Update Mona's GitHub Info

## Sources

1. Read `notes/mona-notes.md` and the current `site/content/github-info.md` using the GitHub repository API tools. Do not use terminal, CLI, or shell commands to read repository files.
2. Fetch all three sources with the `web-fetch` tool:
   - https://github.blog/latest/
   - https://github.blog/changelog/
  - https://awesome-copilot.github.com/workflows/

## Update

Find recent, accurate updates that help developers learn GitHub faster. Prefer useful product changes, features, and practical guidance over general announcements. Compare each candidate with the current page and skip anything already covered or not useful to Mona's audience.

Update only `site/content/github-info.md`, preserving its existing structure and editorial style. Summarize in your own words; do not copy lengthy passages. Attribute every item sourced from the Blog or Changelog with its title, publication date when available, and a direct source link. Do not add unsupported claims. If neither source has a worthwhile new item, leave the page unchanged.

## Review

When there are meaningful changes, use the `create-pull-request` safe output to open a pull request for Mona to review, titled `Update GitHub Info website` (the configured prefix makes it `[mona] Update GitHub Info website`). Describe the updates and link their sources. Never write directly to the default branch, and do not change other files.