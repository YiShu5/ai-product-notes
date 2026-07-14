# 文章与图片仓库拆分设计

## 状态

用户已于 2026-07-14 确认采用“双仓库”方案，目标规模为 100 篇以上。

## 目标

将文章正文和图片资源分开管理，使文章仓库保持轻量，同时为每篇文章提供稳定、清晰、可长期扩展的图片目录。

## 仓库职责

### `YiShu5/ai-product-notes`

公开仓库，只保存 Markdown 文章、文章索引和仓库说明。

```text
ai-product-notes/
├── README.md
└── articles/
    ├── ai-product/
    │   └── 2025/
    ├── agent/
    │   └── 2025/
    ├── rag/
    ├── projects/
    └── career/
```

文章路径统一使用：

```text
articles/<category>/<year>/<article-slug>.md
```

### `YiShu5/ai-product-assets`

新建公开仓库，只保存文章图片和资源说明。

```text
ai-product-assets/
├── README.md
└── images/
    ├── ai-product/
    ├── agent/
    │   └── 2025/
    │       └── coze-agent-deployment-guide/
    ├── rag/
    ├── projects/
    └── career/
```

图片路径统一使用：

```text
images/<category>/<year>/<article-slug>/<sequence>-<image-name>.<ext>
```

## 命名规范

- 分类名、文章名和图片名使用小写英文及连字符。
- 文章目录采用稳定的 `article-slug`，发布后不随意改名。
- 图片以两位序号开头，例如 `01-create-entry.png`。
- 初始分类为 `ai-product`、`agent`、`rag`、`projects` 和 `career`；只有出现明确的新主题时才增加分类。

## 图片引用

文章使用图片仓库的绝对地址，避免依赖文章仓库中的相对路径：

```markdown
![创建智能体](https://raw.githubusercontent.com/YiShu5/ai-product-assets/main/images/agent/2025/coze-agent-deployment-guide/01-create-entry.png)
```

图片仓库必须保持公开。已发布的图片路径视为稳定接口，不随意移动或删除。

## 新文章发布流程

1. 确定文章分类、年份和稳定的 `article-slug`。
2. 在图片仓库中建立该文章的独立图片目录。
3. 上传、按顺序命名并验证全部图片。
4. 在文章仓库中新增 Markdown，使用已经验证的远程图片地址。
5. 更新文章仓库的 README 分类索引。
6. 检查文章图片数量、失效链接、来源和许可信息后发布。

图片必须先于文章发布，避免文章上线时出现破图。

## 当前文章迁移

- 创建公开仓库 `YiShu5/ai-product-assets`。
- 将现有 11 张扣子教程图片复制到：
  `images/agent/2025/coze-agent-deployment-guide/`。
- 将正文移动到：
  `articles/agent/2025/coze-agent-deployment-guide.md`。
- 在旧路径 `articles/coze-agent-deployment-guide.md` 保留迁移说明和新文章链接，避免旧链接直接失效。
- 将正文中的 11 个相对图片地址替换为图片仓库的绝对地址。
- 更新 README 的文章索引。
- 远端图片全部验证成功后，再从文章仓库删除原图片文件。

## 资源约束

- 优先使用 PNG、JPG 或 WebP。
- 单张图片尽量控制在 2 MB 以内；超过时先压缩再提交。
- 不上传包含账号、手机号、公司内部数据或其他敏感信息的截图。
- 不使用 CSDN 等第三方图片热链作为最终地址。

## 故障处理

- 图片仓库创建失败时，不修改现有文章仓库。
- 图片上传或远端访问验证失败时，保留文章仓库中的原图片，不切换正文链接。
- 文章仓库更新失败时，图片仓库中的文件可以保留，待修复后继续。
- 不使用强制推送；两个仓库均通过普通提交保留迁移历史。

## 验收标准

- 两个仓库均为公开仓库，职责清晰。
- 文章仓库中的正文不再保存教程图片。
- 当前文章的 11 个图片地址均能从图片仓库读取。
- README 可以进入新的文章路径，旧文章路径可以跳转到迁移说明。
- 文章保留原始 CSDN 来源和 CC BY-SA 4.0 许可。
- 两个仓库本地提交与远端 `main` 分支一致。

## 非目标

- 不创建 100 个文章仓库或 100 个图片仓库。
- 不启用 GitHub Pages。
- 不在本次迁移中增加自动发布脚本。
