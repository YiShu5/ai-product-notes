# AI Product Notes Repository Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan.

**Goal:** Create and publish the public `YiShu5/ai-product-notes` repository with one cleaned, image-complete Markdown article migrated from CSDN.

**Architecture:** Use a static, GitHub-native repository: a root README acts as the article directory, Markdown lives in `articles/`, and screenshots live in `assets/images/coze-agent/`. No build system or hosting layer is required.

**Tech Stack:** Git, GitHub CLI, Markdown, local PNG assets, shell verification.

## Global Constraints

- [ ] Keep the repository public and use the confirmed name `YiShu5/ai-product-notes`.
- [ ] Use `apply_patch` for authored text files.
- [ ] Preserve original attribution and CC BY-SA 4.0 information.
- [ ] Avoid CSDN hotlinked images in the final article.
- [ ] Do not publish secrets or private company data.

---

## Task 1: Initialize the Local Repository

**Files:**
- Create: `README.md`
- Create: `articles/coze-agent-deployment-guide.md`
- Create: `assets/images/coze-agent/`

- [ ] Run `git init -b main` in the isolated `/tmp/ai-product-notes.*` workspace.
- [ ] Create the repository structure.
- [ ] Add a concise README with repository positioning and an article index.
- [ ] Verify the initial file tree with `rg --files`.

## Task 2: Migrate the CSDN Article

**Files:**
- Modify: `articles/coze-agent-deployment-guide.md`
- Create: `assets/images/coze-agent/*.png`

- [ ] Retrieve the article body and all article screenshots from the canonical CSDN URL.
- [ ] Remove CSDN-specific advertisements, recommendation cards, voting UI, and unrelated modules.
- [ ] Save screenshots with stable ordered filenames under `assets/images/coze-agent/`.
- [ ] Replace remote image links with relative paths from the article.
- [ ] Add original URL, publication/update dates, author-sync note, and CC BY-SA 4.0 notice.

## Task 3: Validate the Local Content

**Files:**
- Verify: `README.md`
- Verify: `articles/coze-agent-deployment-guide.md`
- Verify: `assets/images/coze-agent/*.png`

- [ ] Confirm every Markdown image reference resolves to an existing local file.
- [ ] Confirm no `i-blog.csdnimg.cn` hotlinks remain.
- [ ] Confirm the README links to the article.
- [ ] Confirm the article contains the original source URL and license.
- [ ] Inspect `git diff --check` and repository status.

## Task 4: Commit and Publish

**Files:**
- Commit all repository content.

- [ ] Configure repository-local Git identity only if no usable identity exists.
- [ ] Create a local commit with message `docs: publish initial AI product article`.
- [ ] Run:
  `gh repo create YiShu5/ai-product-notes --public --description "意疏的 AI 产品、Agent、RAG 与实践文章归档" --source . --remote origin --push`
- [ ] Preserve the local repository if remote creation or push fails.

## Task 5: Verify GitHub Delivery

- [ ] Run `gh repo view YiShu5/ai-product-notes --json nameWithOwner,visibility,url,defaultBranchRef`.
- [ ] Verify `README.md` and `articles/coze-agent-deployment-guide.md` through the GitHub API.
- [ ] Verify uploaded image assets are present in the remote tree.
- [ ] Return direct links to the repository, article, and original CSDN source.
