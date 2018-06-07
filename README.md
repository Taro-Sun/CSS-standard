# CSS 规范

## 分类
### CSS文件的分类和引用顺序

按照CSS的性质和用途，将CSS文件分成“公共型样式”、“特殊型样式”、“皮肤型样式”，并以此顺序引用（按需求决定是否添加版本号）。

  1. 公共型样式：包括了以下几个部分：“标签的重置和设置默认值”、“统一调用背景图和清除浮动或其他需统一处理的长样式”、“网站通用布局”、“通用模块和其扩展”、“元件和其扩展”、“功能类样式”、“皮肤类样式”。
  2. 特殊型样式：当某个栏目或页面的样式与网站整体差异较大或者维护率较高时，可以独立引用一个样式：“特殊的布局、模块和元件及扩展”、“特殊的功能、颜色和背景”，也可以是某个大型控件或模块的独立样式。
  3. 皮肤型样式：如果需要这类需求，需要将颜色、背景抽离出来

### CSS内部的分类及其顺序

  1. 重置(reset)和默认(base)(tags)：消除默认样式和浏览器差异，并设置部分标签的初始样式，以减少后面的重复劳动
  2. 布局(grid)(.g-)：将页面分割为几个大块，通常有头部、主体、主栏、侧栏、尾部等
  3. 模块(module)(.m-)：通常是一个语义化的可以重复使用的较大的整体！比如导航、登录、注册、各种列表、评论、搜索等
  4. 元件(unit)(.u-)：通常是一个不可再分的较为小巧的个体，通常被重复用于各种模块中！比如按钮、输入框、loading、图标等
  5. 功能(function)(.f-)：为方便一些常用样式的使用，将这些使用率较高的样式剥离出来，按需使用，通常这些选择器具有固定样式表现，比如清除浮动等，不可滥用
  6. 皮肤(skin)(.s-)：如果你需要把皮肤型的样式抽离出来，通常为文字色、背景色（图）、边框色等，非换肤型网站通常只提取文字色。非换肤型网站不可滥用此类
  7. 状态(.z-)：为状态类样式加入前缀，统一标识，方便识别，她只能组合使用或作为后代出现(.u-ipt.z-dis{}，.m-list li.z-sel{})

## 命名规则

### 分类的命名方法：使用单个字母+"-"为前缀

``` css
/* 布局 */
.g-sd {
  float: left;
  width: 300px;
}
/* 模块 */
.m-logo {
  width: 200px;
  height: 50px;
}
/* 元件 */
.u-btn {
  height: 20px;
  border: 1px solid #333;
}
/* 功能 */
.f-tac {
  text-align: center;
}
/* 皮肤 */
.s-fc,a.s-fc:hover {
  color: #fff;
}
```

## 代码格式

### 空格

#### **选择器** 与 **{** 之间必须包含空格。
 ----

``` css
.selector {
}
```

#### **属性名** 与之后的 **:** 之间不允许包含空格， **:** 与 **属性值** 之间必须包含空格。
----
> 
``` css
.selector {
  margin: 0;
}
```

#### 当一个 css样式 包含多个 选择器 时，每个选择器声明必须独占一行。
---
``` css
.post,
.page,
.comment {
  line-height: 1.5;
}

```
#### **>** 、 **+ **、 **~**  选择器的两边各保留一个空格。
---

``` css 
main > nav {
  padding: 10px;
}

label + input {
  margin-left: 5px;
}

input:checked ~ button {
  background-color: #69C;
}

```

### 省略值为0时的单位

为节省不必要的字节同时也使阅读方便，我们将0px、0em、0%等值缩写为0。
如果是0开始的小数，前面的0可以省略不写

``` css
.m-box {
  margin: 0 10px;
  background-position: 50% 0;
}
body {
  opacity: .6;
  text-shadow: 1px 1px 5px rgba(0, 0, 0, .5);
}
```

### 私有在前，标准在后

先写带有浏览器私有标志的，后写W3C标准的。

---

> 带私有前缀的属性由长到短排列，按冒号位置对齐。
> 
> 标准属性放在最后，按冒号对齐方便阅读，也便于在编辑器内进行多行编辑。

``` css
.m-box {
  -webkit-box-shadow: 0 0 0 #000;
     -moz-box-shadow: 0 0 0 #000;
          box-shadow: 0 0 0 #000;
}
```


### 使用单引号

省略url引用中的引号，其他需要引号的地方使用单引号。

``` css
.m-box {
  background: url(bg.png);
}
.m-box:after {
  content: '.';
}
```

### 使用16进制表示颜色值

除非你需要透明度而使用rgba，否则都使用#f0f0f0这样的表示方法，并尽量缩写。

``` css
 .m-box {
   color: #f00;
   background: rgba(0,0,0,0.5);
}
```

### 根据属性的重要性按顺序书写
先显示定位布局类属性，后盒模型等自身属性，最后是文本类及修饰类属性。

| 显示属性     | 自身属性   |  文本属性和其他修饰类属性  |
| :--------:  | :-------:  | :--------------: |
| display     | width      |  font            |
| visibility  | height     |  text-align      |
| position    | margin     |  text-decoration |
| float       | padding    |  vertical-align  |
| clear       | border     |  white-space     |
| list-style  | overflow   |  color           |
| top         | min-width  |  background      |

``` css
.m-box {
  position: relative;
  width: 600px;
  margin: 0 auto 10px;
  text-align: center;
  color: #000;
}
```
如果属性间存在关联性，则不要隔开写。
``` css
/* 这里的height和line-height有关联性 */
.m-box {
  position: relative;
  height: 20px;
  line-height: 20px;
  padding: 5px;
  color: #000;
}
```

### 选择器顺序
  * 从大到小（以选择器的范围为准）
    ``` css
     /* 从大到小 */
     .m-list p {
       margin: 0;
       padding: 0;
      }
     .m-list p.part {
       margin: 1px;
       padding: 1px;
      }
    ```
  * 从低到高（以等级上的高低为准）
    ``` css
     /* 从低到高 */
     .m-logo a {
       color: #f00;
      }
     .m-logo a:hover {
       color:#fff;
      }
    ```
  * 从先到后（以结构上的先后为准）
    ``` css
     /* 从先到后 */
     .g-hd {
       height:60px;
      }
     .g-bd {
       height:60px;
      }
     .g-ft {
       height:60px;
      }
    ```
  * 从父到子（以结构上的嵌套为准）
    ``` css
     .m-list {
       width: 300px;
      }
     .m-list .itm {
       float: left;
      }
    ```

## 最佳实践

### 统一语义理解和命名

  * 布局(.g-)

      | 语义 | 命名 | 简写 |
      | :--: | :--: | :--: |
      | 文档 | doc | doc |
      | 头部 | head | hd | 
      | 主体 | body | bd |
      | 尾部 | foot | ft |
      | 主栏 | main | mn |
      | 主栏子容器 | mainc | mnc |
      | 侧栏 | side | sd |
      | 侧栏子容器 | sidec | sdc |
      | 合容器 | wrap/box | wrap/box |

  * 模块(.m-)、元件(.u-)

      | 语义 | 命名 | 简写 |
      | :--: | :--: | :--: |
      | 导航 | nav | nav |
      | 子导航 | subnav | snav | 
      | 面包屑 | crumb | crm |
      | 菜单 | menu | menu |
      | 选项卡 | tab | tab |
      | 标题区 | head/title | hd/tt |
      | 内容区 | body/content | bd/ct |
      | 列表 | list | lst |
      | 表格	 | table | tb |
      | 表单 | form | fm |
      | 热点 | hot | hot |
      | 排行 | top | top |
      | 登录 | login | log |
      | 标志 | logo | logo |
      | 广告 | advertise | ad |
      | 搜索 | search | sch |
      | 幻灯 | slide | sld |
      | 提示 | tips | tips |
      | 帮助 | help | help | 
      | 新闻 | news | news |
      | 下载 | download | dld |
      | 注册 | regist | reg |
      | 投票 | vote | vote |
      | 版权 | copyright | cprt |
      | 结果 | result | rst |
      | 标题 | title | tt |
      | 输入 | input | ipt |
  
  * 功能(.f-)
  
      | 语义 | 命名 | 简写 |
      | :--: | :--: | :--: |
      | 浮动清除 | clearboth | cb |
      | 向左浮动 | floatleft | fl | 
      | 向右浮动 | floatright | fr |
      | 内联块级 | inlineblock | ib |
      | 文本居中 | textaligncenter | tac |
      | 文本居右 | textalignright | tar |
      | 文本居左 | textalignleft | tal |
      | 垂直居中 | 垂直居中	 | vam |
      | 溢出隐藏 | overflowhidden | oh |
      | 完全消失 | displaynone | dn |
      | 字体大小 | fontsize | fs | 
      | 字体粗细 | fontweight | fw |
  
  * 皮肤(.s-)
  
      | 语义 | 命名 | 简写 |
      | :--: | :--: | :--: |
      | 字体颜色 | fontcolor | fc |
      | 背景 | background | bg | 
      | 背景颜色 | backgroundcolor | bgc |
      | 背景图片 | 背景图片 | bgi |
      | 背景定位 | backgroundposition | bgp |
      | 边框颜色 | bordercolor | bdc |

  * 状态(.z-)

      | 语义 | 命名 | 简写 |
      | :--: | :--: | :--: |
      | 选中 | selected | sel |
      | 当前 | current | crt | 
      | 显示 | show | show |
      | 隐藏 | hide | hide |
      | 打开 | open | open |
      | 关闭 | close | close |
      | 出错 | error | err |
      | 不可用 | disabled | dis |


参考资料

  [网易NEC](http://nec.netease.com/standard)
  
  [百度FEX编码规范](https://github.com/fex-team/styleguide/blob/master/css.md)
