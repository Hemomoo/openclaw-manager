# OpenClaw Manager

OpenClaw-Easy：包含 Electron 桌面端与 Web 前端的多包仓库，用于一站式构建与发布

## 📋 项目简介

OpenClaw Manager 是一个基于 Monorepo 架构的现代化应用项目，提供 Electron 桌面应用和 Web 前端两种形态。项目使用 pnpm + Turbo 进行高效的包管理和构建优化。

## 🛠 技术栈

- **包管理器**: pnpm 10.26.1
- **构建工具**: Turbo
- **桌面应用**: Electron + React + TypeScript
- **Web 应用**: Next.js + React + TypeScript
- **样式**: TailwindCSS
- **代码规范**: ESLint + Prettier

## 📁 项目结构

```
openclaw-manager/
├── apps/
│   ├── electron-app/          # Electron 桌面应用
│   └── open-claw/             # Web 前端应用
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

### 启动开发环境

```bash
# 启动所有应用
pnpm dev

# 仅启动 Electron 应用
pnpm electron:dev

# 仅启动 Web 应用
pnpm react:dev
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
pnpm react:build
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
