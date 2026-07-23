## 项目概述
Cambridge PET Flashcards — 基于 2025 年剑桥 B1 Preliminary 官方词汇表的 PET 专属 A–Z 图片闪卡课程，面向青少年学习者。包含 1,461 个 PET 专属词条，零 KET 重叠，配有英式发音音频、故事书风格插图和中文释义。

## 技术栈
- **框架**: React 19 + Vite 7
- **语言**: JavaScript (JSX)
- **样式**: 原生 CSS (styles.css)
- **包管理**: pnpm
- **运行时**: Node.js 24
- **字体**: Plus Jakarta Sans (Variable)
- **PWA**: Service Worker + Web App Manifest
- **数据**: JSON 静态数据文件

## 目录结构
```
/workspace/projects/
├── .coze                    # 项目配置（平台读取）
├── AGENTS.md                # 本文件
├── index.html               # HTML 入口
├── package.json             # 依赖与脚本
├── pnpm-lock.yaml           # 锁文件
├── vite.config.js           # Vite 配置
├── src/
│   ├── main.jsx             # React 入口
│   ├── App.jsx              # 主应用组件（核心逻辑）
│   ├── styles.css           # 全局样式
│   └── data/                # 课程数据（JSON）
│       ├── pet-course.json
│       ├── pet-2025-official.json
│       └── ...
├── public/
│   ├── audio/               # 单词发音音频
│   ├── images/              # 故事书风格插图
│   ├── icon.svg             # 应用图标
│   ├── manifest.webmanifest # PWA 清单
│   └── sw.js                # Service Worker
└── scripts/                 # 构建与部署脚本
    ├── coze-preview-build.sh  # 预览构建脚本
    ├── coze-preview-run.sh    # 预览运行脚本（Vite preview）
    ├── build.sh               # 部署构建脚本
    └── run.sh                 # 部署运行脚本（serve）
```

## 关键入口 / 核心模块
- **入口**: `src/main.jsx` → `src/App.jsx`
- **核心组件**: `App.jsx`（约 25KB，包含全部 UI 逻辑和状态管理）
- **样式**: `src/styles.css`（约 27KB，包含全部样式）
- **数据**: `src/data/pet-course.json`（课程主数据）
- **构建**: `vite build` → 输出到 `dist/`

## 运行与预览
- **开发**: `pnpm run dev`（先 build 再 preview）
- **构建**: `pnpm run build`
- **测试**: `pnpm test`（数据验证 + UI 验证）
- **数据构建**: `pnpm run data:build`（Python 脚本）

## 预览与部署配置
- **项目类型**: Web（纯前端 Vite 应用）
- **预览链路**: `scripts/coze-preview-build.sh`（构建） + `scripts/coze-preview-run.sh`（Vite preview 5000 端口）
- **部署链路**: `scripts/build.sh`（安装依赖 + Vite 构建） + `scripts/run.sh`（serve 静态文件 5000 端口）
- **部署模式**: `deploy.profile.kind = "service"`, `deploy.profile.flavor = "web"`
- **技术项目根目录**: 与工作区根目录重合（`path = "."`）

## 用户偏好与长期约束
- Node.js 项目统一使用 pnpm 管理依赖
- 预览端口固定为 5000
- 项目为纯前端静态应用，无后端服务

## 常见问题和预防
- `App.jsx` 和 `styles.css` 文件较大（25KB+），编辑时注意分页读取
- 数据文件为 JSON 格式，修改前需先读取确认结构
- 项目使用 Vite preview 模式运行（先 build 再 serve 静态文件）
