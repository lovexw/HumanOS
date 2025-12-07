# 人体器官健康保养指南 🫀

一个全面、优雅、现代的人体器官健康保养静态网站，提供详细的器官功能说明、保养方法和预防措施。

## ✨ 特点

- 📚 **全面覆盖**：包含20+种主要人体器官的详细信息
- 🎨 **优雅设计**：现代化UI设计，渐变色彩，流畅动画
- 📱 **响应式布局**：完美支持桌面、平板、手机设备
- 🔍 **智能筛选**：按器官类别快速筛选查看
- 💡 **详细指南**：每个器官都有功能介绍、保养方法、注意事项
- 🚀 **纯静态**：无需后端，可直接部署到Cloudflare Pages

## 🏥 涵盖器官系统

### 重要器官
- ❤️ 心脏 - 生命的动力泵
- 🧠 大脑 - 思维与意识的中枢
- 🫘 肾脏 - 体内净化器
- 🤲 皮肤 - 人体最大器官
- 🩸 脾脏 - 免疫和造血功能
- 🦴 骨骼 - 身体的支架
- 💪 肌肉 - 运动系统核心
- 💧 膀胱 - 尿液的储存库
- 🔴 血管系统 - 生命的运输网络
- 🛡️ 淋巴系统 - 免疫防御网络

### 消化系统
- 🫀 肝脏 - 人体化工厂
- 🫃 胃 - 消化食物的主要场所
- 🌀 肠道 - 营养吸收和免疫防线
- 🦷 牙齿 - 咀嚼的第一道关卡

### 呼吸系统
- 🫁 肺 - 呼吸系统核心

### 感觉器官
- 👁️ 眼睛 - 心灵的窗户
- 👂 耳朵 - 听觉与平衡器官
- 👅 舌头 - 味觉器官

### 内分泌系统
- 🔬 胰腺 - 调节血糖和消化酶分泌
- 🦋 甲状腺 - 代谢调控中心

## 🚀 部署到Cloudflare Pages

### 方法一：使用Git（推荐）

1. 将代码推送到GitHub/GitLab仓库
2. 登录 [Cloudflare Dashboard](https://dash.cloudflare.com/)
3. 进入 Pages 页面
4. 点击 "Create a project"
5. 连接你的Git仓库
6. 配置构建设置：
   - **Build command**: 留空（纯静态网站）
   - **Build output directory**: `/`
7. 点击 "Save and Deploy"

### 方法二：直接上传

1. 登录 [Cloudflare Dashboard](https://dash.cloudflare.com/)
2. 进入 Pages 页面
3. 点击 "Create a project" > "Upload assets"
4. 上传整个项目文件夹
5. 网站将自动部署

### 方法三：使用Wrangler CLI

```bash
# 安装Wrangler
npm install -g wrangler

# 登录Cloudflare
wrangler login

# 部署
wrangler pages publish . --project-name=health-guide
```

## 📁 项目结构

```
.
├── index.html          # 主页面
├── styles.css          # 样式表
├── script.js           # 交互脚本
├── README.md           # 项目说明
└── .gitignore          # Git忽略文件
```

## 💻 本地开发

无需安装任何依赖，直接打开 `index.html` 即可在浏览器中查看。

或使用简单的HTTP服务器：

```bash
# Python 3
python -m http.server 8000

# Node.js (需要先安装 http-server)
npx http-server

# PHP
php -S localhost:8000
```

然后访问 `http://localhost:8000`

## 🎨 自定义

### 修改颜色主题

在 `styles.css` 的 `:root` 部分修改CSS变量：

```css
:root {
    --primary-color: #3b82f6;      /* 主色调 */
    --secondary-color: #10b981;     /* 辅助色 */
    --accent-color: #f59e0b;        /* 强调色 */
    /* ... */
}
```

### 添加新器官

在 `script.js` 的 `organData` 对象中添加新器官数据：

```javascript
newOrgan: {
    icon: '🫀',
    name: '器官名称',
    subtitle: '简短描述',
    functions: '详细功能说明...',
    care: ['保养方法1', '保养方法2', ...],
    avoid: ['避免事项1', '避免事项2', ...]
}
```

然后在 `index.html` 中添加对应的卡片。

## 📱 浏览器支持

- Chrome (推荐)
- Firefox
- Safari
- Edge
- 移动端浏览器

## 📄 许可证

本项目仅供教育和学习目的使用。网站内容来源于公开健康知识，使用前请咨询专业医疗人士。

## ⚠️ 免责声明

本网站提供的信息仅供参考，不能替代专业医疗建议、诊断或治疗。如有健康问题，请咨询专业医疗机构和医生。

## 🤝 贡献

欢迎提交问题和改进建议！

## 📧 联系方式

如有问题或建议，请提交Issue。

---

**关爱健康，从了解开始 💚**
