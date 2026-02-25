---
name: frontend-designer
description: Build accessible, responsive, and performant frontend components with design system best practices, modern CSS, and framework-agnostic patterns.
---

# 前端设计师

一个全面的技能，帮助前端设计师和开发人员使用现代最佳实践构建美观、可访问且性能良好的用户界面。

## 此技能的功能

帮助前端设计师/开发人员：
- **组件设计与开发** - 构建可重用、可访问的组件
- **设计系统** - 实现令牌、模式和文档
- **响应式设计** - 移动优先、流畅布局
- **可访问性（WCAG 2.1）** - 包容性设计模式
- **现代CSS** - Flexbox、Grid、自定义属性
- **性能优化** - 快速、高效的前端
- **框架模式** - React、Vue、Svelte最佳实践
- **设计到代码** - Figma到生产工作流程

## 此技能的重要性

**没有系统化方法的后果：**
- 组件实现不一致
- 可访问性问题
- 响应式行为差
- 代码和样式重复
- 难以维护
- 性能问题

**使用此技能的好处：**
- 一致、可重用的组件
- 默认符合WCAG AA标准
- 移动优先响应式设计
- 与设计系统对齐
- 可维护的代码库
- 快速、优化的交付

## 核心原则

### 1. 可访问性优先
- WCAG 2.1 AA最低标准
- 语义化HTML
- 键盘导航
- 屏幕阅读器支持
- 焦点管理
- 颜色对比度

### 2. 移动优先响应式
- 从移动设备开始（320px）
- 渐进增强
- 流畅排版
- 灵活布局
- 触摸友好的目标

### 3. 默认性能
- 最小化CSS/JS
- 延迟加载
- 优化图像
- 关键CSS
- 树摇

### 4. 组件驱动
- 原子设计方法论
- 可重用组件
- 基于属性的定制
- 组合优于继承

### 5. 与设计系统对齐
- 设计令牌
- 一致的间距
- 排版比例
- 调色板
- 组件库

## 组件模式

### 按钮组件

**可访问、灵活的按钮模式：**

```tsx
// React示例
interface ButtonProps {
  variant?: 'primary' | 'secondary' | 'ghost';
  size?: 'sm' | 'md' | 'lg';
  disabled?: boolean;
  loading?: boolean;
  children: React.ReactNode;
  onClick?: () => void;
}

export const Button: React.FC<ButtonProps> = ({
  variant = 'primary',
  size = 'md',
  disabled = false,
  loading = false,
  children,
  onClick,
  ...props
}) => {
  return (
    <button
      className={`btn btn--${variant} btn--${size}`}
      disabled={disabled || loading}
      onClick={onClick}
      aria-busy={loading}
      {...props}
    >
      {loading ? <Spinner /> : children}
    </button>
  );
};
```

**CSS（使用设计令牌）：**

```css
.btn {
  /* 基础样式 */
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: var(--space-2);

  font-family: var(--font-sans);
  font-weight: 600;
  text-decoration: none;

  border: none;
  border-radius: var(--radius-md);
  cursor: pointer;

  transition: all 0.2s ease;

  /* 可访问性 */
  min-height: 44px; /* WCAG触摸目标 */

  &:focus-visible {
    outline: 2px solid var(--color-focus);
    outline-offset: 2px;
  }

  &:disabled {
    opacity: 0.5;
    cursor: not-allowed;
  }
}

/* 变体 */
.btn--primary {
  background: var(--color-primary);
  color: var(--color-on-primary);

  &:hover:not(:disabled) {
    background: var(--color-primary-hover);
  }
}

.btn--secondary {
  background: var(--color-secondary);
  color: var(--color-on-secondary);
}

.btn--ghost {
  background: transparent;
  color: var(--color-primary);
  border: 1px solid currentColor;
}

/* 尺寸 */
.btn--sm {
  padding: var(--space-2) var(--space-3);
  font-size: var(--text-sm);
}

.btn--md {
  padding: var(--space-3) var(--space-4);
  font-size: var(--text-base);
}

.btn--lg {
  padding: var(--space-4) var(--space-6);
  font-size: var(--text-lg);
}
```

### 卡片组件

**灵活、可访问的卡片：**

```tsx
interface CardProps {
  variant?: 'elevated' | 'outlined' | 'filled';
  padding?: 'none' | 'sm' | 'md' | 'lg';
  interactive?: boolean;
  children: React.ReactNode;
}

export const Card: React.FC<CardProps> = ({
  variant = 'elevated',
  padding = 'md',
  interactive = false,
  children,
}) => {
  const Component = interactive ? 'button' : 'div';

  return (
    <Component
      className={`
        card
        card--${variant}
        card--padding-${padding}
        ${interactive ? 'card--interactive' : ''}
      `}
      {...(interactive && { role: 'button', tabIndex: 0 })}
    >
      {children}
    </Component>
  );
};
```

**CSS：**

```css
.card {
  border-radius: var(--radius-lg);
  background: var(--color-surface);
}

.card--elevated {
  box-shadow: var(--shadow-md);
}

.card--outlined {
  border: 1px solid var(--color-border);
}

.card--filled {
  background: var(--color-surface-variant);
}

.card--interactive {
  cursor: pointer;
  transition: transform 0.2s, box-shadow 0.2s;

  &:hover {
    transform: translateY(-2px);
    box-shadow: var(--shadow-lg);
  }

  &:focus-visible {
    outline: 2px solid var(--color-focus);
    outline-offset: 2px;
  }
}

.card--padding-sm { padding: var(--space-3); }
.card--padding-md { padding: var(--space-4); }
.card--padding-lg { padding: var(--space-6); }
```

### 表单输入组件

**可访问的表单输入：**

```tsx
interface InputProps {
  label: string;
  error?: string;
  hint?: string;
  required?: boolean;
  type?: 'text' | 'email' | 'password' | 'number';
}

export const Input: React.FC<InputProps> = ({
  label,
  error,
  hint,
  required = false,
  type = 'text',
  ...props
}) => {
  const id = useId();
  const hintId = `${id}-hint`;
  const errorId = `${id}-error`;

  return (
    <div className="input-wrapper">
      <label htmlFor={id} className="input-label">
        {label}
        {required && <span aria-label="required">*</span>}
      </label>

      {hint && (
        <p id={hintId} className="input-hint">
          {hint}
        </p>
      )}

      <input
        id={id}
        type={type}
        className={`input ${error ? 'input--error' : ''}`}
        aria-required={required}
        aria-invalid={!!error}
        aria-describedby={error ? errorId : hint ? hintId : undefined}
        {...props}
      />

      {error && (
        <p id={errorId} className="input-error" role="alert">
          {error}
        </p>
      )}
    </div>
  );
};
```

## 设计令牌

**设计系统的CSS自定义属性：**

```css
:root {
  /* 颜色 - 主色 */
  --color-primary: #0066FF;
  --color-primary-hover: #0052CC;
  --color-on-primary: #FFFFFF;

  /* 颜色 - 表面 */
  --color-surface: #FFFFFF;
  --color-surface-variant: #F5F5F5;
  --color-on-surface: #1A1A1A;

  /* 颜色 - 边框 */
  --color-border: #E0E0E0;
  --color-border-hover: #BDBDBD;

  /* 颜色 - 语义 */
  --color-error: #D32F2F;
  --color-success: #388E3C;
  --color-warning: #F57C00;
  --color-info: #1976D2;

  /* 间距比例（8px基础） */
  --space-1: 0.25rem;  /* 4px */
  --space-2: 0.5rem;   /* 8px */
  --space-3: 0.75rem;  /* 12px */
  --space-4: 1rem;     /* 16px */
  --space-5: 1.5rem;   /* 24px */
  --space-6: 2rem;     /* 32px */
  --space-8: 3rem;     /* 48px */
  --space-10: 4rem;    /* 64px */

  /* 排版比例 */
  --text-xs: 0.75rem;    /* 12px */
  --text-sm: 0.875rem;   /* 14px */
  --text-base: 1rem;     /* 16px */
  --text-lg: 1.125rem;   /* 18px */
  --text-xl: 1.25rem;    /* 20px */
  --text-2xl: 1.5rem;    /* 24px */
  --text-3xl: 1.875rem;  /* 30px */
  --text-4xl: 2.25rem;   /* 36px */

  /* 字体系列 */
  --font-sans: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
  --font-mono: "SF Mono", Monaco, "Cascadia Code", monospace;

  /* 行高 */
  --leading-tight: 1.25;
  --leading-normal: 1.5;
  --leading-relaxed: 1.75;

  /* 边框半径 */
  --radius-sm: 0.25rem;  /* 4px */
  --radius-md: 0.5rem;   /* 8px */
  --radius-lg: 1rem;     /* 16px */
  --radius-full: 9999px;

  /* 阴影 */
  --shadow-sm: 0 1px 2px rgba(0, 0, 0, 0.05);
  --shadow-md: 0 4px 6px rgba(0, 0, 0, 0.1);
  --shadow-lg: 0 10px 15px rgba(0, 0, 0, 0.1);
  --shadow-xl: 0 20px 25px rgba(0, 0, 0, 0.15);

  /* 焦点环 */
  --color-focus: #0066FF;

  /* 过渡 */
  --transition-fast: 150ms ease;
  --transition-base: 200ms ease;
  --transition-slow: 300ms ease;
}

/* 深色模式 */
@media (prefers-color-scheme: dark) {
  :root {
    --color-surface: #1A1A1A;
    --color-surface-variant: #2A2A2A;
    --color-on-surface: #FFFFFF;
    --color-border: #3A3A3A;
  }
}
```

## 响应式设计模式

### 移动优先断点

```css
/* 移动优先方法 */
.container {
  padding: var(--space-4);

  /* 平板：768px及以上 */
  @media (min-width: 48rem) {
    padding: var(--space-6);
  }

  /* 桌面：1024px及以上 */
  @media (min-width: 64rem) {
    padding: var(--space-8);
    max-width: 1200px;
    margin: 0 auto;
  }
}
```

### 流畅排版

```css
/* 响应式排版 */
h1 {
  font-size: clamp(2rem, 5vw, 3.5rem);
  line-height: var(--leading-tight);
}

h2 {
  font-size: clamp(1.5rem, 4vw, 2.5rem);
}

p {
  font-size: clamp(1rem, 2vw, 1.125rem);
  line-height: var(--leading-normal);
}
```

### 网格布局

```css
/* 响应式网格 */
.grid {
  display: grid;
  gap: var(--space-4);

  /* 自动适应列（最小280px） */
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
}

/* 12列网格系统 */
.grid-12 {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  gap: var(--space-4);
}

.col-span-4 {
  grid-column: span 4;
}

/* 在移动设备上堆叠 */
@media (max-width: 48rem) {
  .col-span-4 {
    grid-column: span 12;
  }
}
```

## 可访问性模式

### 跳过链接

```tsx
export const SkipLink = () => (
  <a href="#main-content" className="skip-link">
    Skip to main content
  </a>
);
```

```css
.skip-link {
  position: absolute;
  top: -40px;
  left: 0;
  background: var(--color-primary);
  color: var(--color-on-primary);
  padding: var(--space-2) var(--space-4);
  text-decoration: none;
  z-index: 100;

  &:focus {
    top: 0;
  }
}
```

### 焦点管理

```tsx
// 带焦点陷阱的模态框
export const Modal = ({ isOpen, onClose, children }) => {
  const modalRef = useRef(null);

  useEffect(() => {
    if (isOpen) {
      // 保存当前聚焦元素
      const previouslyFocused = document.activeElement;

      // 聚焦模态框中的第一个可聚焦元素
      const firstFocusable = modalRef.current?.querySelector(
        'button, [href], input, select, textarea, [tabindex]:not([tabindex="-1"])'
      );
      firstFocusable?.focus();

      // 关闭时恢复焦点
      return () => previouslyFocused?.focus();
    }
  }, [isOpen]);

  if (!isOpen) return null;

  return (
    <div
      ref={modalRef}
      role="dialog"
      aria-modal="true"
      className="modal-overlay"
    >
      <div className="modal">
        {children}
      </div>
    </div>
  );
};
```

### ARIA标签

```tsx
// 带可访问标签的图标按钮
export const IconButton = ({ icon, label, ...props }) => (
  <button
    aria-label={label}
    className="icon-button"
    {...props}
  >
    <span aria-hidden="true">{icon}</span>
  </button>
);

// 加载状态
export const LoadingButton = ({ loading, children, ...props }) => (
  <button
    aria-busy={loading}
    aria-live="polite"
    disabled={loading}
    {...props}
  >
    {loading ? 'Loading...' : children}
  </button>
);
```

## 性能优化

### 关键CSS

```html
<!-- 内联关键CSS -->
<style>
  /* 首屏样式 */
  body { margin: 0; font-family: var(--font-sans); }
  .header { /* 关键头部样式 */ }
  .hero { /* 关键英雄区域样式 */ }
</style>

<!-- 异步加载完整样式表 -->
<link rel="stylesheet" href="styles.css" media="print" onload="this.media='all'">
```

### 延迟加载图像

```tsx
export const LazyImage = ({ src, alt, ...props }) => (
  <img
    src={src}
    alt={alt}
    loading="lazy"
    decoding="async"
    {...props}
  />
);
```

### 代码分割

```tsx
// React延迟加载
const Dashboard = lazy(() => import('./Dashboard'));

function App() {
  return (
    <Suspense fallback={<Loading />}>
      <Dashboard />
    </Suspense>
  );
}
```

## 现代CSS技术

### 容器查询

```css
.card {
  container-type: inline-size;
}

.card-content {
  display: flex;
  flex-direction: column;

  /* 容器>400px时切换为行布局 */
  @container (min-width: 400px) {
    flex-direction: row;
  }
}
```

### CSS Grid Auto-Fit

```css
.gallery {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: var(--space-4);
}
```

### 主题自定义属性

```css
/* 浅色主题（默认） */
:root {
  --bg: #ffffff;
  --text: #000000;
}

/* 深色主题 */
[data-theme="dark"] {
  --bg: #000000;
  --text: #ffffff;
}

body {
  background: var(--bg);
  color: var(--text);
}
```

## 组件库结构

```
src/
├── components/
│   ├── Button/
│   │   ├── Button.tsx
│   │   ├── Button.css
│   │   ├── Button.test.tsx
│   │   └── Button.stories.tsx
│   ├── Card/
│   ├── Input/
│   └── index.ts
├── tokens/
│   ├── colors.css
│   ├── spacing.css
│   ├── typography.css
│   └── index.css
├── utils/
│   ├── a11y.ts
│   └── responsive.ts
└── index.ts
```

## 使用此技能

### 生成组件

```bash
./scripts/generate_component.sh Button
```

创建包含以下内容的组件：
- TypeScript/JSX文件
- CSS模块
- 测试文件
- Storybook故事
- 可访问性检查

### 设计系统设置

```bash
./scripts/setup_design_system.sh
```

创建：
- 设计令牌（CSS自定义属性）
- 基础样式
- 组件模板
- 文档结构

### 可访问性审计

```bash
./scripts/audit_accessibility.sh
```

检查：
- 颜色对比度
- 键盘导航
- ARIA属性
- 语义化HTML
- 焦点管理

## 最佳实践

### 组件设计

✅ **推荐：**
- 使用语义化HTML
- 使组件可键盘访问
- 提供ARIA标签
- 支持浅色和深色模式
- 触摸目标最小44x44px
- 使用适当的标题层次结构
- 处理加载和错误状态

❌ **不推荐：**
- 使用div作为按钮
- 忘记焦点样式
- 硬编码颜色
- 忽略移动视口
- 跳过图像的alt文本
- 创建不可访问的模态框

### CSS最佳实践

✅ **推荐：**
- 使用设计令牌
- 移动优先响应式
- BEM或CSS模块命名
- 逻辑属性（inline-start vs left）
- 现代布局（flexbox, grid）

❌ **不推荐：**
- 使用!important
- 深层嵌套（> 3级）
- 到处使用固定像素值
- 浏览器特定的黑客技术
- 内联样式

### 性能

✅ **推荐：**
- 延迟加载图像
- 代码分割路由
- 最小化CSS
- 使用系统字体
- 优化图像（WebP）
- 内联关键CSS

❌ **不推荐：**
- 加载未使用的CSS
- 大型JavaScript包
- 未优化的图像
- 阻塞资源
- 太多网页字体

## 框架特定模式

### React

```tsx
// 组合模式
export const Card = ({ children }) => (
  <div className="card">{children}</div>
);

export const CardHeader = ({ children }) => (
  <div className="card-header">{children}</div>
);

// 使用
<Card>
  <CardHeader>Title</CardHeader>
  <CardBody>Content</CardBody>
</Card>
```

### Vue

```vue
<!-- 可组合组件 -->
<template>
  <div :class="cardClasses">
    <slot />
  </div>
</template>

<script setup>
const props = defineProps({
  variant: String,
  padding: String
});

const cardClasses = computed(() => [
  'card',
  `card--${props.variant}`,
  `card--padding-${props.padding}`
]);
</script>
```

## 资源

包含的所有参考材料：
- 设计令牌系统
- 可访问性检查清单（WCAG 2.1）
- 响应式设计模式
- 组件库模板
- 性能优化指南

## 总结

此技能提供：
- **可访问组件** - 默认WCAG AA标准
- **响应式设计** - 移动优先方法
- **设计系统** - 基于令牌的一致性
- **现代CSS** - Flexbox、Grid、自定义属性
- **性能** - 优化交付
- **最佳实践** - 生产就绪模式

**使用此技能构建美观、可访问、性能良好的前端。**

---

**"好的设计是可访问的设计。"**