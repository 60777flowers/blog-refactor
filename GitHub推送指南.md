# GitHub 仓库创建和推送指南

## 步骤一:在 GitHub 上创建新仓库

1. 访问 https://github.com/new
2. 填写仓库信息:
   - **Repository name**: `blog-refactor` (或你喜欢的名字)
   - **Description**: 博客重整项目 - Hexo 7.x + Butterfly 主题
   - **Public/Private**: 选择 Private (私密) 或 Public (公开)
   - **不要勾选** "Add a README file"
   - **不要勾选** "Add .gitignore"
   - **不要勾选** "Choose a license"
3. 点击 "Create repository"

## 步骤二:推送代码到 GitHub

### 方式 A: 使用 HTTPS (推荐)

```bash
# 进入博客目录
cd d:\大四下\博客修复与重整

# 初始化 Git 仓库
git init

# 添加所有文件
git add .

# 提交更改
git commit -m "feat: 博客重整完成 - 升级到 Hexo 7.x + Butterfly 主题

- Hexo 从 5.4.0 升级到 7.3.0
- 主题从 yilia 升级到 Butterfly 5.5.4
- 添加字数统计和阅读时间功能
- 配置本地搜索
- 优化侧边栏显示
- 添加完整的修改手册"

# 连接到你的 GitHub 仓库 (替换 YOUR_USERNAME 为你的 GitHub 用户名)
git remote add origin https://github.com/YOUR_USERNAME/blog-refactor.git

# 推送到 GitHub
git branch -M main
git push -u origin main
```

### 方式 B: 使用 SSH (如果你已配置 SSH 密钥)

```bash
# 进入博客目录
cd d:\大四下\博客修复与重整

# 初始化 Git 仓库
git init

# 添加所有文件
git add .

# 提交更改
git commit -m "feat: 博客重整完成 - 升级到 Hexo 7.x + Butterfly 主题"

# 连接到你的 GitHub 仓库 (替换 YOUR_USERNAME 为你的 GitHub 用户名)
git remote add origin git@github.com:YOUR_USERNAME/blog-refactor.git

# 推送到 GitHub
git branch -M main
git push -u origin main
```

## 步骤三:后续部署博客

### 部署到 GitHub Pages

有两种方式:

#### 方式 1: 创建单独的仓库部署博客

为博客的静态文件创建一个单独的仓库(例如 `username.github.io`):

```bash
# 在 blog 目录下
cd d:\大四下\博客修复与重整\blog

# 生成静态文件
npx hexo clean
npx hexo generate

# 部署到 GitHub Pages
npx hexo deploy
```

#### 方式 2: 使用 GitHub Actions 自动部署(推荐)

在同一个仓库中配置 GitHub Actions,自动构建和部署:

1. 在 GitHub 仓库中创建 `.github/workflows/deploy.yml`
2. 添加以下内容(见下文)
3. 在 GitHub 仓库设置中添加 Secrets:
   - `GITHUB_TOKEN`: 自动提供
   - `DEPLOY_REPO`: 你的用户名/仓库名 (例如 `60777flowers/60777flowers.github.io`)

## 步骤四:GitHub Actions 配置文件 (可选)

在项目根目录创建 `.github/workflows/deploy.yml`:

```yaml
name: Hexo Deploy

on:
  push:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout source
      uses: actions/checkout@v3
      with:
        submodules: false

    - name: Use Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '18'

    - name: Install dependencies
      run: |
        cd blog
        npm install

    - name: Generate
      run: |
        cd blog
        npx hexo clean
        npx hexo generate

    - name: Deploy to GitHub Pages
      uses: peaceiris/actions-gh-pages@v3
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        publish_dir: ./blog/public
        cname: yourdomain.com  # 如果有自定义域名
```

## 常见问题

### 问题 1: 推送时需要认证

**解决方法**:
- HTTPS 方式: 使用 GitHub Personal Access Token 替代密码
  1. 访问 https://github.com/settings/tokens
  2. 点击 "Generate new token" → "Generate new token (classic)"
  3. 勾选 `repo` 权限
  4. 生成 token 并复制
  5. 推送时,在输入密码的地方粘贴 token

### 问题 2: 用户名和邮箱未配置

```bash
git config --global user.name "你的用户名"
git config --global user.email "你的邮箱"
```

### 问题 3: 推送失败

**检查项**:
1. 仓库 URL 是否正确
2. 是否有推送权限
3. 网络连接是否正常
4. 用户名和密码/token 是否正确

## 完整的推送命令 (复制粘贴即可)

假设你的 GitHub 用户名是 `YOUR_USERNAME`,仓库名是 `blog-refactor`:

```bash
cd d:\大四下\博客修复与重整
git init
git add .
git commit -m "feat: 博客重整完成"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/blog-refactor.git
git push -u origin main
```

执行到 `git push` 时会提示输入用户名和密码:
- Username: 你的 GitHub 用户名
- Password: 你的 GitHub Personal Access Token

## 下一步

1. 按照**步骤一**在 GitHub 创建仓库
2. 执行**步骤二**的命令推送代码
3. 查看你的 GitHub 仓库,确认代码已成功推送
4. 如需部署博客,按照**步骤三**操作

---

**提示**: 如果遇到问题,请检查每一步的输出信息,或者告诉我具体的错误信息。
