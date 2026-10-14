# my-docs

使用 **MkDocs + Material 主题** 构建的技术文档站，通过 GitHub Actions 自动部署到 GitHub Pages。

🌐 在线访问：**https://dusk5-Surtr.github.io/my-docs/**

## 目录结构

```
my-docs/
├── docs/                       # 存放 Markdown 文档
│   ├── index.md                # 主页
│   ├── about.md                # 关于页面
│   ├── guide.md                # 使用指南
│   └── api.md                  # API 参考
├── .github/
│   └── workflows/
│       └── deploy.yml          # 自动化部署工作流配置
├── mkdocs.yml                  # MkDocs 配置文件
└── README.md                   # 项目说明
```

## 本地预览

```bash
# 1. 安装 MkDocs 及 Material 主题
pip install mkdocs-material

# 2. 启动本地服务器（默认 http://127.0.0.1:8000）
mkdocs serve

# 或者只构建静态文件到 site/ 目录
mkdocs build
```

## 自动部署流程

`.github/workflows/deploy.yml` 在 `main` 分支发生推送、且改动涉及 `docs/**` 或 `mkdocs.yml` 时触发：

| 步骤 | 作用 |
|---|---|
| **检出代码** | `actions/checkout@v4` 取到仓库代码 |
| **设置Python环境** | `actions/setup-python@v4` 配置 Python 3.9 |
| **安装MkDocs及主题** | `pip install mkdocs-material` |
| **构建静态文档** | `mkdocs build`，产物在 `site/` 目录 |
| **部署到GitHub Pages** | `JamesIves/github-pages-deploy-action@v4` 把 `site/` 推送到 `gh-pages` 分支 |

推送后到仓库 **Actions** 标签页可查看运行状态；成功后 GitHub Pages 从 `gh-pages` 分支发布站点。
首次部署后需要 1–2 分钟网站才会更新。
