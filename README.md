# OpenClaw Manager

OpenClaw-Easy：包含 Electron 桌面端与 Web 前端的多包仓库，用于一站式构建与发布

## 📋 项目简介

OpenClaw Manager 是一个基于 Monorepo 架构的现代化应用项目，提供 Electron 桌面应用和 Web 前端两种形态。项目使用 pnpm + Turbo 进行高效的包管理和构建优化。

## 🛠 技术栈

- **包管理器**: pnpm 10.26.1
- **构建工具**: Turbo
- **桌面应用**: Electron + React + TypeScript + Rspack
- **Web 应用**: Next.js 16 + React 19 + TypeScript
- **样式**: TailwindCSS 4
- **UI 组件**: shadcn-ui
- **状态管理**: Zustand
- **代码规范**: ESLint + Prettier

## 📁 项目结构

```
openclaw-manager/
├── apps/
│   ├── electron-app/          # Electron 桌面应用
│   │   ├── src/
│   │   │   ├── main/         # Electron 主进程
│   │   │   └── preload/      # 预加载脚本
│   │   └── package.json
│   └── open-claw/             # Web 前端应用 (Next.js)
│       ├── src/
│       │   ├── app/          # Next.js App Router
│       │   ├── components/   # React 组件
│       │   ├── lib/          # 工具函数
│       │   └── store/        # Zustand 状态管理
│       └── package.json
├── packages/
│   ├── electron-core/         # Electron 核心功能包
│   ├── electron-ipc/          # IPC 通信包
│   └── electron-window/       # 窗口管理包
├── .github/                   # GitHub Actions 工作流
└── package.json               # 根目录配置
```

## 🚀 快速开始

### 环境要求

- Node.js (推荐 v18+)
- pnpm 10.26.1

### 安装依赖

```bash
# 安装所有依赖
pnpm install
```

## 💻 开发指南

### 启动 Web 应用

```bash
# 仅启动 Next.js Web 应用
cd apps/open-claw
pnpm dev
```

访问 `http://localhost:3000` 查看应用。

### 启动 Electron 应用（完整流程）

**重要**：Electron 应用需要 Next.js 开发服务器在 `http://localhost:3000` 运行，否则会显示白屏。

#### 方法 1：使用两个终端（推荐）

**终端 1：启动 Next.js 开发服务器**
```bash
cd apps/open-claw
pnpm dev
```

等待看到输出：
```
▲ Next.js 16.1.6
- Local:        http://localhost:3000
```

**终端 2：构建共享包并启动 Electron**
```bash
# 构建共享包
cd packages/electron-core && pnpm build
cd ../electron-ipc && pnpm build
cd ../electron-window && pnpm build

# 启动 Electron 应用
cd ../../apps/electron-app
pnpm dev
```

#### 方法 2：使用 Turbo 一次性构建

```bash
# 构建所有包（包括共享包）
pnpm build

# 然后按方法 1 的步骤启动 Next.js 和 Electron
```

### 启动所有应用

```bash
# 使用 Turbo 启动所有应用（注意：这不会自动构建共享包）
pnpm dev
```

### 代码检查

```bash
# 运行 ESLint（自动修复）
pnpm lint

# 运行 ESLint（仅检查，CI 模式）
pnpm lint:ci

# 运行类型检查
pnpm typecheck
```

### 代码格式化

```bash
# 格式化所有代码
pnpm format

# 检查代码格式
pnpm format:ci
```

## 🏗 构建指南

### 构建所有应用

```bash
# 构建所有包（包括共享包）
pnpm build
```

### 构建 Electron 应用

```bash
# 构建 Windows 版本
pnpm build:electron:win

# 构建 macOS 版本（通用）
pnpm build:electron:mac

# 构建 macOS Intel 版本
pnpm build:electron:mac-intel

# 构建 macOS ARM 版本
pnpm build:electron:mac-arm

# 构建所有平台
pnpm build:electron
```

### 构建 Web 应用

```bash
# 在根目录构建
pnpm react:build

# 或者在 apps/open-claw 目录下构建
cd apps/open-claw && pnpm build
```

## 🧹 清理

```bash
# 清理所有构建产物
pnpm clean
```

## 📦 其他工具

```bash
# 下载 ytdlp 工具
pnpm download-ytdlp
```

## ❓ 常见问题

### Electron 应用显示白屏

**原因**：Next.js 开发服务器未启动或无法访问 `http://localhost:3000`

**解决方案**：
1. 确保先启动 Next.js 开发服务器：`cd apps/open-claw && pnpm dev`
2. 在浏览器中访问 `http://localhost:3000` 确认服务正常运行
3. 然后再启动 Electron 应用

### 找不到 `@monorepo/electron-core` 模块

**原因**：共享包未构建

**解决方案**：
```bash
cd packages/electron-core && pnpm build
cd ../electron-ipc && pnpm build
cd ../electron-window && pnpm build
```

### 端口 3000 被占用

**解决方案**：
```bash
# 查看占用 3000 端口的进程
lsof -i :3000

# 杀掉占用端口的进程
kill -9 <PID>
```

## 🎨 推荐的 IDE 设置

- [VSCode](https://code.visualstudio.com/)
- [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
- [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)

## 📝 开发规范

本项目遵循以下开发规范，详见 [AGENTS.md](./AGENTS.md)：

- TypeScript/TSX 代码修改后必须进行 lint 和 typecheck 检查
- 使用 Turbo 进行统一的构建和测试管理
- 代码提交前请确保通过所有检查

## 🤝 贡献指南

欢迎贡献代码！请确保：

1. 代码通过 `pnpm lint` 和 `pnpm typecheck` 检查
2. 遵循项目的代码风格
3. 提交清晰的 commit message

## 📄 许可证

MIT License
