# 仓库规范

始终用中文回答，包括注释、文档等

## 测试规范

单元和组件测试放在 `tests/` 目录下（命名为 `*.test.ts`），E2E 浏览器流程测试放在 `tests/e2e/*.spec.ts`。打开 PR 前运行 `pnpm test:run`，UI 行为变更时添加 `pnpm test:e2e`。

## UI 开发规范

**必须使用 shadcn-vue 组件库，禁止 vibe coding 自定义样式，使用 shadcn-vue mcp 找到合适的组件**

### 强制规则
1. **所有 UI 组件必须使用 shadcn-vue** - 禁止手写原生 HTML + Tailwind 组合的基础组件（如按钮、输入框、卡片、对话框等）
2. **优先使用现有组件** - 在 `app/components/ui/` 目录下查找可用组件，创建新组件前必须确认现有组件无法满足需求
3. **组件路径规范** - shadcn-vue 组件位于 `@/components/ui/` 目录，业务组件按页面/功能模块命名（如 `@/components/home/`、`@/components/settings/`、`@/components/layout/` 等）
4. **Tailwind 仅用于布局和间距** - 只能使用 Tailwind 的 spacing、layout、typography 类，不能用于创建基础 UI 组件
5. **组件的安装** - 只能运行 `pnpm dlx shadcn-vue@latest add` 来安装组件

### 组件查找优先级
```
1. @/components/ui/        → shadcn-vue 基础组件
2. @/components/{页面名}/   → 页面专属组件（如 home, settings, layout 等）
3. @/components/           → 其他共享组件
4. 新建 shadcn-vue 组件    → 必须是可复用的基础组件
```

### 禁止事项
- ❌ 禁止 `<button class="px-4 py-2 bg-blue-500 ...">`
- ❌ 禁止 `<div class="border rounded-lg p-4 ...">` 作为卡片使用
- ❌ 禁止创建与 shadcn-vue 功能重复的基础组件


