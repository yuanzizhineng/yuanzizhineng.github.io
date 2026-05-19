# 元字智能科技官网 v2 — 风格指南 & 复刻提示词

> 本文档用于完整记录当前官网（深色科技风 v2）的设计系统、组件规范，以及可用于复刻同类官网的 AI 提示词模板。

---

## 一、设计系统（Design Tokens）

### 1.1 色彩体系

| 角色 | 色值 | CSS 变量 | 用途 |
|------|-------|-----------|------|
| 深底主色 | `#0a0e27` | `--dark` | Hero背景、Footer背景、主section底 |
| 深底次色 | `#0f1333` | `--dark-2` | 交替section背景、导航移动端菜单 |
| 深底卡片 | `#141837` | `--dark-3` | 卡片底色、浮动按钮底 |
| 深底辅助 | `#1a1f45` | `--dark-4` | 备用深色 |
| 品牌蓝 | `#0066ff` | `--blue` | 渐变起点、about-card、contact-strip |
| 电光蓝 | `#00d4ff` | `--neon` | 标题强调、发光边框、链接、section-tag |
| 电光蓝淡底 | `rgba(0,212,255,0.15)` | `--neon-soft` | 图标底、标签底、hover背景 |
| 强调橙 | `#ff6a00` | `--orange` | 主按钮、热销角标、联系电话 |
| 橙色淡底 | `rgba(255,106,0,0.15)` | `--orange-soft` | featured产品卡标签底 |
| 深字（白） | `#ffffff` | `--text-dark` | 深底上的标题、重要数字 |
| 正文字 | `#a0a8c8` | `--text-body` | 段落正文 |
| 辅助字 | `#6b7294` | `--text-light` | 说明文字、占位数据 |
| 边框 | `rgba(255,255,255,0.08)` | `--border` | 卡片边框、分割线 |
| 边框hover | `rgba(0,212,255,0.4)` | `--border-hover` | 悬停时边框色 |

**渐变用法：**
- 蓝色渐变：`linear-gradient(135deg, #0066ff, #003399)` — 用于 about-card、contact-strip
- 电光蓝渐变：`linear-gradient(135deg, #00d4ff, #0066ff)` — 用于 Hero H1 em 标签文字
- 橙色渐变：`linear-gradient(to top, #ff6a00, #ff9a4d)` — 用于 dashboard 高亮柱状图
- 顶部光条：`linear-gradient(90deg, transparent, #00d4ff, transparent)` — 卡片hover时顶部装饰线
- 底部装饰线：`linear-gradient(90deg, #00d4ff, #0066ff)` — 应用场景卡片底部装饰

**发光效果：**
```css
--glow-blue: 0 0 20px rgba(0, 212, 255, 0.25);   /* 蓝色光晕，卡片hover */
--glow-orange: 0 0 20px rgba(255, 106, 0, 0.25);  /* 橙色光晕，featured卡片 */
```

---

### 1.2 字体系统

```css
font-family: -apple-system, BlinkMacSystemFont, "PingFang SC",
             "Microsoft YaHei", "Helvetica Neue", sans-serif;
```

| 用途 | 大小 | 粗细 | 行高 |
|------|------|------|------|
| 页面标题 H1 | `clamp(32px, 6vw, 60px)` | 800 | 1.15 |
| Section 标题 H2 | `clamp(26px, 4vw, 40px)` | 800 | 1.25 |
| Dashboard H2 | `clamp(24px, 3.5vw, 34px)` | 800 | 1.3 |
| 卡片标题 H3 | 17-20px | 700 | — |
| 正文 | 14-15px | 400 | 1.7 |
| 小字/标签 | 11-13px | 600-700 | — |
| 统计数字 | 32px | 800 | 1 |

**clamp() 响应式策略：**
- Hero H1：`clamp(32px, 6vw, 60px)`
- Section H2：`clamp(26px, 4vw, 40px)`
- Dashboard H2：`clamp(24px, 3.5vw, 34px)`

---

### 1.3 间距 & 布局

| 变量 | 值 |
|------|-----|
| 页面最大宽度 | `1200px`（居中 `margin: 0 auto`） |
| 通用横向 padding | `24px` |
| Section 纵向 padding | `100px 24px` |
| 卡片圆角 | 14-18px（按层级递增） |
| 卡片 gap | `24-28px` |
| 按钮圆角 | `6-8px` |
| 导航栏高度 | `68px` |
| 图标容器 | `40-56px` 方形，圆角 `10-14px` |

---

### 1.4 阴影系统

```css
--shadow: 0 4px 30px rgba(0, 0, 0, 0.3);          /* 通用深色投影 */
--glow-blue: 0 0 20px rgba(0, 212, 255, 0.25);     /* 蓝色光晕，卡片hover */
--glow-orange: 0 0 20px rgba(255, 106, 0, 0.25);   /* 橙色光晕，featured卡 */
/* 导航栏滚动投影 */
box-shadow: 0 4px 30px rgba(0, 0, 0, 0.5);
/* 主按钮投影 */
box-shadow: 0 0 20px rgba(255,106,0,0.3);
/* 主按钮hover投影 */
box-shadow: 0 0 35px rgba(255,106,0,0.5);
/* Dashboard截图投影 */
box-shadow: 0 8px 50px rgba(0,0,0,0.5);
```

---

### 1.5 响应式断点

```css
/* 平板：≤1024px */
@media (max-width: 1024px) {
  .adv-grid        → 2列
  .stats-inner     → 3列（每排两个有右边框，第三个无）
  .dash-wrapper    → 1列（截图区换到下方）
  .cust-grid       → 1列
  .about-grid      → 1列
  .scene-grid      → 2列
  .serv-grid       → 2列
}

/* 手机：≤768px */
@media (max-width: 768px) {
  .nav-links       → display:none（切换汉堡菜单）
  .hero            → min-height 90vh
  .hero-btns       → 纵向堆叠，按钮 100% 宽（max-width 320px）
  .stats-inner     → 2列
  .prod-grid       → 1列
  .serv-grid       → 1列
  .footer-top      → 2列
  .adv-grid        → 1列
  .dash-row        → 2列
  .cust-logos      → 2列
  .contact-strip   → 纵向居中
  .about-highlights → 1列
  .scene-grid      → 1列
}

/* 超小屏：≤480px */
@media (max-width: 480px) {
  .footer-top      → 1列
}
```

---

## 二、页面结构（13 大模块）

```
┌─ Navigation（固定导航，深色半透明毛玻璃，滚动后加深阴影）
├─ Hero Section（全屏，深色 + Canvas粒子连线动画）
├─ Stats Bar（6 个统计数字，深色底，数字滚动动画）
├─ 核心优势（4 列卡片，深色底 + 发光边框）
├─ 产品中心（3 列产品卡，中间高亮发光）
├─ 管理后台预览（左文右深色仪表盘截图）
├─ 应用场景（4 列场景卡片，底部渐变装饰线）
├─ 客户案例（左文右 Logo 网格）
├─ 服务保障（4 列 + 联系信息条）
├─ 关于我们（左蓝渐变卡右文）
├─ CTA Section（深色底 + 发光脉冲按钮）
├─ Footer（深蓝黑底，4 列）
└─ 浮动按钮（回到顶部 + 打电话）
```

---

## 三、组件规范

### 3.1 按钮系统

**主按钮（.btn-primary）**
```css
背景: var(--orange)  #ff6a00
字色: white
内边距: 15px 32px
圆角: 8px
投影: 0 0 20px rgba(255,106,0,0.3)
悬停: background → #e55a00, 上移 translateY(-2px), 投影加亮 0 0 35px
```

**次按钮（.btn-secondary）**
```css
背景: transparent
边框: 2px solid var(--neon)  #00d4ff
字色: var(--neon)
悬停: background → var(--neon-soft), box-shadow 蓝色光晕, 上移 translateY(-2px)
```

**产品卡按钮（.prod-btn）**
- 普通卡：电光蓝边框 + 电光蓝字，悬停填充半透明蓝 + 光晕
- 高亮卡（.featured）：橙色底 + 白色字 + 橙色光晕，悬停加亮

**CTA发光按钮（.cta-btn-glow）**
- 继承 .btn-primary 样式
- 附加动画 `pulse-glow-orange`：阴影在 `0 0 15px` ↔ `0 0 35px` 间脉冲

---

### 3.2 卡片悬停动效

所有卡片统一悬停效果：
```css
transition: all 0.4s;
悬停 → border-color: var(--border-hover) + box-shadow: var(--glow-blue) + translateY(-5px)
```

**优势卡片（.adv-card）额外效果：**
- 顶部出现光条：`::before` 元素，`linear-gradient(90deg, transparent, var(--neon), transparent)`，hover时 `opacity: 1`

**应用场景卡片（.scene-card）额外效果：**
- 底部出现渐变线：`::after` 元素，`linear-gradient(90deg, var(--neon), var(--blue))`，hover时 `opacity: 1`

---

### 3.3 Section Tag（小标签）

每个 section 标题上方有一个统一风格的小标签：
```html
<div class="section-tag">核心优势</div>
<h2 class="section-title">为什么选择元字智能？</h2>
<p class="section-desc">不拼低价，拼稳定和服务。</p>
```

```css
.section-tag {
  display: inline-flex; align-items: center; gap: 8px;
  font-size: 12px; font-weight: 700;
  letter-spacing: 2px; text-transform: uppercase;
  color: var(--neon);
}
.section-tag::before {
  content: '';
  width: 20px; height: 2px;
  background: var(--neon); border-radius: 2px;
}
```

---

### 3.4 统计条（Stats Bar）

- 深色底 `var(--dark-2)`，6列等宽
- 数字 `32px, 800, 电光蓝`，带**滚动计数动画**（IntersectionObserver 触发，从0跑到目标值）
- 标签 `13px, 辅助字`
- 每项有右边框 `var(--border)`，最后一项无
- 响应式：1024px 以下 3 列，768px 以下 2 列

**计数动画实现：**
```js
// 使用 IntersectionObserver 检测可见性
// 使用 requestAnimationFrame + easeOutCubic 缓动
// data-target 存储目标值，data-no-plus="true" 控制是否显示+号
```

---

### 3.5 产品卡片

```
┌─────────────────────┐
│ 热销推荐（橙色渐变条，仅 .featured 显示） │
├─────────────────────┤
│ [标准型] 电光蓝/橙色小标签          │
│ 插拔式物联网卡                   │
│ 适用：智能电表·共享设备·...       │
│ ✓ 特征1                        │
│ ✓ 特征2                        │
│ ✓ 特征3                        │
│ ✓ 特征4                        │
├─────────────────────┤
│ 了解详情 →（底部按钮区）          │
└─────────────────────┘
```

- 卡片整体 `border-radius: 16px; overflow: hidden`
- 底部按钮区 `background: rgba(255,255,255,0.02); border-top: 1px solid var(--border)`
- 特征列表前缀用 CSS `::before { content: '✓'; color: #00cc66; }`
- featured 卡片：橙色边框 + 橙色光晕，标签改用 `var(--orange-soft)` 底 + 橙字
- 悬停：蓝色光晕 + 上移5px

---

### 3.6 管理后台模拟截图（深色仪表盘风格）

```
┌──────────────────────────┐
│ ● ● ●  www.yuanzizhineng.com/console │  ← 顶部栏（红黄绿 + 假URL）
├──────────────────────────┤
│ [在网设备] [本月流量] [告警] [在线率] │  ← 4 个统计小卡
├──────────────────────────┤
│ 近7日流量消耗趋势                      │
│ ▇▇▇▇▇▇▇                            │  ← 柱状图（蓝→电光蓝渐变，highlight用橙色渐变）
├──────────────────────────┤
│ 设备名称  │ 流量用量 │ 状态           │  ← 3 列表格
│ 示例设备-01│ — GB/月 │ ● 在线        │
│ 示例设备-02│ — GB/月 │ ● 在线        │
│ 示例设备-03│ — GB/月 │ ⚠ 流量告警    │
└──────────────────────────┘
```

**关键细节：**
- 整体深色底 `#0c1029`，内部卡片 `rgba(255,255,255,0.03)`，圆角 `16px`
- 数据用 `—`（em dash）占位，不用假数字
- 状态用 `.dash-status.online`（半透明绿底+绿字 `rgba(0,204,102,0.15) / #00cc66`）
- 状态用 `.dash-status.warning`（半透明橙底+橙字）
- 顶部栏底 `#0e1230`
- 柱状图：蓝色渐变 `linear-gradient(to top, #0066ff, #00d4ff)`，highlight 橙色渐变
- 截图外层投影 `0 8px 50px rgba(0,0,0,0.5)`

---

### 3.7 应用场景卡片

```
┌─────────────────────┐
│ [🏠] 56px 图标容器         │
│ 智能家居                │
│ › 智能门锁远程控制        │
│ › 环境传感器数据上传      │
│ › 家电远程联动管理        │
│ › 安防摄像头实时监控      │
└─────────────────────┘
```

- 4列网格，深色底 `var(--dark-3)`
- 列表项用 `›` 前缀（CSS `::before`，电光蓝色）
- 底部3px渐变装饰线（hover时显示）
- 悬停：蓝色光晕 + 上移5px

---

### 3.8 服务保障卡片

- 4列网格（v1为3列，v2增加"定制化方案"）
- 深色底 `var(--dark-3)`，图标36px
- 悬停：蓝色光晕 + 上移4px

---

### 3.9 Footer

- 背景 `var(--dark)`，顶边框 `var(--border)`
- 4 列：`1.5fr | 1fr | 1fr | 1fr`
- 品牌列：Logo + 一句话简介
- 链接列：hover 变电光蓝 `var(--neon)`
- 底栏：版权 + ICP 备案号，上边框 `var(--border)`

---

### 3.10 浮动按钮

```css
位置: fixed, 右下角 20px/24px
回到顶部: var(--dark-3)底，默认 display:none，滚动超过 60px 后显示
打电话: 橙色圆 + 橙色光晕，内容是电话图标 📞，href="tel:..."
尺寸: 50px × 50px
```

---

## 四、JavaScript 交互

### 4.1 粒子连线动画（Hero背景）
```js
// Canvas 实现，80个粒子
// 粒子半径随机1-3px，颜色 rgba(0, 212, 255, 0.5)
// 粒子间距离 < 150px 时绘制连线，颜色随距离渐隐
// 全屏自适应 resize
```

### 4.2 导航滚动效果
```js
window.addEventListener('scroll', () => {
  // 滚动 > 60px → nav 加 'scrolled' 类（加深背景 + 底部阴影）
  // 同时显示「回到顶部」按钮
});
```

### 4.3 移动端导航
```js
function toggleMobileNav() {
  document.getElementById('mobileNav').classList.toggle('active');
}
// 点击遮罩层（非菜单区）也可关闭
```

### 4.4 导航高亮
滚动时自动给当前 section 对应的导航链接加 `.active` 类（电光蓝底部边框）。

### 4.5 滚动渐显动画（fade-up）
```js
// IntersectionObserver，threshold: 0.15
// 元素进入视口时添加 .visible 类（opacity: 0 → 1, translateY: 40px → 0）
// 多个同级元素依次延迟 80ms 出现
```

### 4.6 数字滚动计数动画
```js
// IntersectionObserver 检测统计条可见性
// requestAnimationFrame + easeOutCubic 缓动
// 从 0 滚动到 data-target 值，时长 2000ms
// data-no-plus="true" 控制不显示+号（如年份 2025）
```

---

## 五、动画关键帧

```css
/* 蓝色光晕脉冲 */
@keyframes pulse-glow-blue {
  0%, 100% { box-shadow: 0 0 20px rgba(0, 212, 255, 0.25); }
  50% { box-shadow: 0 0 40px rgba(0, 212, 255, 0.5); }
}

/* 橙色光晕脉冲（CTA按钮） */
@keyframes pulse-glow-orange {
  0%, 100% { box-shadow: 0 0 15px rgba(255, 106, 0, 0.3); }
  50% { box-shadow: 0 0 35px rgba(255, 106, 0, 0.6); }
}

/* 绿点脉冲（Hero徽章） */
@keyframes pulse-dot {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.3; }
}

/* 向下箭头弹跳（Hero底部） */
@keyframes bounce-arrow {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(10px); }
}

/* 浮动 */
@keyframes float {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-6px); }
}
```

---

## 六、复刻提示词模板

> 将以下内容中的 `{{变量}}` 替换为实际信息，即可复刻同款官网。

```
你是一个有10年独立建设网站的资深工程师。

请帮我制作一个单HTML文件的企业官网，要求：

=============
一、品牌信息
=============
- 公司全称：{{公司全称}}
- 英文品牌名：{{英文名}}
- Slogan：{{Slogan}}
- 成立时间：{{成立时间}}
- 注册地址：{{详细地址，无多余空格}}
- 联系人：{{联系人}}
- 电话：{{电话格式：XXX-XXXX-XXXX}}
- 微信/QQ：{{号码}}
- 邮箱：{{邮箱}}
- 官网域名：{{域名}}
- 注册资本：{{数字}}万元
- 员工规模：集团 {{}} 人，技术 {{}} 人
- 服务企业：{{}}+
- 年营收：突破 {{}} 万元
- ICP备案号：{{豫ICP备XXXX号-X}}

=============
二、设计风格要求
=============
整体风格：高端科技风、深色系、视觉冲击。
色彩体系：
  - 深底主色：#0a0e27（Hero/Footer/主section底）
  - 深底次色：#0f1333（交替section底）
  - 深底卡片：#141837（卡片底色）
  - 品牌蓝：#0066ff（渐变起点、about-card）
  - 电光蓝：#00d4ff（标题强调、发光边框、链接、section-tag）
  - 强调橙：#ff6a00（主按钮、热销标签、联系电话）
  - 白字标题：#ffffff，正文：#a0a8c8，辅助字：#6b7294
  - 边框：rgba(255,255,255,0.08)，hover边框：rgba(0,212,255,0.4)
字体：PingFang SC / Microsoft YaHei，无衬线。
发光效果：蓝色光晕 box-shadow: 0 0 20px rgba(0,212,255,0.25)
所有数字用真实数据，不用假数据占位（营收、员工数等）。
管理后台截图区的数据用 "—" 占位，不要用假数字。

=============
三、页面模块（按顺序）
=============

【1】固定导航栏（fixed）
- 背景：深色半透明 rgba(10,14,39,0.85) + backdrop-filter: blur(20px)
- 左侧：Logo图片（从本地 logo-2.png 读取，高度48px，宽度自适应，深色背景适配用 filter: invert(1) hue-rotate(180deg) brightness(1.2) saturate(1.4)）
- 中间：7个锚点链接（核心优势 / 产品中心 / 管理后台 / 应用场景 / 客户案例 / 服务保障 / 关于我们）
- 右侧：橙色CTA按钮「免费申请样卡」，带橙色光晕
- 滚动超过60px后导航栏加深背景+阴影
- 导航链接hover/active颜色变为电光蓝

【2】Hero 区（全屏 100vh）
- 背景：深色 #0a0e27 + Canvas粒子连线动画（80个粒子，蓝色，距离<150px连线）
- 粒子动画上方覆盖径向渐变遮罩
- 居中布局：绿色脉冲圆点徽章 + 大标题（em用蓝色渐变字体）+ 副标题 + 双按钮 + 信任条
- 底部：向下滚动箭头弹跳动画
- 主按钮橙色发光，次按钮电光蓝边框+hover发光

【3】统计条（通栏，6列，深色底）
- 数字使用滚动计数动画（IntersectionObserver触发，从0跑到目标值，easeOutCubic，2秒）
- 20+ 集团员工
- 50+ 服务企业客户
- 3  运营商直连通道
- 1006 注册资本（万元）
- 100万+ 营收突破（万元）
- 2025 年2月成立（无+号）

【4】核心优势（深色底 #0a0e27）
- 小标签（电光蓝）+ 标题 + 描述
- 4列卡片网格：
  ① 三大运营商直连（📡）+ 描述
  ② 深度技术支持（⚙️）+ 描述
  ③ 灵活计费模式（💰）+ 描述
  ④ 7×24h快速响应（🛎️）+ 描述
- 卡片样式：深色底 #141837、半透明边框、圆角14px、图标56px电光蓝淡底圆角方底
- 悬停：边框变电光蓝 + 蓝色光晕 + 上移5px + 顶部出现电光蓝光条

【5】产品中心（深色底 #0f1333）
- 小标签 + 标题 + 描述
- 3列产品卡：
  ① 插拔式物联网卡（.featured 高亮，橙色边框+光晕，顶部橙色渐变「热销推荐」条）
  ② 贴片式物联网卡
  ③ 工业级物联网卡
- 每张卡包含：电光蓝/橙色小标签、产品名、适用场景（电光蓝加粗）、4个✓特征、底部按钮
- 特征列表用 CSS ::before 插入绿色 ✓
- 卡片整体圆角16px，overflow:hidden，底部按钮区背景 rgba(255,255,255,0.02)
- 悬停：蓝色光晕 + 上移5px

【6】管理后台预览（深色底 #0a0e27，左右两栏）
- 左栏：小标签 + 标题 + 描述 + 4个功能点（带电光蓝图标）+ CTA按钮
- 右栏：深色仪表盘风格模拟截图
  - 整体底 #0c1029，圆角16px
  - 顶部栏：红黄绿三点 + 假URL地址栏
  - 4个统计小卡（在网设备/本月流量/告警设备/在线率），数据用"—"占位
  - 柱状图区：近7日流量趋势（7个CSS div，蓝色渐变，最后一个.highlight用橙色渐变）
  - 设备列表：3行示例数据，状态用半透明底标签（在线=绿，告警=橙）

【7】应用场景（深色底 #0f1333）
- 小标签 + 标题 + 描述
- 4列场景卡片：
  ① 🏠 智能家居（4条列表，›前缀）
  ② 🚗 智能交通
  ③ 🛡️ 智能安防
  ④ 🏭 工业物联网
- 悬停：蓝色光晕 + 上移5px + 底部出现蓝→蓝渐变装饰线

【8】客户案例（深色底 #0a0e27，左右两栏）
- 左栏：小标签 + 标题 + 描述 + 3个资质badge（运营商授权/科技型中小企业/ICP许可）
- 右栏：3×2 Logo网格（6个客户，每个包含公司名+行业标签）
- Logo卡片：深色底、半透明边框、悬停电光蓝光晕

【9】服务保障（深色底 #0f1333）
- 小标签 + 标题 + 描述
- 4列服务卡片（🕐快速响应 / ⚙️技术支持 / 📞投诉热线 / 🎯定制化方案）
- 下方：蓝色渐变横条（contact-strip），左侧标题+描述，右侧联系电话/微信/邮箱
  - 联系信息每个带半透明圆形图标容器
  - 右上角径向渐变装饰光斑

【10】关于我们（深色底 #0a0e27，左右两栏）
- 左栏：蓝色渐变卡片（about-card），大字标题 + 公司简介 + 4个数据highlight（20+集团员工/1006万注册资本/50+企业客户/100万+营收）
  - 右上角径向渐变装饰光斑
- 右栏：小标签 + 公司全名标题 + 地址+规模描述 + 「查看产品详情」链接（电光蓝下划线，hover时gap变大）

【11】CTA区（深色底 #0f1333，居中）
- 中心径向渐变装饰光斑
- 标题「免费申请样卡，先试再决定」
- 描述文字
- 双按钮：主按钮带橙色脉冲发光动画 + 次按钮电光蓝边框

【12】Footer（深蓝黑底 #0a0e27）
- 顶边框 rgba(255,255,255,0.08)
- 4列：品牌（Logo+简介）/ 产品中心链接 / 支持服务链接 / 联系我们
- 链接hover变电光蓝
- 底栏：© 年份范围 公司名 版权所有 | ICP备案号

【13】浮动按钮
- 右下角固定：橙色圆形「📞」拨号按钮（带橙色光晕）+ 深色「↑」回顶按钮（滚动后显示）
- 尺寸 50×50px

=============
四、动效要求
=============
- Canvas粒子连线动画（Hero背景，80粒子，蓝色，距离<150px连线）
- 滚动渐显fade-up（IntersectionObserver，threshold 0.15，opacity 0→1 + translateY 40px→0）
- 数字滚动计数（IntersectionObserver触发，requestAnimationFrame，easeOutCubic，2秒）
- 卡片hover发光边框+上移（transition 0.4s）
- CTA按钮脉冲发光（@keyframes pulse-glow-orange）
- Hero底部箭头弹跳（@keyframes bounce-arrow）
- 导航链接hover/active变电光蓝+底部边框

=============
五、响应式要求
=============
- 三个断点：1024px / 768px / 480px
- 移动端导航隐藏常规菜单，显示汉堡按钮
- 所有多列网格在移动端变为单列或双列
- Hero区按钮在移动端变为100%宽度（max-width 320px）
- Hero高度在移动端缩减为90vh

=============
六、技术要求
=============
- 单HTML文件，所有CSS内嵌在 <style> 中，所有JS内嵌在 <script> 中
- 不依赖任何外部库或框架
- 使用 CSS 变量（:root）统一管理颜色
- Logo 使用 <img src="logo-2.png">，高度 48px，宽度自适应
- Logo 深色背景适配：filter: invert(1) hue-rotate(180deg) brightness(1.2) saturate(1.4)
- Hero 粒子动画用纯 Canvas JS 手写
- 管理后台截图区用纯 CSS/HTML 模拟，深色仪表盘风格，不要用图片
- 地址、电话等联系信息统一，无多余空格
- 统计数字与 About 区数据保持一致
- 管理后台数据用 "—" 占位，不用假数字

=============
七、交付
=============
输出完整可运行的 index.html 文件，我直接双击即可在浏览器中预览。
```

---

## 七、关键注意事项（踩坑记录）

1. **Logo 深色适配**：原 Logo 为浅底设计，深色背景上需用 `filter: invert(1) hue-rotate(180deg) brightness(1.2) saturate(1.4)` 反转并恢复色相。不要用 `brightness(0) invert(1)` 会丢失品牌蓝紫色。
2. **地址格式**：数字与单位之间不留空格（如 `149号`，不是 `149 号`）。
3. **管理后台数据**：不要用假数字（如 3,847 台），统一用 `—` 占位。
4. **统计条数据**：要与 About 区 highlight 数据完全一致，不要两处写不同的数字。
5. **clamp() 语法**：CSS `clamp()` 内逗号后有空格，如 `clamp(32px, 6vw, 60px)`。
6. **二级标题 ID**：核心优势 section 的 id 是 `advantage`（历史拼写，保持一致）。
7. **移动端导航关闭**：每个菜单项 onclick 都要调用 `toggleMobileNav()` 关闭菜单。
8. **深色卡片边框**：使用 `rgba(255,255,255,0.08)` 而非实色边框，在深底上更自然。
9. **发光效果强度**：box-shadow 的 blur 值控制在 20-40px，过大显得廉价。
10. **粒子动画性能**：粒子数量控制在80个，连线距离150px，避免低端设备卡顿。
11. **fade-up 交错延迟**：同级多个 fade-up 元素依次延迟 80ms，节奏感更好。

---

## 八、文件清单

```
yuanzizn/
├── index.html                          ← 主页面（单文件，深色科技风 v2）
├── logo-2.png                          ← 公司 Logo（蓝紫云朵 + 元字中英文字）
├── 创始人名片2.png                      ← 创始人名片
├── STYLE_GUIDE.md                      ← 网站风格指南（本文档）
└── 元字智能科技（河南）有限公司物联网业务介绍-最终版2.pdf  ← 公司业务介绍
```

---

*最后更新：2026-05-19 · v2 深色科技风*
