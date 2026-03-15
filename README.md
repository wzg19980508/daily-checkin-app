# 📅 每日打卡小程序

一个简洁美观的每日习惯打卡应用，帮助你建立和坚持好习惯。

## ✨ 功能特性

- **📋 习惯管理**: 添加、编辑、删除你的每日习惯
- **✅ 快速打卡**: 一键完成每日打卡，记录成长轨迹
- **📆 日历视图**: 直观查看每月的打卡情况
- **📊 数据统计**: 追踪完成率、连续打卡天数
- **🏆 成就系统**: 解锁徽章，激励自己坚持
- **🎨 精美 UI**: 现代化设计，流畅动画效果

## 🚀 在线演示

访问：[https://your-username.github.io/daily-checkin-app](https://your-username.github.io/daily-checkin-app)

## 🛠️ 本地开发

### 环境要求

- Node.js >= 18.0.0
- npm >= 9.0.0

### 安装运行

```bash
# 克隆项目
git clone https://github.com/your-username/daily-checkin-app.git

# 进入目录
cd daily-checkin-app

# 安装依赖
npm install

# 启动开发服务器
npm run dev

# 构建生产版本
npm run build

# 预览生产构建
npm run preview
```

## 📱 技术栈

- **Vue 3** - 渐进式 JavaScript 框架
- **Vite** - 下一代前端构建工具
- **Tailwind CSS** - 实用优先的 CSS 框架
- **GitHub Pages** - 静态网站托管

## 🎨 UI 设计

### 配色方案

- 主色：蓝色 (#3B82F6) - 代表信任与专业
- 辅助色：紫色 (#7C3AED) - 代表成长与进步
- 成功色：绿色 (#10B981) - 代表完成与成就
- 背景：渐变灰白 - 简洁清爽

### 设计原则

1. **简洁直观**: 减少认知负担，一眼看懂
2. **即时反馈**: 每次操作都有视觉反馈
3. **正向激励**: 通过进度条、徽章等激励用户
4. **移动优先**: 响应式设计，适配各种屏幕

## 📂 项目结构

```
daily-checkin-app/
├── src/
│   ├── App.vue          # 主应用组件
│   ├── main.js          # 应用入口
│   ├── style.css        # 全局样式
│   └── views/           # 页面组件
│       ├── HomeView.vue     # 首页
│       ├── CalendarView.vue # 日历页
│       └── StatsView.vue    # 统计页
├── index.html           # HTML 模板
├── vite.config.js       # Vite 配置
├── package.json         # 项目依赖
└── README.md            # 项目说明
```

## 🔧 部署到 GitHub Pages

```bash
# 安装 gh-pages
npm install -D gh-pages

# 构建项目
npm run build

# 部署到 GitHub Pages
npx gh-pages -d dist
```

然后在 GitHub 仓库设置中启用 GitHub Pages。

## 📝 更新日志

### v1.0.0 (2026-03-15)
- ✨ 初始版本发布
- 🏠 首页打卡功能
- 📆 日历视图
- 📊 数据统计
- 🏆 成就系统

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

## 📄 许可证

MIT License

---

**坚持每一天，成就更好的自己！** 💪
