# Article and Asset Repository Separation Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Split the existing article repository into a lightweight Markdown repository and a public image asset repository that can scale beyond 100 articles.

**Architecture:** Keep `YiShu5/ai-product-notes` as the article index and Markdown source of truth. Create `YiShu5/ai-product-assets` for images, publish each article's images under a stable category/year/slug path, verify remote image availability, and only then switch article links and remove duplicated images from the notes repository.

**Tech Stack:** Git, GitHub CLI, Markdown, PNG assets, GitHub raw content URLs, shell verification.

## Global Constraints

- Both `YiShu5/ai-product-notes` and `YiShu5/ai-product-assets` must be public.
- Article paths use `articles/<category>/<year>/<article-slug>.md`.
- Image paths use `images/<category>/<year>/<article-slug>/<sequence>-<image-name>.<ext>`.
- Categories use lowercase English kebab-case; the initial set is `ai-product`, `agent`, `rag`, `projects`, and `career`.
- Published article slugs and image paths are stable and must not be renamed casually.
- Images use PNG, JPG, or WebP and should remain below 2 MB each.
- Images must be published and verified before article links switch to the asset repository.
- The article must retain its CSDN source URL and CC BY-SA 4.0 notice.
- Do not use CSDN image hotlinks, force-push, GitHub Pages, or automation scripts.
- Do not delete the original article images until all 11 remote images return HTTP 200.

---

### Task 1: Verify the Migration Baseline

**Files:**
- Verify: `README.md`
- Verify: `articles/coze-agent-deployment-guide.md`
- Verify: `assets/images/coze-agent/*.png`
- Verify: `docs/superpowers/specs/2026-07-14-article-assets-separation-design.md`

**Interfaces:**
- Consumes: Existing `YiShu5/ai-product-notes` `main` branch at commit `acd2cd5` plus the approved local design commit.
- Produces: A clean, synchronized notes workspace and a verified list of 11 source PNG files.

- [ ] **Step 1: Confirm GitHub authentication and repository state**

Run:

```bash
gh auth status
gh repo view YiShu5/ai-product-notes --json nameWithOwner,visibility,defaultBranchRef,url
gh repo view YiShu5/ai-product-assets --json nameWithOwner 2>/dev/null || printf 'asset_repo=available\n'
git status --short --branch
```

Expected: GitHub user is `YiShu5`; notes repository is `PUBLIC` with default branch `main`; asset repository is available; local status is clean and only reports commits ahead of `origin/main`.

- [ ] **Step 2: Verify source image count, type, and size**

Run:

```bash
set -e
count=$(find assets/images/coze-agent -maxdepth 1 -type f -name '*.png' | wc -l | tr -d ' ')
[ "$count" -eq 11 ]
file assets/images/coze-agent/*.png | rg 'PNG image data'
oversized=$(find assets/images/coze-agent -maxdepth 1 -type f -size +2M -print)
[ -z "$oversized" ]
printf 'source_images=%s oversized=0\n' "$count"
```

Expected: `source_images=11 oversized=0`.

---

### Task 2: Create and Publish the Image Repository

**Files:**
- Create in asset repository: `README.md`
- Create in asset repository: `images/agent/2025/coze-agent-deployment-guide/*.png`

**Interfaces:**
- Consumes: The 11 verified files from `ai-product-notes/assets/images/coze-agent/`.
- Produces: Public repository `YiShu5/ai-product-assets` with 11 remotely accessible image URLs.

- [ ] **Step 1: Initialize an isolated asset repository**

Run:

```bash
test ! -e /tmp/ai-product-assets.20260714
mkdir -p /tmp/ai-product-assets.20260714/images/agent/2025/coze-agent-deployment-guide
git -C /tmp/ai-product-assets.20260714 init -b main
git -C /tmp/ai-product-assets.20260714 config user.name "YiShu5"
git -C /tmp/ai-product-assets.20260714 config user.email "163510673+YiShu5@users.noreply.github.com"
```

Expected: A new empty Git repository exists at `/tmp/ai-product-assets.20260714` on `main`.

- [ ] **Step 2: Copy the verified article images**

Run from the notes repository:

```bash
cp assets/images/coze-agent/*.png /tmp/ai-product-assets.20260714/images/agent/2025/coze-agent-deployment-guide/
find /tmp/ai-product-assets.20260714/images/agent/2025/coze-agent-deployment-guide -maxdepth 1 -type f -name '*.png' | sort
```

Expected: The output lists `01-create-entry.png` through `11-publish-channels.png`.

- [ ] **Step 3: Create the asset repository README**

Create `/tmp/ai-product-assets.20260714/README.md` with:

````markdown
# AI Product Assets

意疏的 AI 产品文章图片资源仓库，为 [ai-product-notes](https://github.com/YiShu5/ai-product-notes) 提供稳定的图片地址。

## 目录规范

```text
images/<category>/<year>/<article-slug>/<sequence>-<image-name>.<ext>
```

- 每篇文章使用独立图片目录。
- 已发布的目录和文件名保持稳定。
- 图片不包含账号、联系方式或公司内部数据。
````

- [ ] **Step 4: Validate and commit the asset repository**

Run:

```bash
set -e
test "$(find /tmp/ai-product-assets.20260714/images/agent/2025/coze-agent-deployment-guide -type f -name '*.png' | wc -l | tr -d ' ')" -eq 11
git -C /tmp/ai-product-assets.20260714 add README.md images
git -C /tmp/ai-product-assets.20260714 diff --cached --check
git -C /tmp/ai-product-assets.20260714 commit -m "docs: add Coze article images"
```

Expected: One root commit is created with the README and 11 PNG files.

- [ ] **Step 5: Create the public GitHub repository and push**

Run:

```bash
cd /tmp/ai-product-assets.20260714
gh repo create YiShu5/ai-product-assets --public --description "意疏的 AI 产品文章图片资源仓库" --source . --remote origin --push
```

Expected: `https://github.com/YiShu5/ai-product-assets` is created and `main` tracks `origin/main`.

- [ ] **Step 6: Verify all remote image URLs before changing the article**

Run:

```bash
set -e
remote_count=$(gh api "repos/YiShu5/ai-product-assets/git/trees/main?recursive=1" --jq '.tree[].path' | rg '^images/agent/2025/coze-agent-deployment-guide/[0-9]{2}-.*\.png$' | wc -l | tr -d ' ')
[ "$remote_count" -eq 11 ]
for file in /tmp/ai-product-assets.20260714/images/agent/2025/coze-agent-deployment-guide/*.png
do
  name=$(basename "$file")
  url="https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/agent/2025/coze-agent-deployment-guide/$name"
  status=$(curl -L -s -o /dev/null -w '%{http_code}' "$url")
  printf '%s %s\n' "$status" "$name"
  [ "$status" = "200" ]
done
```

Expected: `remote_count` is 11 and every line begins with `200`.

---

### Task 3: Reorganize the Article Repository

**Files:**
- Create: `articles/agent/2025/coze-agent-deployment-guide.md`
- Modify: `articles/coze-agent-deployment-guide.md`
- Modify: `README.md`
- Delete after verification: `assets/images/coze-agent/*.png`

**Interfaces:**
- Consumes: Verified raw image base URL `https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/agent/2025/coze-agent-deployment-guide/`.
- Produces: Categorized article path, legacy link notice, updated README index, and no duplicated tutorial images in the notes repository.

- [ ] **Step 1: Copy the article to its categorized path**

Run:

```bash
mkdir -p articles/agent/2025
cp articles/coze-agent-deployment-guide.md articles/agent/2025/coze-agent-deployment-guide.md
```

Expected: The new article contains the same title, source URL, license, and 11 image references as the original.

- [ ] **Step 2: Replace image paths in the categorized article**

Apply these exact substitutions in `articles/agent/2025/coze-agent-deployment-guide.md`:

```text
../assets/images/coze-agent/01-create-entry.png
https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/agent/2025/coze-agent-deployment-guide/01-create-entry.png

../assets/images/coze-agent/02-create-agent.png
https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/agent/2025/coze-agent-deployment-guide/02-create-agent.png

../assets/images/coze-agent/03-agent-description.png
https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/agent/2025/coze-agent-deployment-guide/03-agent-description.png

../assets/images/coze-agent/04-agent-editor.png
https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/agent/2025/coze-agent-deployment-guide/04-agent-editor.png

../assets/images/coze-agent/05-agent-preview.png
https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/agent/2025/coze-agent-deployment-guide/05-agent-preview.png

../assets/images/coze-agent/06-add-plugin.png
https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/agent/2025/coze-agent-deployment-guide/06-add-plugin.png

../assets/images/coze-agent/07-bing-web-search.png
https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/agent/2025/coze-agent-deployment-guide/07-bing-web-search.png

../assets/images/coze-agent/08-opening-settings.png
https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/agent/2025/coze-agent-deployment-guide/08-opening-settings.png

../assets/images/coze-agent/09-background-image.png
https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/agent/2025/coze-agent-deployment-guide/09-background-image.png

../assets/images/coze-agent/10-skill-settings.png
https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/agent/2025/coze-agent-deployment-guide/10-skill-settings.png

../assets/images/coze-agent/11-publish-channels.png
https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/agent/2025/coze-agent-deployment-guide/11-publish-channels.png
```

Expected: The article has 11 `raw.githubusercontent.com` references and no `../assets/images/` references.

- [ ] **Step 3: Replace the legacy article with a stable migration notice**

Replace `articles/coze-agent-deployment-guide.md` with:

```markdown
# 文章已迁移

《新手别怕！3 分钟学会扣子（Coze）基础智能体部署》已按分类迁移到：

[阅读完整文章](agent/2025/coze-agent-deployment-guide.md)
```

- [ ] **Step 4: Update the README article index**

Replace the article link in `README.md`:

```markdown
| 2025-03-19 | [新手别怕！3 分钟学会扣子（Coze）基础智能体部署](articles/agent/2025/coze-agent-deployment-guide.md) | Coze、智能体、插件、发布 |
```

- [ ] **Step 5: Validate the reorganized article before deleting images**

Run:

```bash
set -e
article=articles/agent/2025/coze-agent-deployment-guide.md
test "$(rg -o 'https://raw\.githubusercontent\.com/YiShu5/ai-product-assets/main/images/agent/2025/coze-agent-deployment-guide/[^)]+' "$article" | wc -l | tr -d ' ')" -eq 11
! rg -n '\.\./assets/images|i-blog\.csdnimg\.cn' "$article"
rg -n 'blog\.csdn\.net/2302_79751907/article/details/146381305' "$article"
rg -n 'CC BY-SA 4\.0' "$article"
rg -n 'agent/2025/coze-agent-deployment-guide\.md' README.md articles/coze-agent-deployment-guide.md
```

Expected: All checks exit 0.

- [ ] **Step 6: Remove duplicated images and commit the notes repository**

Run:

```bash
git rm -r assets/images/coze-agent
git add README.md articles docs/superpowers
git diff --cached --check
git commit -m "docs: separate article images into asset repository"
```

Expected: The commit includes the categorized article, legacy notice, README update, and deletion of 11 PNG files. The already committed design and plan documents remain in history.

- [ ] **Step 7: Push the notes repository**

Run:

```bash
git push origin main
```

Expected: `main` is pushed without force and tracks `origin/main`.

---

### Task 4: Verify the Two-Repository Delivery

**Files:**
- Verify in notes repository: `README.md`
- Verify in notes repository: `articles/coze-agent-deployment-guide.md`
- Verify in notes repository: `articles/agent/2025/coze-agent-deployment-guide.md`
- Verify in asset repository: `README.md`
- Verify in asset repository: `images/agent/2025/coze-agent-deployment-guide/*.png`

**Interfaces:**
- Consumes: The published `main` branches of both repositories.
- Produces: Evidence that repository visibility, paths, image links, attribution, and local/remote commit synchronization satisfy the approved design.

- [ ] **Step 1: Verify repository visibility and default branches**

Run:

```bash
gh repo view YiShu5/ai-product-notes --json nameWithOwner,visibility,defaultBranchRef,url
gh repo view YiShu5/ai-product-assets --json nameWithOwner,visibility,defaultBranchRef,url
```

Expected: Both report `PUBLIC` and `main`.

- [ ] **Step 2: Verify remote trees**

Run:

```bash
set -e
notes_tree=$(gh api "repos/YiShu5/ai-product-notes/git/trees/main?recursive=1" --jq '.tree[].path')
assets_tree=$(gh api "repos/YiShu5/ai-product-assets/git/trees/main?recursive=1" --jq '.tree[].path')
printf '%s\n' "$notes_tree" | rg '^articles/agent/2025/coze-agent-deployment-guide\.md$'
printf '%s\n' "$notes_tree" | rg '^articles/coze-agent-deployment-guide\.md$'
! printf '%s\n' "$notes_tree" | rg '^assets/images/coze-agent/'
test "$(printf '%s\n' "$assets_tree" | rg '^images/agent/2025/coze-agent-deployment-guide/[0-9]{2}-.*\.png$' | wc -l | tr -d ' ')" -eq 11
```

Expected: Both article paths exist, no old images remain in notes, and the asset repository contains 11 PNG files.

- [ ] **Step 3: Verify the remotely published article**

Run:

```bash
set -e
article=$(gh api -H "Accept: application/vnd.github.raw+json" "repos/YiShu5/ai-product-notes/contents/articles/agent/2025/coze-agent-deployment-guide.md?ref=main")
test "$(printf '%s' "$article" | rg -o 'https://raw\.githubusercontent\.com/YiShu5/ai-product-assets/main/images/agent/2025/coze-agent-deployment-guide/[^)]+' | wc -l | tr -d ' ')" -eq 11
printf '%s' "$article" | rg 'blog\.csdn\.net/2302_79751907/article/details/146381305'
printf '%s' "$article" | rg 'CC BY-SA 4\.0'
! printf '%s' "$article" | rg 'i-blog\.csdnimg\.cn|\.\./assets/images'
```

Expected: The remote article has 11 asset-repository image links, original attribution, and no old hotlinks.

- [ ] **Step 4: Verify every image and local/remote commit identity**

Run:

```bash
set -e
for name in $(gh api "repos/YiShu5/ai-product-assets/git/trees/main?recursive=1" --jq '.tree[].path' | rg '^images/agent/2025/coze-agent-deployment-guide/[0-9]{2}-.*\.png$' | xargs -n1 basename)
do
  url="https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/agent/2025/coze-agent-deployment-guide/$name"
  [ "$(curl -L -s -o /dev/null -w '%{http_code}' "$url")" = "200" ]
done
[ "$(git rev-parse HEAD)" = "$(git ls-remote origin refs/heads/main | awk '{print $1}')" ]
[ "$(git -C /tmp/ai-product-assets.20260714 rev-parse HEAD)" = "$(git -C /tmp/ai-product-assets.20260714 ls-remote origin refs/heads/main | awk '{print $1}')" ]
[ -z "$(git status --porcelain=v1)" ]
[ -z "$(git -C /tmp/ai-product-assets.20260714 status --porcelain=v1)" ]
printf 'verification=passed images=11 repositories=2\n'
```

Expected: `verification=passed images=11 repositories=2`.
