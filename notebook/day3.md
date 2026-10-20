# day3复习

## CSS 引入方式（3 种）

| 方式 | 写法 | 说明 |
| :--- | :--- | :--- |
| 行内 | `<p style="color:red">` | 写在标签的 `style` 属性里 |
| 内嵌 | `<head>` 里写 `<style>...</style>` | 写在本页 head 里 |
| 外链 | `<link rel="stylesheet" href="style.css">` | 单独 .css 文件，全站共用 |

```html
<!-- 行内：只作用当前标签 -->
<p style="color: red;">红字</p>

<!-- 内嵌：作用整个页面 -->
<head>
    <style>
        p { color: red; }
    </style>
</head>

<!-- 外链：作用所有引入它的页面 -->
<link rel="stylesheet" href="style.css">
```

优先级：行内 > 内嵌/外链。

## 选择器

```css
选择器 {
    属性: 值;   /* 每条声明用分号结尾 */
}
```

| 选择器 | 写法 | 选中谁 |
| :--- | :--- | :--- |
| 标签 | `p { }` | 所有 `<p>` |
| 类 | `.card { }` | 所有 `class="card"` |
| id | `#nav { }` | 唯一的 `id="nav"` |
| 通配符 | `* { }` | 所有元素 |

```css
p { color: black; }                /* 标签 */
.card { border: 1px solid #ccc; }  /* 类 */
#nav { background: blue; }         /* id */
* { margin: 0; }                   /* 通配符 */
```

优先级：id > 类 > 标签 > 通配符。

- 类 `.xxx` 用最广（可复用）
- id `#xxx` 一页只能出现一次
- 通配符 `*` 常用来一键清零默认样式

## 画盒子（盒模型）

每个元素都是一个盒子，由内到外四层：

```text
margin（外边距）→ border（边框）→ padding（内边距）→ content（内容）
```

```css
div {
    width: 250px;          /* 宽 */
    height: 100px;         /* 高 */
    border: 1px solid #080808;   /* 边框：粗细 样式 颜色 */
    border-radius: 10px;   /* 圆角 */
    padding: 10px 16px;    /* 内边距 */
    margin: 0 0 12px 20px; /* 外边距 */
    background: #f4f6f4;   /* 背景 */
}
```

- border 三件套：`粗细 样式 颜色`，样式常用 `solid`（实线）、`dashed`（虚线）
- padding/margin 缩写：`上 右 下 左`（顺时针）；2 个值 = 上下/左右，1 个值 = 四周
- `border-radius: 50%` 就是圆形

## 字体修饰属性

| 属性 | 作用 | 常用值 |
| :--- | :--- | :--- |
| `font-weight` | 粗细 | `normal`(400) / `bold`(700) / 100~900 |
| `font-style` | 斜体 | `normal` / `italic` |
| `font-size` | 字号 | `16px` / `1.2em` |

```css
p {
    font-weight: bold;   /* 加粗 */
    font-style: italic;  /* 斜体 */
    font-size: 18px;     /* 字号 */
}
```

## 行高 line-height

控制一行文字的高度（两行之间的间距）。

```css
p { line-height: 1.5; }   /* 1.5 倍字号，最灵活 */
p { line-height: 30px; }  /* 固定 30px */
```

用倍数（1.5、1.8）随字号自动缩放，最灵活。

## 字体族 font-family

写多个字体作为「备胎」，前面的没有就用后面的。

```css
body {
    font-family: "Microsoft YaHei", "PingFang SC", sans-serif;
}
```

- 中文/带空格的字体名加引号
- 最后放通用字体族兜底：`sans-serif`（无衬线）、`serif`（衬线）、`monospace`（等宽，代码常用）

## font 属性（简写）

把字体相关属性合并成一行：

```css
/* 分开写 */
p {
    font-style: italic;
    font-weight: bold;
    font-size: 18px;
    line-height: 1.5;
    font-family: "Microsoft YaHei", sans-serif;
}

/* 简写（顺序固定） */
p {
    font: italic bold 18px/1.5 "Microsoft YaHei", sans-serif;
}
```

顺序固定：`font-style font-weight font-size/line-height font-family`

- `font-size` 和 `font-family` 必须写，其他可省略
- 字号和行高之间用 `/` 连：`18px/1.5`

## 文本修饰属性

| 属性 | 作用 | 常用值 |
| :--- | :--- | :--- |
| `text-decoration` | 文字装饰线 | `none` / `underline` / `line-through` / `overline` |
| `text-align` | 水平对齐 | `left` / `center` / `right` |
| `text-indent` | 首行缩进 | `2em`（缩进 2 个字） |

```css
a { text-decoration: none; }      /* 去掉下划线 */
p { text-decoration: underline; } /* 加下划线 */
h1 { text-align: center; }        /* 居中 */
p { text-indent: 2em; }           /* 首行缩进两个字 */
```

## 文字颜色 color

```css
h1 { color: #121111; }                    /* 十六进制，最常用 */
h1 { color: rgb(104, 119, 185); }         /* 红绿蓝 0~255 */
h1 { color: rgba(255, 255, 255, 0.85); }  /* 多一个 a = 透明度 0~1 */
```

| 写法 | 说明 |
| :--- | :--- |
| `#f4f6f4` | 十六进制，6 位，两位一组（红绿蓝） |
| `rgb(104,119,185)` | 十进制红绿蓝 |
| `rgba(...,0.85)` | 加透明度，0 全透明 / 1 不透明 |

## 调试工具（DevTools）

按 **F12**（或右键 →「检查」）打开。

| 功能 | 怎么做 | 作用 |
| :--- | :--- | :--- |
| 选元素 | 点左上角箭头图标，再点页面元素 | 高亮定位元素 |
| 看样式 | 右侧 Styles 面板 | 看元素用了哪些 CSS |
| 实时改 | 点任意属性值直接改 | 页面立刻变，但只是临时预览 |

调试流程：F12 → 点箭头 → 点元素 → 右侧看样式 → 直接改值实时预览 → 满意后抄回代码文件。

- DevTools 里改样式**不会保存**，刷新就恢复，最终要写回文件
- 样式没生效时，在 Styles 面板里会被**划掉**，说明被更高优先级覆盖了
- 盒子模型：Styles 面板下面有示意图，鼠标移上去会在页面高亮 margin/border/padding 区域
