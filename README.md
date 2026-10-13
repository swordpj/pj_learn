---
type: guide
tags:
  - 使用指南
---

# pj_learn · 学习笔记库

日常入口是 [[学习首页]]。这是一个使用 Obsidian 内置模板、每日笔记和 Bases 的本地笔记库。

## 目录

| 目录 | 存放内容 |
| --- | --- |
| `00-收件箱` | 临时想法、问题与尚未整理的笔记；新笔记默认位置 |
| `10-主题` | 主题索引、学习路线、学习总览 |
| `20-概念` | 一个问题或概念一篇，用自己的话解释 |
| `30-资料` | 书籍、课程、论文、网页等来源笔记 |
| `40-实践` | 练习、实验、项目与排错记录 |
| `50-复盘` | 阶段回顾、每周复盘 |
| `60-日记` | 每日笔记，文件名为 `YYYY-MM-DD` |
| `90-模板` | 五种内置模板 |
| `99-附件` | 粘贴或拖入笔记的图片和其他附件 |

## 第一次使用

1. 打开 [[学习首页]]，点击左侧“打开今天的日记”。
2. 新建一篇笔记，先起名字，再从命令面板选择“插入模板”。
3. 将笔记移到概念、资料或实践目录，并关联到 [[10-主题/主题索引|主题索引]]。
4. 在 `next_review` 属性填写希望复习的日期，例如 `2026-10-20`。

普通新建笔记不会自动套用模板；每日笔记会自动使用“每日笔记”模板。插入模板前起好名字，可以让模板中的标题正确展开。

## 属性与复习

- `type`：`concept`（概念）、`source`（资料）、`practice`（实践）；其余模板使用 `daily` 和 `review`。
- `status`：`待整理`、`学习中`、`待复习`、`已掌握`。
- `created`：创建日期，由模板填写。
- `next_review`：下次复习日期；留空表示尚未安排。
- `topics`：主题笔记链接列表。在属性编辑器里添加已有主题的双向链接。
- `tags`：少量稳定的标签；不要用标签重复所有文件夹分类。

[[10-主题/学习总览.base|学习总览]] 自动收集概念、资料、实践目录中的笔记。“到期复习”显示复习日期不晚于今天、且尚未标记为已掌握的笔记。复习完成后手动更新状态和日期；它不发送通知，也不自动计算间隔。

## 命令行

已启用官方 Obsidian CLI，命令为 `obsidian`。可执行文件来自本机 Obsidian 应用，并通过 `~/.local/bin/obsidian` 链接注册。`obsidian-cli` 同时是已安装的代理技能名称，不需要再安装同名的第三方命令行包。

CLI 与桌面应用配合工作；若连接失败，先打开 Obsidian 和本库。显式指定 `vault=pj_learn`，可避免写入其他库。

```bash
# 查看当前版本支持的命令
obsidian help

# 查看本库
obsidian vault=pj_learn vault

# 打开今天的日记
obsidian vault=pj_learn daily

# 搜索笔记
obsidian vault=pj_learn search query="关键词"

# 从模板创建概念笔记；替换示例名称后执行
obsidian vault=pj_learn create path="20-概念/你的概念.md" template="学习笔记" open

# 在日记中追加一个任务
obsidian vault=pj_learn daily:append content="- [ ] 复习今天的核心概念"

# 查询到期复习列表
obsidian vault=pj_learn base:query path="10-主题/学习总览.base" view="到期复习" format=md
```

## 网页提取

已安装 `defuddle`，可把公开网页的正文提取成 Markdown。下面命令输出到终端，确认内容后再保存进 `30-资料`，并补上原始链接和自己的理解：

```bash
defuddle parse https://help.obsidian.md/cli --md
```

Defuddle 通过当前 Node.js 环境全局安装；切换 Node 版本后，如命令不可用，可在新环境重新安装 `defuddle`。

## Codex 技能

安装位置为 `~/.codex/skills/`，来源为 [kepano/obsidian-skills](https://github.com/kepano/obsidian-skills)，固定版本 `3ccff5338ea700537839b21900aa5358a0402c98`。

| 技能 | 能力 |
| --- | --- |
| `obsidian-cli` | 查询、创建、搜索和管理笔记 |
| `obsidian-markdown` | 双向链接、属性、引用块和嵌入 |
| `obsidian-bases` | 笔记表格、筛选、公式与视图 |
| `json-canvas` | 概念图、学习路线与 Canvas 画布 |
| `defuddle` | 提取网页正文为 Markdown |

技能已安装，下一个对话回合可用。可以直接说“把这篇资料整理进笔记库”“为这个主题建立学习路线”或“帮我整理收件箱”。本库的协作约定见 `AGENTS.md`。

## 本地版本记录

本目录使用本地 Git 记录文件版本，不连接远程仓库。工作区布局、回收站和系统临时文件不纳入版本记录。学习一段时间后，可以手动保存一个版本：

```bash
git add .
git commit -m "更新学习笔记"
```

Git 位于同一块磁盘上，不能代替异地备份。初始化前的配置和原始 Welcome 笔记保存在 `~/.local/share/obsidian-setup/backups/pj_learn-20261013-200801/`；原始 `Welcome.md` 也保留在库内。

参考：[官方 CLI 文档](https://help.obsidian.md/cli)、[Defuddle 项目](https://github.com/kepano/defuddle)。
