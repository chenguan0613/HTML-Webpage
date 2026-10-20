# Day1 复习

## 标签语法

```html
<!-- 双标签 如-->
<p>contents</p>
<!-- 单标签 如-->
<br>, <hr>, <img src="1.png">
```

属性写到标签里，属性名="属性值"， 不同属性见用空格隔开

```html
<a href="http://example.com" target="blank">links</a>
```

## HTML骨架

```html
<!DOCTYPE html>              <!-- 1. 声明文档类型：这是 HTML5 -->
<html lang="zh-CN">          <!-- 2. 根标签，lang 声明语言 -->
<head>                       <!-- 3. 头部：给浏览器看的信息，页面上不显示 -->
    <meta charset="UTF-8">   <!--    字符编码，保证中文不乱码 -->
    <title>网页标题</title>   <!--    标签页上的标题 -->
</head>
<body>                       <!-- 4. 身体：页面真正显示的内容都在这里 -->

</body>
</html>

```

## 排版标签

| 标签 | 含义 |
| :---: | :---: |
| `<h1>`~`<h6>` | 标题 |
| `<strong>` / `<b>` | 加粗 |
| `<em>` / `<i>` | 斜体 |
| `<ins>` / `<u>` | 下划线 |
| `<del>` / `<s>` | 删除线 |
| `<sub>` / `<sup>` | 下标/上标 |

## 换行与水平线标签

```html
<br>   <!-- 换行：文字断到下一行，不产生段落间距 -->
<hr>   <!-- 水平线：画一条分隔横线 -->
```

`<br>`和`<p>`的区别: `<br>`只换行，`<p>`是另起一段，段落间是又间距的。

## 图像标签

```html
<img src="图片路径" alt="图片描述">
```

`src`为图片路径，`alt`为加载失败时显示的文字。

## 超链接标签

```html
<a href="目标地址">可点击的文字或图片</a>
```

`href` 决定跳到哪里，常用写法：

| 用法 | 例子 | 说明 |
| :--- | :--- | :--- |
| 外链 | `<a href="https://www.baidu.com">百度</a>` | 跳到别的网站 |
| 相对路径 | `<a href="about.html">关于</a>` | 跳本站另一页 |
| 锚点 | `<a href="#intro">跳到简介</a>` | 跳同页某位置 |
| 空链接 | `<a href="#">占位</a>` | 还没定跳哪时用 |

`target="_blank"` 在新标签页打开（默认是当前页跳转）。

锚点链接分两步：

```html
<!-- 第 1 步：给目标元素加 id -->
<h2 id="intro">简介</h2>

<!-- 第 2 步：用 #id 跳过去 -->
<a href="#intro">回到简介</a>
```

## 多媒体标签

### 音频

```html
<audio src="music.mp3" controls></audio>
```

| 属性 | 作用 |
| :--- | :--- |
| `src` | 音频路径 |
| `controls` | 显示播放控件，不写就没有 |
| `autoplay` | 自动播放（浏览器常禁止） |
| `loop` | 循环播放 |
| `muted` | 静音 |
| `preload="none"` | 点击时才加载，省流量 |

### 视频

```html
<video src="movie.mp4" controls width="600" height="400"></video>
```

`<video>` 支持 `<audio>` 的所有属性，还多了 `width` / `height` / `poster`（封面图）。

### 兼容多格式

不同浏览器支持的格式可能不同，用 `<source>` 写多个候选：

```html
<audio controls>
    <source src="music.mp3" type="audio/mpeg">
    <source src="music.ogg" type="audio/ogg">
    你的浏览器不支持 audio 标签
</audio>
```
