# day4复习

## 复合选择器

| 类型 | 写法 | 含义 | 例子 |
| :--- | :--- | :--- | :--- |
| 后代 | `A B`（空格） | A 里面任意层级的 B | `.card h2` |
| 子代 | `A > B` | A 的直接子级 B | `.main > img` |
| 并集 | `A, B`（逗号） | A 和 B 都选 | `h1, h2, h3` |
| 交集 | `AB`（连着写） | 同时满足 A 和 B | `p.card` |

```css
/* 后代：card 里所有的 h2（隔几层都行） */
.card h2 { color: blue; }

/* 子代：只选 main 的直接子级 img */
.main > img { width: 100%; }

/* 并集：多个选择器共用一套样式 */
h1, h2, h3 { color: rgb(104, 119, 185); }

/* 交集：既是 p 又带 card 类 */
p.card { border: 1px solid #ccc; }
```

记忆：空格 = 后代，`>` = 亲儿子，逗号 = 一起选。

## 伪类选择器

伪类表示元素的某种状态。

| 伪类 | 含义 |
| :--- | :--- |
| `:hover` | 鼠标悬停 |
| `:focus` | 获得焦点（输入框被点击） |
| `:first-child` | 第一个子元素 |
| `:last-child` | 最后一个子元素 |
| `:nth-child(n)` | 第 n 个子元素 |

```css
a:hover { color: red; }
input:focus { border-color: blue; }
li:first-child { font-weight: bold; }
li:nth-child(2) { color: green; }
```

链接专属伪类（顺序固定，记 LVHA）：

```css
a:link { color: blue; }     /* 未访问 */
a:visited { color: purple; } /* 访问过 */
a:hover { color: red; }      /* 悬停 */
a:active { color: orange; }  /* 点击瞬间 */
```

顺序：`:link → :visited → :hover → :active`

## CSS 三大特性

### 层叠性

同一个选择器，写在后面的覆盖前面的：

```css
p { color: red; }
p { color: blue; }   /* 生效 */
```

### 继承性

文字/字体相关属性会传给子元素：`color`、`font-*`、`line-height`、`text-*`。
盒子相关（width/height/margin/padding/border/background）不继承。

```css
body { color: #333; }   /* 所有文字自动变灰 */
```

### 优先级

```text
行内样式 > id > 类/伪类 > 标签 > 通配符 > 继承
```

越「具体」越优先（id 比 class 具体，class 比标签具体）。

## Emmet 写法

输入简写 + Tab 展开成代码。

| 符号 | 作用 | 例子 | 展开结果 |
| :--- | :--- | :--- | :--- |
| `.` | 类 | `.card` | `<div class="card"></div>` |
| `#` | id | `#nav` | `<div id="nav"></div>` |
| `>` | 子元素 | `ul>li` | `<ul><li></li></ul>` |
| `+` | 兄弟 | `div+p` | `<div></div><p></p>` |
| `*` | 重复 | `li*3` | 3 个 `<li>` |
| `{}` | 文字 | `p{你好}` | `<p>你好</p>` |
| `$` | 自动编号 | `li.item$*3` | item1、item2、item3 |
| `()` | 分组 | `(ul>li)*2` | 两个 ul |

```text
输入: ul>li.item$*3
展开:
<ul>
    <li class="item1"></li>
    <li class="item2"></li>
    <li class="item3"></li>
</ul>
```

默认省略标签名用 `<div>`，其他标签要写标签名（如 `p.card`）。

## 背景属性

### 拆分写法

```css
body {
    background-color: #fff;               /* 背景色 */
    background-image: url("bg.png");      /* 背景图 */
    background-repeat: no-repeat;         /* 是否重复 */
    background-position: center;          /* 位置 */
    background-size: cover;               /* 尺寸 */
    background-attachment: fixed;         /* 是否固定 */
}
```

| 属性 | 作用 | 常用值 |
| :--- | :--- | :--- |
| `background-color` | 背景色 | `#fff` / `rgba(...)` |
| `background-image` | 背景图 | `url("...")` |
| `background-repeat` | 重复 | `no-repeat` / `repeat` / `repeat-x` / `repeat-y` |
| `background-position` | 位置 | `center` / `left top` / `60% 30%` |
| `background-size` | 尺寸 | `cover` / `contain` / `100%` |
| `background-attachment` | 固定 | `fixed` / `scroll` |

### 复合写法

```css
body {
    background: #fff url("bg.png") no-repeat center / cover;
    /*        颜色  图片        重复    位置  / 尺寸 */
}
```

`position` 和 `size` 之间用 `/` 隔开，可省略不需要的值。

## 显示模式 display

| 值 | 类型 | 特点 | 例子 |
| :--- | :--- | :--- | :--- |
| `block` | 块级 | 独占一行、能设宽高 | `div`、`p`、`h1`、`ul` |
| `inline` | 行内 | 不换行、不能设宽高 | `span`、`a`、`strong` |
| `inline-block` | 行内块 | 不换行、能设宽高 | `img`、`input` |
| `none` | 隐藏 | 彻底消失、不占位 | 配合 JS 显隐 |

```css
div { display: block; }
span { display: inline; }
a { display: inline-block; width: 100px; height: 40px; }
div { display: none; }
```

可以互相转换：

```css
.dropdown a { display: block; }        /* 行内变块级，整行可点 */
li { display: inline-block; }          /* 块级变行内块，横向排 */
```

`flex` 和 `grid` 也是 `display` 的值，属于布局，后续展开。
