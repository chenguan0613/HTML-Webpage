# day2 复习

## 列表

列表靠 `<li>` 装每一项，外面包不同的容器：

```html
<!-- 无序列表：圆点 -->
<ul>
    <li>第一条</li>
    <li>第二条</li>
</ul>

<!-- 有序列表：数字 1. 2. 3. -->
<ol>
    <li>第一步</li>
    <li>第二步</li>
</ol>
```

| 标签 | 含义 |
| :--- | :--- |
| `<ul>` | 无序列表，前面是圆点 |
| `<ol>` | 有序列表，自动编号 |
| `<li>` | 列表项 |

```html
<ul>
    <li>水果
        <ul>
            <li>苹果</li>
            <li>香蕉</li>
        </ul>
    </li>
</ul>
```

## 表格

```html
<table>
    <tr>
        <th>姓名</th>
        <th>年龄</th>
    </tr>
    <tr>
        <td>奏</td>
        <td>17</td>
    </tr>
</table>
```

| 标签 | 含义 |
| :--- | :--- |
| `<table>` | 整个表格 |
| `<tr>` | 一行 |
| `<th>` | 表头单元格（加粗居中） |
| `<td>` | 普通数据单元格 |

## 合并单元格

colspan 横着并，rowspan 竖着并

| 属性 | 方向 | 含义 |
| :--- | :--- | :--- |
| `colspan="2"` | 横向 | 横跨 2 列 |
| `rowspan="2"` | 纵向 | 竖跨 2 行 |

```html
<!-- 横向合并 -->
<tr><td colspan="2">横跨两列</td></tr>

<!-- 纵向合并 -->
<tr><td rowspan="2">竖跨两行</td><td>A</td></tr>
<tr><td>B</td></tr>
```

> 用了 `colspan` 后这一行要少写一个单元格；`rowspan` 同理，下一行少写一格。

## 表单 form

| 标签 | 作用 |
| :--- | :--- |
| `<form>` | 表单容器，包住所有控件 |
| `<input>` | 输入框（靠 `type` 变类型） |
| `<select>` + `<option>` | 下拉菜单 |
| `<textarea>` | 多行文本域 |
| `<label>` | 标签文字，点它聚焦输入框 |
| `<button>` | 按钮 |

### input 标签

```html
<input type="text">      <!-- 普通文本 -->
<input type="password">  <!-- 密码，显示为 ••• -->
<input type="email">     <!-- 邮箱，自带格式校验 -->
<input type="radio">     <!-- 单选按钮 -->
<input type="checkbox">  <!-- 多选勾选框 -->
```

| 属性 | 作用 |
| :--- | :--- |
| `name` | 给控件起名；**同名 radio 才能互斥** |
| `value` | 提交时传的值 |

```html
<!-- 两个 radio 都叫 gender，所以只能选一个 -->
<label><input type="radio" name="gender" value="male">男</label>
<label><input type="radio" name="gender" value="female">女</label>

<!-- checkbox 同名算一组，可勾多个 -->
<label><input type="checkbox" name="hobby" value="music">音乐</label>
```

> 重点：单选靠 `name` 相同实现互斥。

### 下拉菜单

```html
<select name="city">
    <option value="">请选择</option>
    <option value="beijing">北京</option>
    <option value="shanghai">上海</option>
</select>
```

### 文本域（多行）

```html
<textarea name="sign" rows="3"></textarea>
```

`rows="3"` 显示 3 行高，能输多行（`input` 只能输一行）。

### label 标签

```html
<label for="username">用户名</label>
<input type="text" id="username">
```

`label` 的 `for` = 对应控件的 `id`，点文字会自动聚焦到输入框。
另一种写法：直接用 `<label>` 包住控件，如 `<label><input type="radio">男</label>`。

### 按钮 button

```html
<button type="submit">注册</button>   <!-- 提交表单 -->
<button type="reset">重置</button>    <!-- 清空表单 -->
<button type="button">普通按钮</button> <!-- 配合 JS 用 -->
```

| `type` | 作用 |
| :--- | :--- |
| `submit` | 提交表单 |
| `reset` | 恢复初始值 |
| `button` | 普通按钮，需 JS 绑定 |

## div 和 span

| 标签 | 类型 | 特点 |
| :--- | :--- | :--- |
| `<div>` | 块级 | 独占一行，自动换行，做布局分区 |
| `<span>` | 行内 | 不换行，给一段文字里几个字单独加样式 |

```html
<div>块级，独占一行</div>
<div>块级，另起一行</div>

<p>这句话里 <span>这几个字</span> 可以单独上色</p>
```

## 字体实体

有些符号在 HTML 里有特殊含义，要显示得用「实体」：

| 写法 | 显示 | 说明 |
| :--- | :--- | :--- |
| `&nbsp;` | （空格） | 不换行空格 |
| `&lt;` | `<` | 小于号 |
| `&gt;` | `>` | 大于号 |
| `&amp;` | `&` | 与号 |
| `&copy;` | © | 版权 |
| `&middot;` | · | 中间点 |
| `&times;` | × | 乘号 |
| `&yen;` | ¥ | 人民币 |

> 想显示 `<h1>` 这几个字，要写成 `&lt;h1&gt;`，否则会被当成标签。
