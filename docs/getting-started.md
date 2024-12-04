# 准备开始

Material for MkDocs 是一个基于 [MkDocs] 的强大文档框架，MkDocs 是一个用于项目文档的静态网站生成器。[^1]如果你熟悉 Python，可以使用 Python 包管理器`pip`安装 Material for MkDocs。如果不熟悉，我们建议使用`docker`。

[^1]:2016 年，Material for MkDocs 最初只是 MkDocs 的一个简单主题，但在几年的时间里，它现在远不止于此 —— 凭借众多内置插件、设置和无数的自定义功能，Material for MkDocs 现在是为你的项目创建文档的最简单和最强大的框架之一。

[MkDocs]: https://www.mkdocs.org
[pip]: #with-pip
[docker]: #with-docker

## 安装

### 使用 pip <small>推荐</small> {#with-pip data-toc-label="使用 pip"}

Material for MkDocs 作为一个 [Python包] 发布，可以使用`pip`安装，理想情况下是在一个 [虚拟环境] 中安装。打开终端，使用以下命令安装 Material for MkDocs：

=== "最新版"

    ``` sh
    pip install mkdocs-material
    ```

=== "9.x 版本"

    ``` sh
    pip install mkdocs-material=="9.*" # (1)!
    ```
    
    1. 	Material for MkDocs 使用 [语义化版本控制] [^2]，这就是为什么将升级限制在当前主版本是个好主意。
        这将确保你不会意外地 [升级到下一个主版本]，因为下一个主版本可能包含会悄悄破坏你网站的破坏性更改。此外，你可以使用`pip freeze`创建一个锁定文件，以便构建始终可重现：
    
        ```
        pip freeze > requirements.txt
        ```
    
        Now, the lockfile can be used for installation:
    
        ```
        pip install -r requirements.txt
        ```

[^2]:
    请注意，现有功能的改进有时会发布为补丁发布，例如改进的内容选项卡渲染，它们不被认为是新功能。

这将自动安装所有依赖项的兼容版本：[MkDocs]、[Markdown]、[Pygments] 和 [Python Markdown 扩展]。Material for MkDocs 始终努力支持最新版本，因此无需单独安装这些包。

---

:fontawesome-brands-youtube:{ style="color: #EE0F0F" }
__[How to set up Material for MkDocs]__ by @james-willett – :octicons-clock-24:
27m – 学习如何在 GitHub Pages 上使用 Material for MkDocs 逐步创建和托管文档网站。

[How to set up Material for MkDocs]: https://www.youtube.com/watch?v=xlABhbnNrfI

---

!!! tip

    如果你之前没有使用 Python 的经验，我们建议阅读 [使用 Python 的 pip 管理项目依赖项]，这是一篇关于 Python 包管理机制的非常好的入门文章，并且在你遇到错误时可以帮助你进行故障排除。

[Python包]: https://pypi.org/project/mkdocs-material/
[虚拟环境]: https://realpython.com/what-is-pip/#using-pip-in-a-python-virtual-environment
[语义化版本控制]: https://semver.org/
[升级到下一个主版本]: upgrade.md
[Markdown]: https://python-markdown.github.io/
[Pygments]: https://pygments.org/
[Python Markdown 扩展]: https://facelessuser.github.io/pymdown-extensions/
[使用 Python 的 pip 管理项目依赖项]: https://realpython.com/what-is-pip/

### 使用 docker

官方 [Docker 镜像] 是一种在几分钟内快速启动并运行的好方法，因为它预安装了所有依赖项。打开终端并使用以下命令拉取镜像：

=== "Latest"

    ```
    docker pull squidfunk/mkdocs-material
    ```

=== "9.x"

    ```
    docker pull squidfunk/mkdocs-material:9
    ```

`mkdocs`可执行文件作为入口点提供，`serve`是默认命令。如果你不熟悉 Docker，不用担心，我们将在以下部分为你介绍。

以下插件与 Docker 镜像捆绑在一起：

- [mkdocs-minify-plugin]
- [mkdocs-redirects]

  [Docker 镜像]: https://hub.docker.com/r/squidfunk/mkdocs-material/
  [mkdocs-minify-plugin]: https://github.com/byrnereese/mkdocs-minify-plugin
  [mkdocs-redirects]: https://github.com/datarobot/mkdocs-redirects

???  问题 :"如何向 Docker 镜像添加插件？"

    Material for MkDocs 仅捆绑了选定的插件，以保持官方镜像的大小较小。如果你想使用的插件未包含在内，可以轻松添加它们：
    
    === "Material for MkDocs"
    
        创建一个Dockerfile并扩展官方镜像：
    
        ``` Dockerfile title="Dockerfile"
        FROM squidfunk/mkdocs-material
        RUN pip install mkdocs-macros-plugin
        RUN pip install mkdocs-glightbox
        ```
    
    === "Insiders"
    
        克隆或派生 Insiders 存储库，并在存储库的根目录中创建一个名为user-requirements.txt的文件。然后，将要安装的插件添加到文件中，例如：
    
        ``` txt title="user-requirements.txt"
        mkdocs-macros-plugin
        mkdocs-glightbox
        ```
    
    接下来，使用以下命令构建镜像：
    
    ```
    docker build -t squidfunk/mkdocs-material .
    ```
    
    新镜像将安装其他包，并且可以与官方镜像完全一样使用。

### 使用 git

Material for MkDocs 可以通过从[GitHub](https://github.com/squidfunk/mkdocs-material)克隆存储库到项目根目录的子文件夹中直接使用，如果你想使用最新版本，这可能会很有用：

```
git clone https://github.com/squidfunk/mkdocs-material.git
```

接下来，使用以下命令安装主题及其依赖项：

```
pip install -e mkdocs-material
```

[GitHub]: https://github.com/squidfunk/mkdocs-material
