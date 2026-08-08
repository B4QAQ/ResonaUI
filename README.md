<p align="center">
  <img src="src/common/logo.png" width="120" alt="ResonaUI Logo">
</p>

<h1 align="center">ResonaUI</h1>
<p align="center"><strong>Simple, Lite, Easy, by Design</strong></p>
<p align="center">基于 XiaomiVela 的可穿戴设备 UI 框架</p>

<p align="center">
  <a href="#-特性">特性</a> •
  <a href="#-快速开始">快速开始</a> •
  <a href="#-项目结构">项目结构</a> •
  <a href="#-开发指南">开发指南</a> •
  <a href="#-构建部署">构建部署</a>
</p>

---

## ✨ 特性

### 🎯 Simple - 简约至上
- **极简设计**：专为小屏可穿戴设备优化，减少视觉噪音
- **直观模块**：清晰的模块划分，`global.uiAdm`、`global.storageManager`、`global.fetchManager` 触手可及
- **统一规范**：一套代码适配圆形、方形、药丸形等多种表盘形态

### 🪶 Lite - 轻量高效
- **内存友好**：针对手环等资源受限设备深度优化，分批渲染、及时释放
- **按需加载**：页面组件按需引入，减少首屏加载时间
- **GC 机制**：内置页面池自动回收，防止内存泄漏

### 🚀 Easy - 开箱即用
- **动画系统**：内置页面过渡动画，开箱即用
- **键盘组件**：完整的输入法支持，光标控制、选区操作一应俱全
- **设置框架**：灵活的设置项配置，支持列表、事件、帮助文档等多种类型

### 🎨 by Design - 设计驱动
- **响应式布局**：智能适配不同屏幕尺寸与形状
- **主题系统**：全局 CSS 变量，轻松定制应用风格
- **组件复用**：通用组件抽象，减少重复代码

---

## 📦 快速开始

### 环境要求

- Node.js >= 8.10
- pnpm（推荐）或 npm

### 安装依赖

```bash
# 使用 pnpm（推荐）
pnpm install

# 或使用 npm
npm install
```

### 启动开发

```bash
pnpm start
```

### 代码规范化

```bash
# macOS / Linux
sh husky.sh

# Windows
./husky.sh
```

---

## 📁 项目结构

```
ResonaUI-Example/
├── src/
│   ├── common/
│   │   ├── css/           # 全局样式
│   │   ├── js/            # 核心模块
│   │   │   ├── uiAdm.js   # UI 管理（动画、页面池）
│   │   │   ├── storage.js # 数据存储
│   │   │   ├── fetch.js   # 网络请求
│   │   │   └── useful.js  # 工具函数
│   │   └── others/        # 静态资源
│   ├── components/        # 可复用组件
│   ├── pages/             # 页面
│   │   ├── index/         # 主页
│   │   ├── init/          # 初始化向导
│   │   └── settings/      # 设置页面
│   ├── app.ux             # 应用入口
│   └── manifest.json      # 应用配置
├── VelaDocs/              # Vela 开发文档
├── AGENTS.md              # AI 辅助开发规范
└── commitlint.config.js   # 提交规范配置
```

---

## 🛠 开发指南

### 全局模块

ResonaUI 将常用模块挂载到 `global`，无需重复 import：

```javascript
// UI 管理
global.uiAdm.registerPage(this.$page.name, this)
global.uiAdm.unregisterPage(this.$page.name)
global.uiAdm.MessageBox('操作成功')

// 数据存储
await global.storageManager.getSettings()
await global.storageManager.saveSettings({ key: value })

// 网络请求
const result = await global.fetchManager.sendFetch('/api/path', true, { param: 'value' })
```

### 页面开发

```javascript
// 1. 注册页面（onInit）
global.uiAdm.registerPage(this.$page.name, this)

// 2. 注销页面（onDestroy）
global.uiAdm.unregisterPage(this.$page.name)

// 3. 页面跳转
this.route('settings/settingslist', { title: '偏好设置' })

// 4. 返回上一页
this.back()
```

### 设置项配置

```javascript
// 支持多种设置项类型
set: [
  { title: '动画选项', lore: '性能设置', type: 'list', val: '0', valList: ['关闭', '开启'] },
  { title: '清除数据', lore: '谨慎操作', type: 'event', val: '0', valList: ['确认', '清除中'] },
  { title: '使用文档', lore: '[QR:https://docs.example.com,扫码查看]', type: 'help', val: false },
]
```

## 🔨 构建部署

### 开发构建

```bash
pnpm build
```

### 发布构建

```bash
pnpm release
```

产物输出到 `dist/` 目录。

---

## 📱 设备适配

ResonaUI 支持多种可穿戴设备形态：

| 形态 | 屏幕形状 | 适配方式 |
|------|----------|----------|
| 圆形 | `circle` | `@media screen and (shape: circle)` |
| 方形 | `rect` | `@media screen and (shape: rect)` |
| 药丸形 | `pill-shaped` | `@media screen and (shape: pill-shaped)` |

### 设备信息获取

```javascript
const info = await getDeviceInfo()
console.log(info.screenWidth)    // 屏幕宽度
console.log(info.screenShape)    // 屏幕形状
console.log(info.product)        // 设备代号
```

---

## 📖 相关文档

- [XiaomiVela 开发文档](https://iot.mi.com/vela/quickapp/zh/guide/)
- [VelaDocs 本地文档](./VelaDocs/)（项目内置）
- [AGENTS.md](./AGENTS.md) - AI 辅助开发规范

---

## 🤝 参与贡献

1. Fork 本仓库
2. 创建功能分支：`git checkout -b feat/your-feature`
3. 提交更改：`git commit -m 'feat: add your feature'`
4. 推送分支：`git push origin feat/your-feature`
5. 提交 Pull Request

---

## 📄 许可证

本项目采用 [AGPL-3.0](https://www.gnu.org/licenses/agpl-3.0.html) 许可证。

**common/** 目录下的核心模块（uiAdm.js、storage.js、fetch.js、useful.js）均为 AGPL-3.0 协议。

---

<p align="center">
  <strong>ResonaUI</strong> - 让可穿戴设备开发更简单
  <br>
  <sub>Built with ❤️ for XiaomiVela</sub>
</p>
