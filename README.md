# SASS

使用教程参考官网文档：[https://www.sass.hk/](https://www.sass.hk/)

## SASS/SCSS

## 安装

全局安装：

```bash
npm install sass -g
```

## 编译

运行命令编译：

```bash
sass src/style.scss dist/style.css
```
表示将 `src` 目录下的 `style.scss` 文件编译为 `dist` 目录下的 `style.css` 文件，然后引用编译后的文件即可。

监听当个文件，每次修改保存时自动编译：

```bash
sass --watch src/style.scss:dist/style.css
```

监听整个文件夹：

```bash
sass --watch src/:dist/
```

## 在 Vue 中使用 SASS

1. 安装相关的包：

```bash
npm install --save-dev sass    // 如果已经全局安装，则可以跳过
npm install --save-dev sass-loader@7.3.1 node-sass
// sass-loader 安装 7.3.1 的版本，安装较高版本可能报错： Module build failed: TypeError: this.getResolve is not a function
```

2. 对于 Vue 文件，修改 `<style>` ：
```html
<style scoped lang="scss">
$red: #ff0000;

body {
    background-color: $red;
}
</style>
```

3. 运行 `npm run dev`，打开项目，样式生效。

4. 格式化 `.scss` 代码。在 VS Code 的扩展库中查找并安装 SCSS Formatter，需要格式代码时，在文档中右键-> Format Document With -> SCSS Formatter

## 项目中使用 SASS 的最佳实践

### 1.目录结构

创建 `src/assets/styles` 目录，用于存放通用的样式文件。对于某个页面/组件/布局中的特定样式，可以在当前页面中定义样式，或者在页面所在的文件夹定义样式文件，这样便于维护。

### 2.定义全局样式

创建 `styles/global.scss` 全局样式文件，在入口脚本文件 `src/main.js`中引入：

```js
import './assets/styles/global.scss';
```

### 3.重置默认样式

不同浏览器的默认样式不同，为了使页面在不同浏览器中按照预期进行显示，可以对浏览器的默认样式进行覆盖。创建 `styles/reset.scss`：

```scss
/* 覆盖默认样式 */
html, body, div, span, applet, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
a, abbr, acronym, address, big, cite, code,
del, dfn, em, img, ins, kbd, q, s, samp,
small, strike, strong, sub, sup, tt, var,
b, u, i, center,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, embed,
figure, figcaption, footer, header, hgroup,
menu, nav, output, ruby, section, summary,
time, mark, audio, video {
  margin: 0;
  padding: 0;
  border: 0;
  font-size: 100%;
  font: inherit;
  vertical-align: baseline;
}
/* HTML5 display-role reset for older browsers */
article, aside, details, figcaption, figure,
footer, header, hgroup, menu, nav, section {
  display: block;
}
body {
  line-height: 1;
}
ol, ul {
  list-style: none;
}
blockquote, q {
  quotes: none;
}
blockquote:before, blockquote:after,
q:before, q:after {
  content: '';
  content: none;
}
table {
  border-collapse: collapse;
  border-spacing: 0;
}
html, body {
  width: 100%;
  height: 100%;
  overflow: auto;
  margin: 0;
  scroll-behavior: smooth;
  -webkit-overflow-scrolling: touch;
}
```

在 `global.scss` 中引入：

```scss
@import "./reset.scss";
```

4.定义通用样式

创建 `_common.scss`，用于定义通用样式，以及使用 `@mixin` 定义可复用样式，然后在 `global.scss` 中引入和局部引入。例如：

```scss
// 布局
@mixin flex-center {
    display: flex;
    justify-content: center;
}
@mixin flex-start-center {
    display: flex;
    justify-content: flex-start;
    align-items: center;
}
@mixin flex-center-center {
    display: flex;
    justify-content: center;
    align-items: center;
}
@mixin flex-between-center {
    display: flex;
    justify-content: space-between;
    align-items: center;
}
@mixin flex-column-start-center {
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;
}
@mixin flex-column-center-center {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

// 其他通用样式
body {
    font-size: 16px;
}
.p {
    text-align: justify;
    line-height: 1.67;
}
```

5.定义通用主体色（如果需要）

如果不同页面使用到统一的颜色，可以考虑定义复用主题色，创建 `_theme.scss`，例如：

```css
$dark: #1e1e1e;
$red: #ff2f47;
$orange: #fd5133;
$green: #15c288;
$white: #fff;
$bg-color: #ff6743;
```