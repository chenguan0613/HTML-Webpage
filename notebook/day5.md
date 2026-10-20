# day5 复习

## 结构伪类选择器

根据元素在兄弟中的位置来选中。

| 伪类 | 选中 |
| :--- | :--- |
| `:first-child` | 第一个子元素 |
| `:last-child` | 最后一个子元素 |
| `:nth-child(n)` | 第 n 个 |
| `:nth-child(odd)` / `:nth-child(even)` | 奇数 / 偶数个 |
| `:nth-child(2n)` | 2、4、6…（等价 even） |
| `:nth-child(2n+1)` | 1、3、5…（等价 odd） |
| `:only-child` | 唯一的子元素 |

```css
li:first-child { color: red; }
li:last-child { color: blue; }
li:nth-child(2) { color: green; }
li:nth-child(even) { background: #f0f0f0;}
```

`nth-child` 按「在所有兄弟中的位置」数，不是「第几个同类型」。

## 伪元素选择器

伪元素是「创造」一个原本不存在的虚拟元素。

| 伪元素 | 作用 |
| :--- | :--- |
| `::before` | 在元素内容前面插入内容 |
| `::after` | 在元素内容后面插入内容 |
| `::first-letter` | 第一个字 |
| `::first-line` | 第一行 |
| `::selection` | 被选中的文字 |

```css
p::before { content: "*"; }
p::after { content: "（完）"; color: #999; }
p::first-letter { font-size: 30px; color: red; }
::selection { background: yellow; }
```

核心规则：`::before` / `::after` 必须写 `content`，否则不显示（空内容写 `content: ""`）。

伪类 `:hover` 是「已有元素的状态」（单冒号）；伪元素 `::before` 是「创造新元素」（双冒号）。

## PxCook 用法

PxCook 是把设计稿量成代码的工具。

| 步骤 | 做什么 |
| :--- | :--- |
| 导入 | 打开设计稿（PSD / Sketch / XD） |
| 标注 | 点元素，显示宽高、颜色、字号、间距 |
| 复制 | 直接复制生成的 CSS 代码 |
| 切图 | 导出图标/图片文件 |

流程：拿到设计稿 → 量出版心宽度和各区块尺寸 → 逐个量宽高/字体/颜色/圆角/阴影 → 复制进 CSS。

核心价值：别肉眼估尺寸，用工具量，页面才能和设计稿一致。PxCook 量设计稿，F12 调试页面，一对搭档。

## 盒子模型

### 组成（由内到外）

```text
content（内容）→ padding（内边距）→ border（边框）→ margin（外边距）
```

### 边框线 border

```css
border: 2px solid red;   /* 粗细 样式 颜色 */
```

样式：`solid` 实线、`dashed` 虚线、`dotted` 点线、`none` 无。
可单独设边：`border-top` / `border-bottom` / `border-left` / `border-right`。

### 内边距 padding

```css
padding: 10px;                 /* 四周 */
padding: 10px 20px;            /* 上下 左右 */
padding: 10px 20px 30px 40px;  /* 上 右 下 左 */
```

### 尺寸计算（content-box vs border-box）

默认 `content-box`：width 只算内容区，边框和内边距额外加。

```css
div {
    width: 200px;
    padding: 10px;
    border: 5px solid red;
    /* 实际宽度 = 200 + 10*2 + 5*2 = 230px */
}
```

改 `border-box`：width 直接等于含 padding 和 border 的总宽。

```css
div {
    box-sizing: border-box;
    width: 200px;   /* 最终就是 200，不再额外加 */
}
```

项目开头统一写：`* { box-sizing: border-box; }`

## 版心居中

```css
.page {
    max-width: 1200px;   /* 最大宽度，窄屏自动缩小 */
    margin: 0 auto;      /* 上下 0，左右 auto = 居中 */
}
```

居中秘诀：块级元素 + 有宽度 + `margin: 0 auto`。

## 清除默认样式

浏览器会给部分元素加默认 margin/padding（body 有 8px、ul 有缩进等）。

```css
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
```

## 内容溢出 overflow

| 值 | 效果 |
| :--- | :--- |
| `visible` | 默认，溢出照样显示 |
| `hidden` | 溢出部分裁掉隐藏 |
| `scroll` | 一直显示滚动条 |
| `auto` | 溢出时才出现滚动条（最常用） |

```css
.box { overflow: auto; }    /* 内容多就出滚动条 */
.card { overflow: hidden; } /* 裁掉超出圆角的内容 */
```

## 外边距问题

### 兄弟之间：垂直 margin 合并（取最大值）

```css
.box1 { margin-bottom: 30px; }
.box2 { margin-top: 50px; }
/* 间距是 50px（取大），不是 80px */
```

只有垂直方向合并，水平不合并。

### 父子之间：子元素 margin-top 塌陷到父元素

```css
.parent { background: #eee; }   /* 父没设 padding/border */
.child { margin-top: 50px; }
/* 结果：子没动，整个父元素一起往下跑了 */
```

解决方案（给父元素加其一）：

1. `padding-top: 1px;`
2. `border-top: 1px solid transparent;`
3. `overflow: hidden;`

记忆：父和第一个子元素之间，别用子元素的 margin-top，改用父元素的 padding-top。

## 行内元素的垂直内外边距

| 方向 | 是否有效 |
| :--- | :--- |
| 水平（左右） | 有效，能撑开距离 |
| 垂直（上下） | 不占位，没效果 |

```css
a { padding: 10px; }   /* 左右有效，上下无效 */
```

解决：把行内元素改成行内块。

```css
a { display: inline-block; }   /* 上下 margin/padding 生效 */
```

## 圆角与盒子阴影

### 圆角 border-radius

```css
.box { border-radius: 10px; }   /* 四角 10px */
.box { border-radius: 50%; }    /* 圆形（宽高相等时） */
```

### 盒子阴影 box-shadow

```css
box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
/*          水平 垂直 模糊 颜色 */
```

| 值 | 含义 |
| :--- | :--- |
| 第 1 个 | 水平偏移（正右负左） |
| 第 2 个 | 垂直偏移（正下负上） |
| 第 3 个 | 模糊半径（越大越模糊） |
| 第 4 个 | 颜色（常用半透明黑） |

```css
box-shadow: 0 2px 8px rgba(0,0,0,0.08);    /* 淡投影，卡片常用 */
box-shadow: 0 10px 24px rgba(0,0,0,0.55);  /* 深投影，悬浮感 */
box-shadow: 0 0 0 2px red;                 /* 无偏移无模糊 = 描边 */
```
