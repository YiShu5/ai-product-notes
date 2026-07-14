# AI Product Notes Repository Design

## Status

Approved by the user on 2026-07-14.

## Goal

Create a public GitHub repository at `YiShu5/ai-product-notes` for publishing the user's AI product, Agent, RAG, and hands-on technical articles.

## Initial Scope

- Create a lightweight article repository rather than a GitHub Pages site.
- Add a repository-level `README.md` as the article index.
- Store Markdown articles under `articles/`.
- Store article images locally under `assets/images/<article-slug>/`.
- Migrate the first article from CSDN:
  - Title: 新手别怕！3 分钟学会扣子（Coze）基础智能体部署
  - Original: https://blog.csdn.net/2302_79751907/article/details/146381305

## Repository Structure

```text
ai-product-notes/
├── README.md
├── articles/
│   └── coze-agent-deployment-guide.md
├── assets/
│   └── images/
│       └── coze-agent/
└── docs/
    └── superpowers/
        ├── plans/
        └── specs/
```

## Content Rules

- Preserve the author's original meaning while removing CSDN advertisements, recommendation modules, voting blocks, and platform-only UI text.
- Keep screenshots in the repository so the article does not depend on CSDN image hotlinks.
- Add the original CSDN URL, original publication date, update date, and CC BY-SA 4.0 attribution near the beginning of the article.
- Use repository-relative image paths so images render on GitHub.
- Do not include credentials, private business data, or unpublished company information.

## Failure Handling

- If an image cannot be retrieved, keep the article publishable, record the missing image in verification output, and do not silently substitute an unrelated image.
- If repository creation or push fails, preserve the complete local repository and report the exact failing operation.

## Out of Scope

- GitHub Pages deployment.
- Automated CSDN synchronization.
- Rewriting or expanding the article beyond light cleanup for GitHub readability.
