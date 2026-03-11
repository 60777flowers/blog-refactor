# GitHub Actions 部署失败故障排除

## 问题
GitHub Actions 工作流 "Build and Deploy" 失败

## 可能的原因

### 1. GitHub Pages 权限不足
**症状**: 工作流在部署步骤失败

**解决方案**:

1. 访问仓库设置: https://github.com/60777flowers/blog-refactor/settings/actions

2. 在 "Workflow permissions" 部分,确保选择:
   - ✅ **Read and write permissions**

3. 点击 **Save** 保存设置

---

### 2. GitHub Pages 设置问题
**症状**: 工作流成功但页面未更新

**解决方案**:

1. 访问 GitHub Pages 设置: https://github.com/60777flowers/blog-refactor/settings/pages

2. 确保 "Source" 选择为:
   - ✅ **GitHub Actions**

3. 如果显示其他选项,点击 **Edit** 改为 **GitHub Actions**

---

### 3. 仓库权限问题
**症状**: 没有权限部署到 Pages

**解决方案**:

1. 检查你是否是仓库的所有者
2. 如果是组织仓库,确保组织允许你部署 Pages

---

### 4. 工作流权限配置
**症状**: "Resource not accessible by integration" 错误

**解决方案**:

确保 `.github/workflows/pages.yml` 文件包含以下权限:

```yaml
permissions:
  contents: write
  pages: write
  id-token: write
```

我已经更新了工作流文件,包含了这些权限。

---

## 快速修复步骤

### 步骤 1: 更新仓库设置

1. 访问: https://github.com/60777flowers/blog-refactor/settings/actions
2. 在 "Workflow permissions" 下选择:
   - **Read and write permissions**
3. 点击 **Save**

### 步骤 2: 确认 Pages 设置

1. 访问: https://github.com/60777flowers/blog-refactor/settings/pages
2. 确认 "Source" 显示为 **GitHub Actions**

### 步骤 3: 重新运行工作流

1. 访问: https://github.com/60777flowers/blog-refactor/actions
2. 找到最新的 "Build and Deploy" 工作流
3. 点击右侧的 **...** 按钮
4. 选择 **Re-run jobs**
5. 等待工作流完成

---

## 验证部署成功

工作流成功后,你应该看到:
- ✅ 绿色的对勾标记
- ✅ 状态显示为 "Success"

然后访问博客: https://60777flowers.github.io/blog-refactor/

---

## 如果仍然失败

### 方案 A: 使用 gh-pages 分支部署

如果 GitHub Actions 一直有问题,可以使用传统方法:

```bash
cd d:\大四下\博客修复与重整\blog
npx hexo clean
npx hexo generate

cd ..
git subtree push --prefix blog/public origin gh-pages
```

然后在 Pages 设置中选择:
- Source: **Deploy from a branch**
- Branch: **gh-pages** 和 **/(root)**

---

### 方案 B: 手动上传静态文件

如果以上方法都不行:

1. 生成静态文件:
```bash
cd d:\大四下\博客修复与重整\blog
npx hexo clean
npx hexo generate
```

2. 在浏览器中访问: https://github.com/new
3. 创建仓库: `60777flowers.github.io`
4. 选择 Public
5. 上传 `blog/public` 文件夹中的所有文件

---

## 检查工作流日志

1. 访问: https://github.com/60777flowers/blog-refactor/actions
2. 点击失败的 "Build and Deploy" 运行
3. 展开每个步骤查看详细日志
4. 找到红色的错误信息
5. 告诉我具体的错误内容

---

## 常见错误信息

### "Resource not accessible by integration"
**原因**: GitHub Actions 权限不足
**解决**: 按照上面的"步骤 1"设置权限

### "Error: Invalid artifact url"
**原因**: 工作流配置问题
**解决**: 已更新工作流文件,请重新运行

### "Error: Pages build failed"
**原因**: 静态文件生成失败
**解决**: 检查本地 `npx hexo generate` 是否成功

---

## 现在应该做什么?

1. 首先,按照"快速修复步骤"配置权限
2. 然后重新运行工作流
3. 如果还有问题,查看工作流日志并告诉我具体的错误信息

---

**注意**: 工作流可能需要 1-2 分钟才能完成,请耐心等待。
