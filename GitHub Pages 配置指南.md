# GitHub Pages 配置指南

## 问题说明

你的博客项目使用了 GitHub Actions 来自动构建和部署,但遇到以下问题:
1. 之前的工作流使用了过时的 `peaceiris/actions-gh-pages@v3` 方法
2. GitHub Pages 设置需要配置正确的源
3. 工作流失败导致自动部署无法正常工作

## 解决方案

### 方案一:修复 GitHub Actions 工作流(推荐)

我已经更新了 `.github/workflows/pages.yml` 文件,使用最新的 GitHub Actions Pages 部署方法。

#### 1. 配置 GitHub Pages 设置

1. 访问你的仓库设置: https://github.com/60777flowers/blog-refactor/settings/pages
2. 在 "Build and deployment" 部分找到 "Source"
3. 选择 **GitHub Actions**
4. 点击 **Save**

#### 2. 重新运行工作流

1. 访问 Actions 页面: https://github.com/60777flowers/blog-refactor/actions
2. 找到最新的 "Build and Deploy" 工作流
3. 点击 "Re-run jobs" 按钮
4. 等待工作流完成(约 1-2 分钟)

#### 3. 访问博客

工作流成功后,你的博客将部署到:
- **https://60777flowers.github.io/blog-refactor/**

---

### 方案二:使用 GitHub Pages 的 Branch 部署(备用方案)

如果方案一仍然有问题,可以使用传统的分支部署方式。

#### 步骤 1: 创建 gh-pages 分支

```bash
cd d:\大四下\博客修复与重整\blog
npx hexo clean
npx hexo generate

cd ..
git subtree push --prefix blog/public origin gh-pages
```

#### 步骤 2: 配置 GitHub Pages

1. 访问 https://github.com/60777flowers/blog-refactor/settings/pages
2. Source 选择: **Deploy from a branch**
3. Branch 选择: **gh-pages** 和 **/(root)**
4. 点击 **Save**

#### 步骤 3: 访问博客

等待 2-5 分钟后访问: https://60777flowers.github.io/blog-refactor/

---

### 方案三:手动上传静态文件(最简单)

如果自动化部署一直有问题,可以手动上传。

#### 步骤 1: 生成静态文件

```bash
cd d:\大四下\博客修复与重整\blog
npx hexo clean
npx hexo generate
```

#### 步骤 2: 上传到 GitHub

1. 访问: https://github.com/new
2. Repository name: `60777flowers.github.io`
3. Public: 选择 **Public**
4. 点击 **Create repository**

5. 访问: https://github.com/60777flowers/60777flowers.github.io
6. 点击 "uploading an existing file"
7. 将 `blog/public` 文件夹中的所有文件拖入
8. 点击 **Commit changes**

#### 步骤 3: 配置 GitHub Pages

1. 访问: https://github.com/60777flowers/60777flowers.github.io/settings/pages
2. Source 选择: **Deploy from a branch**
3. Branch 选择: **main** 和 **/(root)**
4. 点击 **Save**

#### 步骤 4: 访问博客

等待 2-5 分钟后访问: https://60777flowers.github.io/

---

## 验证部署状态

### 检查工作流状态

1. 访问: https://github.com/60777flowers/blog-refactor/actions
2. 查看最新的 "Build and Deploy" 工作流
3. 应该显示 ✅ 绿色对勾

### 检查部署状态

1. 访问: https://github.com/60777flowers/blog-refactor/settings/pages
2. 查看 "Deployment" 部分
3. 应该显示 "Your site is live at: https://60777flowers.github.io/blog-refactor/"

---

## 常见问题

### 问题 1: 工作流失败 "pages build and deployment failed"

**原因**:
- GitHub Pages 设置未配置为 GitHub Actions
- 工作流权限不足

**解决**:
1. 确保在仓库 Settings → Pages 中选择了 "GitHub Actions" 作为 Source
2. 检查仓库 Settings → Actions → General,确保 "Workflow permissions" 选择 "Read and write permissions"

### 问题 2: 部署成功但页面显示 404

**原因**:
- 网站刚部署,需要等待几分钟
- 缓存问题

**解决**:
1. 等待 2-5 分钟后重试
2. 清除浏览器缓存
3. 使用无痕模式访问

### 问题 3: 样式文件加载失败

**原因**:
- 静态资源路径不正确
- 缺少必要的文件

**解决**:
1. 检查 `blog/public` 文件夹是否包含所有必要的文件
2. 查看浏览器控制台的错误信息
3. 重新生成静态文件:`npx hexo clean && npx hexo generate`

---

## 推荐方案

**推荐使用方案一**(GitHub Actions),因为:

✅ 自动化: 每次推送代码都会自动部署
✅ 简单: 不需要手动上传文件
✅ 高效: 构建速度快,使用 GitHub 的官方 Actions
✅ 可靠: 使用官方的 `actions/deploy-pages@v4`

---

## 下一步

1. 按照**方案一**配置 GitHub Pages 设置
2. 重新运行工作流
3. 等待部署完成
4. 访问你的博客

如果方案一有问题,再尝试方案二或方案三。

---

**最后更新**: 2026-03-11
**文档版本**: 1.0
