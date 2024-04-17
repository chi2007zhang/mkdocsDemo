搭建对外文档中心

# 简介

本教程为希望利用 GitHub 和 Read the Docs 托管 Markdown 文档并搭建在线技术文档中心的读者提供详细的指导与说明。通过本教程，读者将掌握从设置 Git 环境到发布在线文档的完整流程，最终建立在线技术文档中心。

## 目标读者目标读者

本教程面向以下读者：

- 掌握基本计算机操作，但技术基础相对薄弱，对 Git、GitHub 和 Markdown 不够熟悉的读者。
- 希望搭建自己的在线技术文档中心的读者。

## 教程目标

通过本教程，你将能够：

- 安装并配置 Git，用于为构建技术文档版本管理体系。
- 注册并授权 GitHub 账号，从而利用 GitHub 托管文档。
- 安装和配置 VS Code 编辑器，配置一个高效、易用的文档编辑环境。
- 掌握 Markdown 基础语法，编写格式清晰的文档。
- 创建、编辑和推送文档到 GitHub 仓库，实现文档的版本管理与团队协作。
- 通过 Read the Docs 构建在线文档中心。

## 操作环境

本教程使用的软件及其版本如下：

- 操作系统：Windows 11
- Git：2.41.0.windows.3
- GitHub：Free, pro, and team
- Read the Docs：Version 3.1
- VS Code：Version 1.81

## 前提条件

在开始之前，请确保你已经掌握以下知识：

1. 了解MkDocs。更多信息，请参考[MkDocs中文指南](https://markdown-docs-zh.readthedocs.io/zh-cn/latest/)。
2. Git 的分支管理的原理以及常用 Git 指令的含义，如 Clone、Pull、Commit、Stage、Push、Merge 等。更多信息，参考 [Git Reference](https://git-scm.com/docs)。
3. GitHub 的基础操作及其与 Git 的关系。更多信息，参考 [GitHub 入门文档](https://docs.github.com/zh/get-started)。
4. 了解 Read the Docs。更多信息，参考 [Read the Docs: documentation simplified](https://docs.readthedocs.io/en/stable/)。
5. VS Code 界面操作，及其与 Git 指令的关系。更多信息，参考 Introduction to Git in VS Code。
6. Markdown 基础语法。具体语法，参考 [Markdown Guideline](https://www.markdownguide.org/basic-syntax/)。

### MkDocs

MkDocs是一个快速的、简单的、优美的静态网站生成器，专门用于构建项目文档。文档源文件以 Markdown 编写，并通过一个 YAML 配置文件进行配置。[Getting Started](https://www.mkdocs.org/getting-started/) 和 [User Guide](https://www.mkdocs.org/user-guide/)。

- MkDocs可以生成独立站点，或者仅用于生成较大站点的文档部分。
- MkDocs基于Python编写，所有配置都用一个简单的配置文件管理，配置项的内容也仅有一页文档。它见名知意就是为Markdown而生，根据Markdown格式将内容渲染成美观的文档，并通过目录层级关系对应文档的树状结构，使得所有文档组织分明且层次递进。

- MkDocs可以从代码中提取函数文档，模块文档，以及类文档，将它们按照你的要求展示出来。

- MkDocs有很多扩展插件，可以显示 mermaid 流程图，数据公式。

- 更多主题：https://github.com/mkdocs/mkdocs/wiki/MkDocs-Themes

### Git 

Git是一个开源的**分布式版本控制系统**。

- 常用命令：

  -   git clone ：将远程仓库clone到本地计算机。

  -   git status ：展示工作区及暂存区域中不同状态的文件。

  -   git add ：将内容从工作目录添加到暂存区。

  -   git commit ：所有通过 git add 暂存的文件提交到本地仓库。

  -   git push ：将本地仓库的记录提交到远程仓库。

  -   git reset HEAD <file> ：从暂存区移除指定文件。

  -   git push ：拉取远程仓库的数据。

  -   git init

### Github

Github是基于 Git 的**代码托管平台**。

- 因为只支持 Git 作为**唯一的版本库**格式进行托管，故名 GitHub，就是一个平台上面有无数个 Git 仓库——Git 版的百度云，承担存储远程仓库的作用。
- 还可考虑Gitee (国内) 或者Gitlab (私有仓库免费，但社区不如Github)。

### RTD (Read the docs) 

RTD (Read the docs) 是一个**基于 Sphinx** 的免费**文档托管网站**。

- 在与Github连接上配置无误的情况下，当Github上有文件改动时，会自动触发RTD自动更新对应的文档。
- RTD提供了丰富的文档主题，有着灵活的配置，可以满足大部分的需求。

# MkDocs操作简介

## 安装

在开始写文档之前，需要安装 3 个库：

- mkdocs
  - 主要的文档库核心
- mkdocstrings[python]
  - 负责从代码中提取文档
- mkdocs-material
  - 一个好看的代码主题

```c
pip install mkdocs -U
pip install "mkdocstrings[python]" -U
pip install mkdocs-material -U
```

查看是否安装成功

```c
mkdocs --version
```

## 创建新项目

```c
mkdocs new my-project
cd my-project
```

新项目路径下，有一个配置文件 `mkdocs.yml`, 和一个包含文档源码的 `docs` 文件夹. 在 `docs` 文件夹里包含了一个名为 `index.md` 的文档.

```
D:\GitHub>mkdocs new GuideToBldExternalDocCenter
INFO    -  Creating project directory: GuideToBldExternalDocCenter
INFO    -  Writing config file: GuideToBldExternalDocCenter\mkdocs.yml
INFO    -  Writing initial docs: GuideToBldExternalDocCenter\docs\index.md

D:\GitHub>cd GuideToBldExternalDocCenter
```

![image-20240416155344623](Guide%20to%20building%20an%20external%20document%20center.assets/image-20240416155344623.png)

### Commands

- `mkdocs new [dir-name]` - Create a new project.
- `mkdocs serve` - Start the live-reloading docs server.
- `mkdocs build` - Build the documentation site.
- `mkdocs -h` - Print help message and exit.

### Project layout

```bash
mkdocs.yml    # The configuration file.
docs/
    index.md  # The documentation homepage.
    ...       # Other markdown pages, images and other files.
```

## 文档预览

控制台切换当前目录到 `mkdocs.yml` 配置文件相同文件夹, 输入 `mkdocs serve` 命令以启动内建服务器:

```
D:\GitHub\GuideToBldExternalDocCenter>mkdocs serve
INFO    -  Building documentation...
INFO    -  Cleaning site directory
INFO    -  Documentation built in 0.12 seconds
INFO    -  [16:14:49] Watching paths for changes: 'docs', 'mkdocs.yml'
INFO    -  [16:14:49] Serving on http://127.0.0.1:8000/
INFO    -  [16:15:26] Browser connected: http://127.0.0.1:8000/
```

在浏览器中打开 http://127.0.0.1:8000/ , 将看到以下页面:

![image-20240416162450690](Guide%20to%20building%20an%20external%20document%20center.assets/image-20240416162450690.png)

## 添加页面

内建服务器支持在配置文件,文档目录或主题发生改变时自动载入并重新生成文档.



编辑配置文件 `mkdocs.yml` 。 把 `site_name` 改成其他内容并保存文档。

![image-20240416165205583](Guide%20to%20building%20an%20external%20document%20center.assets/image-20240416165205583.png)

刷新浏览器将看到网页标题已发生改变。

![image-20240416165434117](Guide%20to%20building%20an%20external%20document%20center.assets/image-20240416165434117.png)



编辑 `docs/index.md` 文件并保存. 刷新浏览器你将看到文档被同步更新.

## 编辑导航页



## 设置主题





## 更改图标



## 构建网站



## 部署



## 其它

### YAML基础语法
1. 大小写敏感
2. 数据值前边必须有空格，作为分隔符
3. 使用缩进表示层级关系
4. 缩进时不允许使用Tab键，只允许使用空格（各个系统 Tab对应的 空格数目可能不同，导致层次混 乱）。
5. 缩进的空格数目不重要，只要相同层级的元素左侧对齐即可
6. "#"表示注释，从这个字符一直到行尾，都会被解析器忽略。

