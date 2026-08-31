# Nextpilot Document Website

> ⚠️ **重要通知** - 本仓库已归档
>
> 该仓库已停止维护，请访问新的仓库：[nextpilot-official-website](https://github.com/nextpilot/nextpilot-official-website)
>
> 官方网站已迁移至：<https://nextpilot.org>，原域名 <https://docs.nextpilot.org> 自动跳转到新的网站。

## 如何使用

本仓库托管了 NextPilot Document Website 网站，包含产品介绍、精彩案例、用户手册、开发指南等内容。

- 官方网站：<https://docs.nextpilot.org>

- 用户手册：<https://docs.nexpilot.org/manual>

- 开发指南：<https://docs.nexpilot.org/develop>

> 当仓库更新时，Github 基于 [.github/workflows/mkdocs-gh-deploy.yml](.github/workflows/mkdocs-gh-deploy.yml) 自动触发编译，并将生成结果推送到 [gh-pages分支](https://github.com/nextpilot/nextpilotgithub.io/tree/gh-pages)。

## 如何编译

NextPilot Document Website 基于 [mkdocs](https://www.mkdocs.org/) 和 [mkdocs-material](https://squidfunk.github.io/mkdocs-material/) 进行发布的，需要 **python3.8** 以上版本。

安装mkdocs依赖项

```shell
# 升级pip工具
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple --upgrade pip

# 设置PyPi国内镜像源
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple

# 安装mkdocs等依赖项
pip install -r docs/requirements.txt
```

编译帮助文档

```shell
# 下载代码到本地
git clone https://github.com/nextpilot/nextpilot.github.io.git
# 切换到docs目录
cd nextpilot.github.io
# 编译文档
mkdocs build
# 或者使用，在浏览器http://127.0.0.1:8063/可以预览效果
mkdocs serve
```

## 参考资料

- [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/getting-started/)
- [MkDocs static i18n plugin documentation，多国语言支持](https://ultrabug.github.io/mkdocs-static-i18n)
- [mkdocs-literate-nav，使用 SUMMARY.md 创建导航栏](https://oprypin.github.io/mkdocs-literate-nav/index.html)
- [mkdocs-awesome-nav，使用.nav.yml 自定义导航栏](https://lukasgeiter.github.io/mkdocs-awesome-nav/)
