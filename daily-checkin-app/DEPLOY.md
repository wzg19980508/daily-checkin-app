# 🚀 部署指南

## 方式一：GitHub Pages（推荐）

### 步骤 1: 创建 GitHub 仓库

1. 登录 GitHub: https://github.com
2. 点击右上角 **+** → **New repository**
3. 仓库名：`daily-checkin-app`
4. 可见性：选择 **Public**（公开）
5. 点击 **Create repository**

### 步骤 2: 推送代码到 GitHub

在项目目录下执行以下命令（替换 `your-username` 为你的 GitHub 用户名）：

```bash
cd /home/admin/openclaw/workspace/daily-checkin-app

# 添加远程仓库（替换 your-username）
git remote add origin https://github.com/your-username/daily-checkin-app.git

# 推送到 GitHub
git push -u origin master
```

### 步骤 3: 启用 GitHub Pages

1. 进入你的 GitHub 仓库页面
2. 点击 **Settings** → **Pages**
3. 在 **Build and deployment** 部分：
   - Source: 选择 **GitHub Actions**
4. 等待部署完成（约 1-2 分钟）

### 步骤 4: 访问你的应用

部署完成后，你的应用将在以下地址可用：

```
https://your-username.github.io/daily-checkin-app/
```

---

## 方式二：Vercel 部署（备选）

### 步骤 1: 安装 Vercel CLI

```bash
npm install -g vercel
```

### 步骤 2: 登录 Vercel

```bash
vercel login
```

### 步骤 3: 部署

```bash
cd /home/admin/openclaw/workspace/daily-checkin-app
vercel
```

按提示操作即可完成部署。

---

## 方式三：Netlify 部署（备选）

### 步骤 1: 登录 Netlify

访问：https://app.netlify.com

### 步骤 2: 拖拽部署

1. 先构建项目：`npm run build`
2. 将 `dist` 文件夹拖拽到 Netlify 的部署区域
3. 等待部署完成

---

## 常见问题

### Q: 推送时提示需要认证？

**A:** 可以使用以下方式之一：

1. **GitHub Token**（推荐）:
   ```bash
   git remote add origin https://YOUR_TOKEN@github.com/your-username/daily-checkin-app.git
   ```

2. **SSH 方式**:
   ```bash
   # 生成 SSH 密钥
   ssh-keygen -t ed25519 -C "your_email@example.com"
   
   # 将公钥添加到 GitHub: Settings → SSH and GPG keys
   cat ~/.ssh/id_ed25519.pub
   
   # 使用 SSH 地址
   git remote add origin git@github.com:your-username/daily-checkin-app.git
   ```

### Q: GitHub Pages 显示 404？

**A:** 等待 1-2 分钟，部署需要时间。检查 Actions 标签页查看部署状态。

### Q: 如何自定义域名？

**A:** 在 GitHub Pages 设置中添加自定义域名，然后在你的域名提供商处配置 CNAME 记录。

---

## 需要帮助？

如果遇到问题，请检查：

1. ✅ Node.js 版本 >= 18
2. ✅ 所有依赖已安装 (`npm install`)
3. ✅ 构建成功 (`npm run build`)
4. ✅ GitHub Actions 工作流已启用

祝你部署顺利！🎉
