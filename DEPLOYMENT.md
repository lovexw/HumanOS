# Cloudflare Pages 部署指南

本文档详细说明如何将人体器官健康保养指南网站部署到Cloudflare Pages。

## 📋 前置要求

- Cloudflare 账户（免费）
- Git 仓库（GitHub、GitLab 或 Bitbucket）或本地项目文件

## 🚀 部署方法

### 方法一：通过 Git 连接（推荐）

这是最推荐的方法，支持自动部署和版本管理。

#### 步骤 1: 准备 Git 仓库

如果还没有，先创建 Git 仓库：

```bash
cd /path/to/your/project
git init
git add .
git commit -m "Initial commit: Health guide website"
```

将代码推送到 GitHub/GitLab：

```bash
git remote add origin https://github.com/yourusername/health-guide.git
git branch -M main
git push -u origin main
```

#### 步骤 2: 在 Cloudflare 创建 Pages 项目

1. 登录 [Cloudflare Dashboard](https://dash.cloudflare.com/)
2. 在左侧菜单选择 **Pages**
3. 点击 **Create a project**
4. 选择 **Connect to Git**
5. 授权 Cloudflare 访问你的 Git 仓库
6. 选择你的仓库

#### 步骤 3: 配置构建设置

在 "Set up builds and deployments" 页面：

- **Project name**: `health-guide`（或你喜欢的名称）
- **Production branch**: `main`
- **Framework preset**: `None`
- **Build command**: 留空（这是纯静态网站）
- **Build output directory**: `/`
- **Root directory**: `/`（或留空）
- **Environment variables**: 无需设置

#### 步骤 4: 部署

1. 点击 **Save and Deploy**
2. 等待几分钟，Cloudflare 会自动部署你的网站
3. 部署完成后，你会获得一个 `.pages.dev` 域名

#### 步骤 5: 访问网站

部署成功后，你的网站将可以通过以下地址访问：
```
https://health-guide-xxx.pages.dev
```

### 方法二：直接上传文件

如果你不想使用 Git，可以直接上传文件。

#### 步骤：

1. 登录 [Cloudflare Dashboard](https://dash.cloudflare.com/)
2. 进入 **Pages**
3. 点击 **Create a project**
4. 选择 **Upload assets**
5. 拖拽或选择项目文件夹
6. 点击 **Deploy site**

**注意**：此方法不支持自动部署，每次更新需要手动上传。

### 方法三：使用 Wrangler CLI

适合开发者使用命令行工具。

#### 步骤 1: 安装 Wrangler

```bash
npm install -g wrangler
# 或
yarn global add wrangler
```

#### 步骤 2: 登录 Cloudflare

```bash
wrangler login
```

这会打开浏览器进行身份验证。

#### 步骤 3: 部署项目

```bash
cd /path/to/your/project
wrangler pages publish . --project-name=health-guide
```

#### 步骤 4: 后续更新

每次更新后，只需再次运行：

```bash
wrangler pages publish . --project-name=health-guide
```

## 🌐 自定义域名

部署后，你可以添加自定义域名。

### 步骤：

1. 在 Cloudflare Pages 项目中，进入 **Custom domains**
2. 点击 **Set up a custom domain**
3. 输入你的域名（如 `health.example.com`）
4. 按照提示在你的域名 DNS 设置中添加 CNAME 记录：
   ```
   CNAME: health.example.com -> health-guide-xxx.pages.dev
   ```
5. 等待 DNS 生效（通常几分钟到几小时）

## 🔄 自动部署

使用 Git 连接方式时，每次推送到主分支都会自动触发部署：

```bash
git add .
git commit -m "Update content"
git push
```

Cloudflare 会自动检测变更并重新部署网站。

### 预览部署

推送到非主分支时，Cloudflare 会创建预览部署：

```bash
git checkout -b feature-update
# 修改文件
git add .
git commit -m "Add new feature"
git push origin feature-update
```

这会生成一个预览 URL，可以在合并到主分支前测试。

## ⚙️ 高级配置

### 环境变量

虽然这个项目不需要，但如果需要，可以在项目设置中添加环境变量：

1. 进入项目 **Settings**
2. 选择 **Environment variables**
3. 添加变量（如 `API_KEY`）

### 自定义构建命令

如果将来需要构建步骤（如使用构建工具），可以在项目设置中配置：

```bash
# Build command 示例
npm run build
# 或
make build
```

### Headers 和 Redirects

项目中已包含：
- `_headers` - 设置安全响应头和缓存策略
- `_redirects` - 配置 URL 重定向规则

这些文件会被 Cloudflare Pages 自动识别和应用。

## 📊 监控和分析

### Web Analytics

启用 Cloudflare Web Analytics（免费）：

1. 在项目设置中找到 **Web Analytics**
2. 点击 **Enable**
3. 获取访问统计数据（无需 cookie，隐私友好）

### 部署历史

查看所有部署历史：

1. 进入项目主页
2. 查看 **Deployments** 选项卡
3. 可以回滚到任何历史版本

## 🐛 故障排查

### 问题：部署失败

**解决方案**：
- 检查 Build output directory 是否设置为 `/`
- 确保所有文件都已提交到 Git 仓库
- 查看部署日志了解具体错误

### 问题：网站样式不正常

**解决方案**：
- 清除浏览器缓存
- 检查文件路径是否正确（使用相对路径）
- 在浏览器开发者工具查看是否有 404 错误

### 问题：自定义域名不工作

**解决方案**：
- 等待 DNS 传播（可能需要几小时）
- 使用 `dig` 或 `nslookup` 检查 DNS 记录
- 确保 CNAME 记录正确指向 `.pages.dev` 域名

### 问题：更新没有生效

**解决方案**：
- 强制刷新浏览器（Ctrl+Shift+R 或 Cmd+Shift+R）
- 检查 Cloudflare Pages 是否完成部署
- 清除 Cloudflare 缓存

## 💡 性能优化

Cloudflare Pages 已经提供了很多优化：

- ✅ 全球 CDN 分发
- ✅ 自动 HTTPS
- ✅ HTTP/2 和 HTTP/3
- ✅ Brotli 压缩
- ✅ 免费无限带宽

额外优化建议：

1. **图片优化**：使用 WebP 格式和适当尺寸
2. **代码压缩**：CSS 和 JS 已经很简洁，必要时可以使用压缩工具
3. **字体优化**：已使用 Google Fonts，可考虑自托管字体
4. **资源预加载**：在 HTML 中添加 `<link rel="preconnect">`（已添加）

## 📱 移动端优化

网站已经是响应式设计，在移动端测试：

1. 使用浏览器开发者工具的设备模拟器
2. 在真实手机上测试
3. 使用 [Google Mobile-Friendly Test](https://search.google.com/test/mobile-friendly)

## 🔒 安全性

已配置的安全措施（在 `_headers` 文件中）：

- `X-Frame-Options: DENY` - 防止点击劫持
- `X-Content-Type-Options: nosniff` - 防止 MIME 类型混淆
- `X-XSS-Protection: 1; mode=block` - XSS 保护
- `Referrer-Policy` - 控制 Referrer 信息
- `Permissions-Policy` - 限制浏览器功能访问

## 📈 SEO 优化

已包含的 SEO 功能：

- ✅ 语义化 HTML
- ✅ Meta 标签（description, keywords）
- ✅ `robots.txt` 文件
- ✅ `sitemap.xml` 文件
- ✅ 响应式设计
- ✅ 快速加载速度

部署后记得：

1. 在 `sitemap.xml` 中更新域名
2. 在 `robots.txt` 中更新 Sitemap URL
3. 提交 sitemap 到 Google Search Console

## 🎉 部署成功！

恭喜！你的人体器官健康保养指南网站已成功部署到 Cloudflare Pages。

现在你可以：
- 分享你的网站链接
- 添加自定义域名
- 继续添加更多内容
- 监控访问统计

有问题？查看 [Cloudflare Pages 文档](https://developers.cloudflare.com/pages/)

---

**祝你的健康网站帮助更多人！💚**
