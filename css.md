## 一、基础知识
### 1、css单位
（1）px<br>
（2）%
  
    width、height、font-size的百分比是相对于父元素“相同属性”的值计算
    line-height的百分比相对于当前元素的font-size值来计算的
    vertical-align的百分比相对于当前元素的lin-height值决定的
（3）em：1em= `“当前元素”的font-size值` <br>
若当前元素的font-size值没有定义，则当前元素会继承父元素的font-size；若所有祖先元素都没有定义font-size，则当前元素继承浏览器默认的font-size（16px）
  
    使用技巧：
    1、首行缩进使用 text-indent: 2em
    2、使用em作为统一单位
    html{ font-size: 62.5% } //设置html标签的元素字体大小为 62.5% * 16px = 10px
    这时1em = 10px
（4）rem：相对于根元素（html元素）的字体大小。`rem布局是移动端最常见的布局方式之一`
### 2、css特性：继承性、层叠性
（1）继承性：子元素继承父元素的某些样式属性

    文本相关属性：font...、line-height、text-align、text-indent、word-spacing
    列表相关属性：list-style-image、list-style-position、list-style-type、list-style
    颜色相关属性：color
注：a元素本身有默认的颜色样式，优先级比继承的颜色要高。若想a元素也能继承父元素的颜色，可在a元素中使用" color: inherit; " <br>
（2）层叠性 ：样式的覆盖。对一个元素，若重复定义了多个相同的属性，`且这些样式具有相同的权重时`，css会以最后定义的属性值为准。（“后来者居上原则”）<br>
即要满足：`元素相同、属性相同、权重相同`
### 3、css优先级
css：层叠样式表，层叠指的就是样式的覆盖。当样式的覆盖发生冲突时，以优先级高的为准

    常见的五种样式冲突：
    1、引用方式冲突  行内样式 > (内部样式 = 外部样式) 
    若内部样式与外部样式同时存在，则以最后引用的样式为准（“后来者居上原则”）
    2、继承方式冲突  “最近的祖先元素”获胜
    3、指定样式冲突  当直接指定"当前元素"的样式发生冲突时， 样式权重高的获胜
       行内样式 > id选择器 > class选择器 > 元素选择器 
       class选择器优先级 = 属性选择器 = 伪类（如：hover、:first-child）
       元素选择器优先级 = 伪元素（::before、::after、::first-letter、::first-line）
    4、继承样式和指定样式冲突  指定样式获胜
    5、!important 优先级最高
    如何覆盖!important：使用相同的选择器，再添加一条!important的css语句，但这条语句得放在后面（“后来者居上”）
                        使用优先级更高的选择器，再添加一条!important的css语句
### 4、css的引用方式
外部样式表多用于公有样式，内部样式表多用于私有样式，行内样式表多用于小修改或者优先级方面
### 5、css的层次选择器
    M N  后代选择器，选择M元素内部后代的N元素（所有N元素）   
    M>N  子代选择器，选择M元素内部子代的N元素（所有第一级N元素）
    M~N  兄弟选择器，选择M元素后“所有”的同级N元素
    M+N  相邻选择器，选择M元素相邻的“下一个”同级N元素
    :first-letter  选中元素内容中的“第一个字”或“第一个字母”
    :first-line  选中元素内容中的“第一行文字”
## 二、css规范
### 1、命名规范
文件名：reset.css用于去除元素的默认样式，使得所有浏览器页面的外观保持统一 <br>
id和class名：推荐用中划线，其中为避免class命名的重复，命名时一般取父元素的class名作为前缀       
注：reset.css必须在其他css代码前引入
## 三、盒子模型
margin外边距 - border边框 - padding内边距 - content内容区
### 1、内容区
有width、height、overflow3个属性<br>
width和height是针对内容区而言，不包括padding；当内容区信息太多超出内容区所占范围时，可使用overflow溢出属性来指定处理方法（eg：overflow-y: scroll; overflow: hidden）
### 2、内边距
padding: 上 右 下 左
### 3、外边距
#### （1）外边距叠加
当两个`垂直外边距` `相遇`时，这两个外边距将会合并为一个。叠加后的高度为叠加前两个外边距中的最大值

    1、同级元素：垂直外边距相遇时叠加
    2、父子元素：当一个元素包含在另一个元素中，父元素没有padding或border把子元素的外边距隔开，父子元素的相邻上下外边距发生合并
注：外边距叠加针对的是block和inline-block元素    
#### （2）负margin技术 
当元素的margin-top或者margin-left为负数时，“当前元素”会被拉出去，然后覆盖“其他元素”
当元素的margin-bottom或者margin-right为负数时，“后续元素”会被拉进，然后覆盖“当前元素”<br>

    使用技巧：
    1、图片与文本对齐
       vertical-align: text-bottom
       设置图片 margin: 0 3px -3px 0
    2、自适应两列布局
       假设左边列的宽度固定，右边列的宽度自适应
       固定的那一列：width: 100%; margin-right: -200px
       自适应的那一列：width:200px
    3、元素水平垂直居中（block、inline、inline-block都能用此方法）
       父元素{
          position: relative
       }
       子元素{
          position: absolute
          top: 50%
          left: 50%   //先把子元素的左上角定位到父元素的中心
          margin-top: height值一半的负值
          margin-left: width值一半的负值
       }       
### 4、边框
border: 1px solid red
### 5、overflow：定义`内容区`中内容溢出元素边框时发生的事情
visible、hidden、scroll、auto <br>
overflow: hidden 隐藏内容，以免影响布局；清除浮动
## 四、display属性
### 1、 block 块元素
eg: h1~h6,p,div,hr,ul<br>
块元素独占一行，排斥其他元素（block、inline等）与其位于同一行<br>
块元素内部可以容纳其他块元素和行内元素
### 2、inline 行内元素
eg: a,span <br>
行内元素可以与其他行内元素位于同一行 <br>
行内元素内部可以容纳其他`行内元素`，但不能容纳块元素 <br>
无法定义height和width <br>
可以定义margin-left和margin-right，无法定义margin-top和margin-bottom
### 3、inline-block 行内块元素
eg: img,input <br>
可以定义height和width <br>
可以与其他`行内元素`位于同一行（这时行内元素之间有间距）<br>
要为span、a等行内元素定义一定的width和height时，就可通过display: inline-block实现
### 4、table-cell：让元素以表格单元格的形式呈现
### 5、去除inline-block元素间距
为父元素定义 font-size:0
## 五、文本效果
### 1、text-align: center 水平居中
    text-align元素对inline元素、inline-block元素有效，对block元素无效
    text-align: center 与margin: 0 auto ：
    text-align:center 实现的是文字、inline元素和inline-block元素的水平居中；在父元素中定义（这样其除block外的子元素都水平居中了）
    margin: 0 auto 实现的是block元素的水平居中；在当前元素中定义（当前元素一定要定义width值）    
### 2、line-height
当line-height与height值相同时，实现单行文字的垂直居中<br>
当line-height取值为百分比或em值时，元素的行高是相对于`当前元素`的font-size值<br>
line-height值的继承：子元素会继承父元素line-height属性的像素(px)值，而非百分比
### 3、vertical-align
用于定义`周围的`文字、inline元素、inline-block元素相对于该元素基线的垂直对齐方式（“该元素”指被定义了vertical-align属性的元素） <br>
vertical-align元素对inline元素、inline-block元素有效，对block元素无效 <br>
vertical-align属性取值：负值、百分比和关键字<br>
#### （1）负值
如：vertical-align: -2px表示元素相对于基线`向上`偏移2px
#### （2）百分比：相对于`当前元素`所继承的line-height属性值
如：vertical-align: 50%; line-height: 20px; 则相当于vertical-align:10px，表示元素相对于基线向下偏移10px
#### （3）关键词：top、middle、baseline、bottom
应用：如单选框或复选框与文字垂直居中对齐
## 六、表单效果
### 1、textarea
    1、固定大小：min-width、max-width
    2、禁止拖动：resize: none
## 七、浮动布局
脱离文档流的方法：浮动、定位
### 1、浮动的特点
（1）浮动元素变成block类型，故可以定义width、height、padding、margin <br>
（2）该元素脱离文档流后，后面的元素会紧跟着填上空缺的位置
### 2、浮动的影响
（1）对自身：变成block元素 <br>
（2）对父元素：若浮动元素的height大于父元素的height，或者父元素没有定义高度height，此时浮动元素会脱离父元素，即“父元素高度塌陷” <br>
（若父元素没设置高度但设置了宽度，塌陷后的父元素将变成一条线）<br>
（3）对子元素：如果一个元素是浮动元素（没有定义height），并且它的子元素也是浮动元素，则这个浮动元素会自适应地包含该子元素
### 3、浮动的副作用
（1）父元素高度塌陷，边框不能撑开 <br>
（2）页面布局错乱
### 4、清除浮动：不想浮动元素后面的元素环绕着它，希望后面的元素回归到正常的文档流
    三种方法：
    clear:both 
    overflow:hidden（应用于浮动元素的父元素）
    ::after伪元素
## 八、定位布局
1、元素只有在定义了position属性（除static）之后，top、left、bottom、right才生效。（通常使用两个就够了）<br>
2、position: absolute 会将元素转换为block元素 <br>
3、子元素相对父元素定位 <br>
父元素定义position: relative，子元素定义position: absolute，再配合top、left等实现定位 <br>
4、z-index属性：设置元素的堆叠顺序 <br>
数值越大，越外层；若z-index值相同，遵循“后来者居上”原则来叠加
## 九、css图形
### 1、圆角半径 border-radius
    一个值：四个角都一样
    两个值：左上、右下
    三个值：左上、右上左下、右下 
    四个值：左上、右上、右下、左下 （顺时针）
半圆：height=width的一半，右下角和左下角的圆角半径为0 <br>
圆：4个角的圆角半径为宽度（或高度）的一半
## 十、css性能优化
### 1、属性简写
border: 1px solid red <br>
background: url(...) no-repeat 80px 40px （后两个为背景的位置）
## 十一、css技巧
### 1、水平居中
    text-align: center 与margin: 0 auto ：
    text-align:center 实现的是文字、inline元素和inline-block元素的水平居中；在父元素中定义（这样其除block外的子元素都水平居中了）
    margin: 0 auto 实现的是block元素的水平居中；在当前元素中定义（当前元素一定要定义width值）  
### 2、垂直居中
    inline-height与height值相同：单行文本
    
    万能方法：
    父元素{
       position: relative
    }
    子元素{
       position: absolute
       top: 50%
       left: 50%   //先把子元素的左上角定位到父元素的中心
       margin-top: height值一半的负值
       margin-left: width值一半的负值
    }          
### 3、iconfont技术
    （1）下载好图标字体文件（.eto .woff .ttf .svg）并放入网站目录中
    （2）在css中使用@font-face自定义字体
    （3）在HTML中，元素添加class="iconfont"
    （4）在元素中添加图标对应的字符串

