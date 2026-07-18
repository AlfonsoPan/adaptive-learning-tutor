---
name: interactive-teaching-svg
description: 把知识点绘制成风格统一的中文交互式教学 SVG 图（指针与触摸交互、可选滑杆联动、ARIA 无障碍、静态首帧完整可读），并通过 Obsidian iframe 安全插入。适用于学习笔记、Obsidian 库、教程配图的绘制，以及把 Excalidraw/手绘草图重构成规范教学图。
---

# 交互式教学 SVG 出图规范

把一段教材/笔记内容变成一张"能讲、能点、能拖、能看"的单文件 SVG 教学图。成品统一使用 1200×688 逻辑画布的浅色卡片式版面：大标题 + 小节号副标题，分区卡片承载内容，关键部件支持触摸/鼠标轻点与拖动，底部有交互说明面板，无任何外部依赖。

配套文件：`assets/template.svg` 是可直接渲染的最小完整骨架。必须保留其中的 1200×688 根节点、`<style>`、`<defs>` active-glow 滤镜、底部交互面板样式和末尾 `<script>` IIFE 的基线行为；按内容替换 topics 字典和图形元素。只有加入滑杆等真实交互控件时才扩展脚本，扩展不得删减 pointer 四事件、捕获/释放、键盘、复位与静态首帧一致性逻辑。

## 何时使用 / 不使用

- 适用：学习笔记配图、概念关系图、流程/因果链图、等效电路/磁路图、波形与矢量图、需要"指着讲"的教学示意。
- 不适用：精确数据可视化（用图表库）、照片级渲染、需要打印投稿的矢量图（本规范面向屏幕阅读）。

## 六条设计原则

1. **静态优先**：禁用 JS、转为 PDF 或只查看首帧时，画面必须完整表达全部信息。初始 SVG 标记中的图形位置、数值、滑杆位置与提示文字必须和 JavaScript 初始化完成后的状态一致，脚本启动时不得发生可见跳变。交互只是增强，不得承载唯一的关键结论。
2. **单文件自包含**：图形、CSS、JavaScript 全部放在同一个 `.svg` 内；禁止外链字体、图片、CSS、JS、模块或任何网络资源，也不要使用 `<image>` 引入本地文件。禁止 `fetch()`、远程 URL、本地绝对路径、`window.parent`、`window.top`、`parent.document` 以及对父页面的其他依赖。交互界面优先使用 SVG 原生图元，尽量不用 `foreignObject`、HTML `<input>` 或其他内嵌 HTML 控件。
3. **信息保真**：重构图时保留原图全部标签、数值、结构关系；数值与正文冲突时以正文为准，不虚构物理内容。
4. **语义配色**：同一语义在所有图里用同一颜色（见配色表），读者跨图建立直觉。
5. **无障碍内置**：`title`/`desc`、ARIA、键盘可达、尊重 `prefers-reduced-motion`，一个都不能少。
6. **仅运行可信 SVG**：Obsidian 当前 iframe 不能添加 `sandbox`，因此只插入由当前工作流生成、完成代码审查和验收的 SVG；不得直接运行下载、复制或来源不明的 SVG。

## 画布与布局

- 根元素必须包含：`<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1200 688" width="100%" height="100%" style="display:block;width:100%;height:100%;" preserveAspectRatio="xMidYMid meet" role="img" aria-labelledby="svg-title svg-desc">`。统一保留 1200×688 `viewBox`，不得删除、改成固定像素尺寸或让 Obsidian 容器使用其他比例。
- 布局必须实际利用 1200×688 画布，避免内容只挤在上半部而产生大面积内部空白；全部可见内容、描边、滤镜光晕、箭头端头和底部面板均不得超出 `viewBox`。
- 紧跟 `<title id="svg-title">` 与 `<desc id="svg-desc">`。desc 结构：`图 X-X：一句话概括全图内容与关键结论……可悬停、点击高亮各部件。`
- 第一个绘制元素：用 `width="1200" height="688"` 铺满 `viewBox` 的白色 `<rect>` 背景。
- 大标题：`x=44 y=52`，27px、字重 600、`#0f172a`，点出结论而非泛泛命名（如"持续转矩来自磁场的切向作用，而不是完全对齐"）。
- 副标题：`x=44 y=78`，14px、`#64748b`，注明来源小节与图号，如 `§7.1 · 图 7-1：转子永磁磁链沿 d 轴，定子磁场在前方形成转矩角 δ`。
- 内容区从 y≈96 开始，左右页边距 40。分区一律用卡片：`<rect rx="12" fill="#f8fafc" stroke="#cbd5e1" stroke-width="1.2"/>`，卡片标题 16px/600/#0f172a，卡片内边距约 24。
- 多卡片布局：左右分栏（对比类）、中心辐射（因素汇聚类）、横向流程（因果链类）、环状（反馈闭环类）。箭头一律用 `<marker>` 端头，不用手画三角。
- **底部交互面板**（照抄模板）：`x=40 y=596 width=1120 height=76`、圆角 14 的浅底条；左侧蓝点（`#1971c2`，r=6）+ `interaction-title`（17px/500）+ `interaction-detail`（14px/#475569）。面板底部为 672，距 688 画布底部 16。

## 配色（只允许这个色板）

| 语义 | 颜色 |
|---|---|
| 主标题/强调文字 | `#0f172a` |
| 正文文字 | `#334155` / `#475569` |
| 次要文字/副标题/注记 | `#64748b` |
| 坐标轴/辅助线 | `#94a3b8` |
| 卡片描边/分隔 | `#cbd5e1`；网格浅线 `#e2e8f0`；卡片底 `#f8fafc` |
| 磁通/信号流/磁路/主箭头（蓝） | 主 `#1d4ed8`，边 `#2563eb`，深字 `#1e40af`，浅底 `#eff6ff` |
| 电学量/功率/磁动势源/警示（橙） | 主 `#ea580c`，深字 `#c2410c`，浅底 `#ffedd5` |
| 结论/关键量/强调框（琥珀） | 边 `#d97706`，字 `#b45309`/`#92400e`，浅底 `#fffbeb` |
| 交互蓝点 | `#1971c2`；高亮光晕 `#38bdf8`（只出现在 defs 滤镜里） |

结构件、中性框用石板灰系填充（`#e2e8f0` 底 + `#64748b` 边）。不要在色板外发明颜色。

## 文字与符号

- 字体栈（已在 style 块中）：`-apple-system,BlinkMacSystemFont,'Segoe UI','PingFang SC',sans-serif`。禁止外链字体。
- 字号阶梯：大标题 27 / 卡片标题 16 / 正文 12.5–14 / 轴刻度与辅助 10.5–12.5。
- **下标用平级 tspan 写法**（嵌套 tspan 在部分渲染器错位，禁用）：
  `R<tspan dy="2" font-size="10">fe</tspan>`，后续文字再 `<tspan dy="-2">` 回到基线。
- 特殊符号直接写 Unicode：`Φ ψ δ ω θ π × · ⁻ ⁵ ⁶ µ ≈ ≤ ≥ ° → ⇒`。
- 公式保持线性排版（如 `Φ ≈ NI/(Rfe+Rg) ≈ 82.3 µWb`），不用 MathML。
- 文字宽度预算：中文 1 字 ≈ 字号 px，英文 1 字符 ≈ 0.55×字号。写每个 `<text>` 前估算宽度，确保不超出所在卡片/框的边界。

## 交互规范

每个可讲解的部件包成交互组：`<g data-topic="key" tabindex="0" role="button" aria-label="对该部件的一句话描述">`。

- 语义相同的多处元素共用同一个 `data-topic`，实现联动高亮（如两处气隙磁阻框）。
- 标准行为（模板脚本已实现，照抄即可）：鼠标悬停可预览，但任何关键功能都不能只依赖 hover；鼠标或触摸轻点锁定/再点取消；拖动超过阈值后松开不触发轻点；Esc 或轻点空白复位；键盘 Tab 聚焦、Enter/Space 等效轻点。
- 所有按压、移动与释放统一使用 `pointerdown`、`pointermove`、`pointerup`，同时处理 `pointercancel`；不要分别维护 mouse 与 touch 两套事件。按下后必须直接调用 `setPointerCapture(event.pointerId)`，不得把它写成可选调用；释放或取消时必须释放捕获并清理状态。
- 用约 8 px 的移动阈值区分轻点与拖动，避免拖动结束时误锁定主题。只有真实滑杆/拖动命中区使用 `.slider-hit-area` 或等效类并设置 `touch-action: none; cursor: pointer;`；普通 topic 保持可点击但不阻断页面滚动。
- JavaScript 必须使用 Obsidian 桌面端 Electron 与 iOS/Android 移动端 WebView 共同支持的标准 DOM、Pointer Events 和 SVG API；不得依赖仅桌面浏览器可用的实验 API、Node.js API 或外部运行时。
- 所有脚本放在相关 SVG 元素之后的 `<script><![CDATA[ ... ]]></script>` 中，初始化时直接通过 `document.getElementById()` 或当前 SVG 根节点查询元素；禁止依赖父页面 DOM。
- 脚本中的 `topics` 字典是唯一允许改写部分：每个 key 给出 `label`（面板标题）与 `detail`（一两句讲解，内容取自笔记正文，口语化、说清"所以怎样"）。含流向箭头的 topic 设 `animate: true`，点击时触发一次 `flow-once` 流动动画。
- **markup 里的每个 data-topic 键必须出现在 topics 字典中，反之亦然**——交付前必查。

### 可选：滑杆联动

图天然围绕一个连续变量（角度、时间、负载）时，可在交互面板右侧加滑杆（参照效果：拖动转矩角 δ 看 T/Tmax 变化、拖动 θe 让游标扫过波形）。要求：

- 轨道 rect + 手柄 circle + 名称与 min/max 刻度文字；手柄 `role="slider"`，带 `aria-valuemin/aria-valuemax/aria-valuenow`。
- 轨道上覆盖透明 `.slider-hit-area`，触摸命中高度不小于 36 px，优先取 44 px；支持点击轨道直接改变滑杆位置。
- 使用 `pointerdown` / `pointermove` / `pointerup` 和直接 `setPointerCapture(event.pointerId)` 实现拖动，结束时调用 `releasePointerCapture(event.pointerId)`，并处理 `pointercancel`；`.slider-hit-area` 必须设置 `touch-action: none; cursor: pointer;`，同时支持键盘 Left/Right/Home/End。滑杆使用原生 SVG 图元，尽量不用 HTML `<input>`。
- 拖动联动更新图中的矢量/游标/读数；**首帧取一个有教学代表性的值**（如 δ=52°），且 SVG 标记中预先写入的手柄位置、图形与数值必须与 JavaScript 初始化该值后的结果完全一致。
- 拿不准就不加——滑杆是加分项，不是必需项。

## 制作流程

1. **读源材料**：笔记正文（找到对应小节与图注）、原图/草图（提取全部信息要素：标签、数值、结构关系、公式）。
2. **定图眼**：用一句话写下这张图要让读者记住什么（它会成为大标题与 desc）。
3. **规划布局**：选布局类型（分栏/辐射/流程/环状），划分卡片，列出 data-topic 清单（通常 6–8 个），在固定 1200×688 画布内分配空间。
4. **写文件**：以 `assets/template.svg` 为骨架，保留根节点、style/defs/面板样式和脚本基线行为；填入内容元素与 topics 字典，并让内容充分使用画布。
5. **机器校验**：`python3 -c "import xml.dom.minidom,sys; xml.dom.minidom.parse(sys.argv[1]); print('OK')" 文件.svg` 必须输出 OK；程序化核对 data-topic 键与 topics 字典一一对应，并检查 pointer 四事件、`setPointerCapture(...)`/`releasePointerCapture(...)`、滑杆命中区大小与 `touch-action: none`。禁止外链、图片引用、网络请求、`fetch()`、绝对路径、父页面访问；检查 `viewBox="0 0 1200 688"`、根 `style`、背景尺寸、`preserveAspectRatio="xMidYMid meet"` 和静态/初始化状态一致。
6. **渲染目检**：用无头浏览器截图后亲眼看图：
   `"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless --disable-gpu --screenshot=/tmp/x.png --window-size=1200,688 "file:///绝对路径.svg"`（Edge/Chromium 同理）。
   检查：文字不出框、元素无意外重叠、箭头指向正确、下标无错位、配色符合语义。发现问题改坐标后重新截图复查。
7. **生成 Base64 快照并插入 Obsidian**：保留独立 `.svg` 源文件，把其完整 UTF-8 字节编码成无换行 Base64，写入 DataviewJS 的 `svgBase64`，再用 `data:image/svg+xml;base64,` 创建 iframe。禁止读取附件或调用 `getResourcePath()`。
8. **双端交互复验**：插入后必须分别在 Obsidian 桌面端和移动端实际加载、轻点并拖动一次，确认指针捕获、触摸、锁定/复位以及现有图形、数值、滑杆联动正常。任一端失败都必须修复并在两端重新复验；没有对应设备或无法完成实测时必须明确报告，不能声称通过。

## 验收清单（交付前逐项过）

- [ ] XML 解析通过；根元素包含 `viewBox="0 0 1200 688"`、`width="100%"`、`height="100%"`、`style="display:block;width:100%;height:100%;"` 和 `preserveAspectRatio="xMidYMid meet"`；内容充分使用画布且无裁切。
- [ ] `title`/`desc` 齐全，desc 含图号与"可悬停、点击高亮"。
- [ ] style 块、active-glow、交互面板样式和 IIFE 基线行为与模板一致；差异仅限准确 W/H、内容、topics、对应几何以及确有需要的滑杆扩展，且未削弱任何基线交互。
- [ ] 每个交互组都有 `data-topic`+`tabindex="0"`+`role="button"`+`aria-label`；键与 topics 字典一一对应。
- [ ] 脚本位于相关元素之后，使用 `pointerdown` / `pointermove` / `pointerup` / `pointercancel`，直接调用 `setPointerCapture()`/`releasePointerCapture()` 并处理取消；滑杆命中区至少 36–44 px、支持点击轨道定位且为 `touch-action: none`；鼠标和触摸共用同一逻辑。
- [ ] 颜色全部来自色板且语义正确；下标为平级 tspan 写法。
- [ ] 截图目检通过：无文字溢出、无重叠、箭头正确。
- [ ] 图形、CSS、JavaScript 完全自包含；无外部 JS、CSS、字体、图片、网络请求、`fetch()`、本地绝对路径或父页面访问；尽量无 `foreignObject`、HTML `<input>` 与内嵌 HTML；首帧与 JS 初始化状态一致。
- [ ] 重构场景：原图信息要素无遗漏，数值与正文一致。
- [ ] Obsidian 的 DataviewJS 使用外层 `aspect-ratio:1200 / 688` 和 iframe `display:block;width:100%;height:100%;border:0;background:transparent;`，不设固定像素高度、无 `sandbox`，`src` 仅为 `data:image/svg+xml;base64,` 加当前 `svgBase64`。
- [ ] 笔记没有调用 `adapter.read()`、`adapter.readBinary()`、`getResourcePath()`、`fetch()`、`URL.createObjectURL()`、`Blob`、`iframe.srcdoc` 或 `iframe.contentDocument`；独立 SVG 与解码后的 Base64 快照字节完全一致；桌面端和移动端均已实际加载、点击和拖动通过。

## 常见错误（不要犯）

- 发明色板外颜色、给每张图换一种风格——本规范的价值就在于跨图一致。
- 文字超出卡片、为塞内容缩到 10px 以下——减内容或增大 H，不缩字号。
- 关键信息只存在于交互 detail 里、静态画面看不到——静态优先原则被破坏。
- 使用 `<image>`、外部位图、系统外字体、网络资源、`foreignObject`、HTML `<input>` 或嵌套 tspan 下标。
- 只监听 `click`、`mousedown` 或 `touchstart`，导致鼠标和触摸行为不一致。
- 在笔记嵌入代码中读取附件或使用 `adapter.read()`、`adapter.readBinary()`、`getResourcePath()`、`fetch()`、对象 URL、Blob、`srcdoc`、`contentDocument`。
- 在未审查来源的情况下把外部 SVG 放进无 sandbox 的 iframe。

## Obsidian 兼容性（务必告知用户）

必须使用 Base64 数据 URI iframe，禁止使用 `![[xxx.svg]]` 或 SVG Viewer 代码块承载交互。独立 `.svg` 只作为源文件与单独打开入口保留，笔记实际显示固定的 Base64 快照。执行顺序如下：

1. 把可信且已验收的 SVG 保存到 Vault 内，根节点规范为 1200×688。把文件完整 UTF-8 字节编码成无换行 Base64，不做文本改写、URL 编码或二次转码。
2. 在笔记中先保留源文件链接（不是嵌入）：`[[assets/xxx.svg|↗ 单独打开 SVG]]`。
3. 使用以下 DataviewJS，并把 `svgBase64` 替换为源文件的完整 Base64：

   ```dataviewjs
   const svgTitle = "07_磁场夹角与转矩";
   const svgBase64 = "这里放完整的Base64内容";

   const wrapper = dv.container.createDiv();
   wrapper.style.cssText =
     "width:100%;aspect-ratio:1200 / 688;";

   const iframe = wrapper.createEl("iframe", {
     attr: {
       title: svgTitle,
       loading: "eager"
     }
   });

   iframe.style.cssText =
     "display:block;" +
     "width:100%;" +
     "height:100%;" +
     "border:0;" +
     "background:transparent;";

   iframe.src = "data:image/svg+xml;base64," + svgBase64;
   ```

4. 禁止在嵌入代码中使用 `adapter.read()`、`adapter.readBinary()`、`getResourcePath()`、`fetch()`、`URL.createObjectURL()`、`Blob`、`iframe.srcdoc` 或 `iframe.contentDocument`。不给 iframe 添加 `sandbox`；只运行经过审查、可信任的 SVG JavaScript。
5. 每次修改独立 SVG 后必须重新规范化根节点、重新进行 UTF-8 Base64 编码、替换 `svgBase64`，并把 Base64 解码结果与独立 SVG 做逐字节或 SHA-256 一致性校验。不得留下过期快照。
6. 在 Obsidian 桌面端实际完整加载、点击并拖动一次，再在 Obsidian 移动端重复；确认移动端不依赖附件是否下载，页面滚动与滑杆拖动无明显冲突，初始状态、数值、箭头和曲线同步，实际拖动后数值确实变化。
