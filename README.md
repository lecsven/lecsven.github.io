# 个人博客（Hexo + GitHub Pages）

基于 [Hexo](https://hexo.io/) 的静态博客，使用 NexT 主题，通过 GitHub Pages 对外发布。

- 源码：`hexo` 分支（仓库默认分支）
- 产物：`master` 分支（由部署命令自动生成，请看下方说明）

## 分支说明

| 分支 | 作用 | 是否手动修改 |
| --- | --- | --- |
| `hexo` | 站点源码：文章、配置、主题、图片 | 是 |
| `master` | 构建产物，GitHub Pages 实际服务的分支 | **否**，由 `hexo deploy` 覆盖 |

> `master` 每次部署都会被 `public/` 的内容整体覆盖（force-push）。不要在该分支上手动提交或保存任何文件。

## 本地开发

```bash
# 安装依赖
npm install

# 本地预览（默认 http://localhost:4000）
hexo server
```

## 发布

```bash
# 清理缓存并重新生成，然后部署到 master 分支
hexo clean && hexo generate && hexo deploy
```

部署完成后，GitHub Pages 通常需要几十秒刷新，稍等片刻再访问线上地址。

## 写作约定

- 文章放在 `source/_posts/`，文件名会成为 URL 的一部分。
- Front matter 至少包含 `title` 与 `date`：

  ```yaml
  ---
  title: 文章标题
  date: 2026-01-01
  tags:
    - 标签
  ---
  ```

## 图片约定

出于稳定性考虑，**图片一律自托管在本仓库**，不使用会限流或防盗链的第三方图床。

- 存放位置：一篇一个目录，按文章 slug 命名

  ```text
  source/images/
  ├─ <post-slug-a>/01.jpg
  ├─ <post-slug-a>/02.jpg
  └─ <post-slug-b>/01.png
  ```

- 引用方式：使用**根相对路径**，不受文章层级影响

  ```markdown
  ![说明](/images/<post-slug>/01.jpg)
  ```

## 目录结构

```text
.
├─ _config.yml            # Hexo 站点配置
├─ source/
│  ├─ _posts/             # 文章（Markdown）
│  ├─ _data/              # 主题备用配置与自定义样式
│  └─ images/             # 自托管图片
├─ themes/
│  └─ next-reloaded/      # NexT 主题（已直接内置在仓库中）
└─ package.json
```

## 注意事项

- **主题已内置**：`themes/next-reloaded/` 是直接纳入版本控制的普通目录，`git clone` 后即可构建，无需初始化任何子模块。
- **`url` 配置**：`_config.yml` 中的 `url` 必须是站点的正式地址，否则 `canonical`、`og:url`、`og:image` 等元信息会出错（影响搜索引擎与社交分享）。
- **图片不要外链第三方图床**：第三方一旦限流、启用防盗链或关停，站点会大面积裂图。
