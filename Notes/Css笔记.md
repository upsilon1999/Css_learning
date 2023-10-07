# Css复习

```sh
windows上的 徽标键 + v 可以选择剪切版的内容复制
```



## CSS简介

```sh
样式层叠表
样式： 文字大小、背景颜色、元素宽高等等
层叠： 一层一层"涂"上去
表：操作列表
```

>表

```css
height:80px;
width:80px;
color:red;
```

## CSS的编写位置

### 行内样式/内联样式

```html
<!-- 在html标签身上有一个style属性，专门用于写行内样式 -->
<!-- style属性可以理解为一个CSS对象，里面以键值对的形式书写内容 -->
<!-- CSS不区分大小写，
        1. color:red; <=> COLOR:RED;
        2. font-Size:20px; <=> font-size:20px;
        只要键名存在就可以写
-->
<h1 style="color:blue;font-size: large;">欢迎学习CSS</h1>
```

```sh
1.写在html标签的style属性值中
2. css对象不区分大小写

缺点：
不好复用
写多了难看
```

```sh
作用范围：当前标签
```



### 内部样式

```html
<style>
    /*
        style标签可以放在head或body内部，和其他html标签一样
        如果我们位置乱写，浏览器在解析的时候会吧style标签解析到head里
        内部样式即在html内部使用style标签包裹的样式，写法

        标识符 {
            css对象
        }
    */
    h1{
        color:aqua;
    }
</style>
```

```sh
顾名思意：写在了html内部
```

>与内联样式相比的优势

```sh
1.结构更加清晰
2.同一个html中可以轻松复用
```

>问题

```sh
1.并没有实现结构和样式的完全分离
2.多个html不能复用
```

### 外部样式

`html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
	
	<title>位置3_外部样式</title>
	<!-- 
		rel <==> relation 关系的意思，要引入的文档与当前文档的关系 
		stylesheet 代表要引入的文件和当前文件是样式的关系

		href 引入的文档来自于哪里
	-->
	<link rel="stylesheet" href="./wrap.css">
</head>
<body>
	<h1>欢迎学习CSS</h1>
</body>
</html>
```

`wrap.css`

```css
h1{
	color:blue;
}
```

>小结

```sh
顾名思意：
就是将样式写在html外面，然后引入
```

>优势

```sh
1.实现了结构与样式的分离，
2.实现了多个html的复用
3.会触发浏览器的缓存机制，多个html读取一个外部css，浏览器只读一次，后续都从缓存里面拿
```

## CSS样式表的优先级

### 行内&内部

`html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>样式表的优先级别</title>
	<style>
		h1{
			color:red;
		}
	</style>
</head>
<body>
	<h1 style="color:blue;">欢迎前来学习CSS</h1>
</body>
</html>
```

>结论

```sh
当有样式冲突时
优先级： 行内样式 > 内部样式
```

### 行内&外部

`wrap.css`

```css
h1{
    font-size:20px;
}
```

`html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>样式表的优先级别</title>
	<style>
		h1{
			color:red;
		}
	</style>
	<link rel="stylesheet" href="./wrap.css">
</head>
<body>
	<h1 style="color:blue;font-size: 200px;">欢迎前来学习CSS</h1>
</body>
</html>
```

>结论

```sh
当有样式冲突时
优先级： 行内样式 > 外部样式
```

### 内部&外部

`wrap.css`

```css
h1{
    font-size:20px;
},
h2{
    color:red;
}
```

`html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>样式表的优先级别</title>
	<style>
		h1{
			color:red;
		}
		h2{
			color: blue;
		}
	</style>
	<link rel="stylesheet" href="./wrap.css">
</head>
<body>
	<h1 style="color:blue;font-size: 200px;">欢迎前来学习CSS</h1>
	<h2>测试内外优先级</h2>
</body>
</html>
```

`html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>样式表的优先级别</title>
    <link rel="stylesheet" href="./wrap.css">
	<style>
		h1{
			color:red;
		}
		h2{
			color: blue;
		}
	</style>
</head>
<body>
	<h1 style="color:blue;font-size: 200px;">欢迎前来学习CSS</h1>
	<h2>测试内外优先级</h2>
</body>
</html>
```

>结论

```sh
我们会发现，内部样式和外部样式优先级一样，谁后导入就听谁的
```

### 结论

`html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>样式表的优先级别</title>
	<style>
		/* 
			样式优先级别结论
			行内样式  > 内部样式 = 外部样式
		*/
		h1{
			color:red;
		}
		h2{
			color: blue;
		}
	</style>
	<link rel="stylesheet" href="./wrap.css">
</head>
<body>
	<h1 style="color:blue;font-size: 200px;">欢迎前来学习CSS</h1>
	<h2>测试内外优先级</h2>
</body>
</html>
```

>结论

```sh
行内样式 > 内部样式 = 外部样式
1.内部样式、外部样式，这二者的优先级相同，且：后面的会覆盖前面的（简记："后来者居上"）
2.同一个样式表中，优先级也和编写顺序有关，且：后面的会覆盖前面的 简记："后来者居上"）
```

1.

```css
h1{
    color:red;
    color:blue;
}
```

后来者居上，蓝色生效。

2.

```css
h1{
    color:red;
    color:blue;
}
h1{
    color:yellow;
}
```

后来者居上，黄色生效。

## CSS的语法规范

### 基本结构

`html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>语法规范</title>
	<style>
		h1{
			color:green;
			font-size: 100px;
		}
	</style>
</head>
<body>
	<h1>学习css语法规范</h1>
</body>
</html>
```

下面就来分析css的结构

```css
选择器 { 声明1 ; 声明 2;}
```

```css
h1{ color:green;font-size:100px;}

选择器  h1
声明块   { color:green;font-size:100px;} 
声明    color:green;
```

>小结

```sh
一个声明就是一个样式，一堆声明组成一个声明块，声明块就是一堆具体的样式
```

```sh
声明是	'属性名:属性值' 的形式
```

>通过mdn了解

```sh
Mdn -- references -- css -- Selectors(选择器)
Mdn -- references -- css -- Properties(属性名)
```

### 注释

和js的多行注释一样

```css
/*这里是注释*/
h1{
    /*这里是注释*/
    color:red;
    font-size:100px
}
```



### 书写规范

>最后一组声明后的分号可省略

```css
h1{
    color:red;
    font-size:100px
}
```

但是推荐不省略

>选择器和声明块之前推荐有空格

```css
h1 {
    color:red;
}
```

可以没有，但是推荐有

>声明的属性名的冒号推荐与属性值之间也保有空格

```css
h1 {
    color: red;
}
```

可以没有，但是推荐有

>注释推荐左右加空格

```css
/* 这里是注释 */
h1{
    /* 这里是注释 */
    color:red;
    font-size:100px
}
```

>不区分大小写

```css
h1 {
    color: red;
}
```

```css
h1 {
    Color: rEd;
}
```

```css
h1 {
    COLOR: RED;
}
```

三者是一样的，推荐使用小写

## CSS的代码风格

```css
/* 
    展开风格
    开发时推荐，便于维护和调试
*/
h1 {
    color: red;
}
/* 
    紧凑风格
    项目上线时推荐，可以减少文件体积
*/
h1{font-size:100px;}
```

>总结

```sh
项目上线时，我们会通过工具将"展开风格"的代码，变成"紧凑风格"，这样可以减少文件体积，节约网络流量，同时也能让用户打开网页时候速度更快。
```

## CSS基本选择器

```sh
基本选择器包括:
1.通配选择器
2.元素选择器
3.类选择器
4.id选择器
```

### 通配选择器

* 作用：可以选中所有的html元素

* 语法：

  ```css
  * {
      属性名 ：属性值
  }
  ```

* 举例

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
  	<meta charset="UTF-8">
  	<meta http-equiv="X-UA-Compatible" content="IE=edge">
  	<meta name="viewport" content="width=device-width, initial-scale=1.0">
  	<title>通配选择器</title>
  	<style>
  		/* 
  			通配选择器 *
  			作用： 可以选中所有的HTML元素
  
  			主要场景：清除样式时作用巨大
  		*/
  		* {
  			color: red;
  			font-size: 10px;
  		}
  	</style>
  </head>
  <body>
  		<h1>我是标题</h1>
  		<p>我是段落</p>
  </body>
  </html>
  ```

  ```css
  /* 
      通配选择器 *
      作用： 可以选中所有的HTML元素
  
      主要场景：清除样式时作用巨大
  */
  * {
      color: red;
      font-size: 10px;
  }
  ```

  >小结

  ```sh
  所有HTML标签
  那么 html、head、body、meta、h1、h2等等全都生效
  ```

### 元素选择器

* 作用：为页面中**某种元素**统一设置样式

* 语法：

  ```css
  标签名 {
      属性名: 属性值;
  }
  ```

* 举例

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
  	<meta charset="UTF-8">
  	<meta http-equiv="X-UA-Compatible" content="IE=edge">
  	<meta name="viewport" content="width=device-width, initial-scale=1.0">
  	<title>元素选择器</title>
  	<style>
  		/*
  			元素选择器
  			会把页面上所有的同名元素赋予相同的样式，不能实现差异化
  
  			作用：为页面中 某种元素 统一设置样式
  
  			语法：
  			标签名 {
  				属性名：属性值;
  			}
  		*/
  		h1{
  			color: chocolate;
  		}
  		p {
  			color:green;
  		}
  	</style>
  </head>
  <body>
  	<h1>我是标题</h1>
  	<p>我是段落</p>
  	<p>我是第二个段落</p>
  </body>
  </html>
  ```

  ```css
  /*
      元素选择器
      会把页面上所有的同名元素赋予相同的样式，不能实现差异化
  
      作用：为页面中 某种元素 统一设置样式
  
      语法：
      标签名 {
          属性名：属性值;
      }
  */
  h1{
      color: chocolate;
  }
  p {
      color:green;
  }
  ```

* 备注：元素选择器无法单独实现**差异化设置**，例如在上面代码中，所有p元素效果都一样

### 类选择器

* 作用：根据元素的class值，来选中某些元素。

  ```sh
  class 有类别种类的意思，所以class的值，又称：类名
  ```

* 语法

  ```css
  .类名 {
      属性值: 属性名;
  }
  ```

* 举例

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
  	<meta charset="UTF-8">
  	<meta http-equiv="X-UA-Compatible" content="IE=edge">
  	<meta name="viewport" content="width=device-width, initial-scale=1.0">
  	<title>类选择器</title>
  	<style>
  		/* 
  			class属性，本身就有分类的意思
  			其值我们常常成为类名
  
  			要把类名和元素名做区分，在类名前面加".",
  			如果不加会被解析器认为是元素选择器，去寻找标签
  		*/
  		.one{
  			color:aqua;
  		}
  		.two{
  			color: brown;
  		}
  		.big{
  			font-size: 20px;
  		}
  		/* 
  			注意事项：
  			1.类对页面中所有具有该类名的标签生效
  			2.一个标签只能写一个class属性，因为按照html标签的特性，后写的同名属性无效
  			3.要给一个标签写多个类，可以在class的属性值中以空格隔开
  
  			class值的规则：
  			1.不能是纯数字
  			2.不能使用中文
  			3.多个单词以短杠连接
  		
  		*/
  	</style>
  </head>
  <body>
  	<h1>我是标题</h1>
  	<!-- 1.类对页面中所有具有该类名的标签生效 -->
  	<p class="one">我是段落</p>
  	<span class="one"></span>
  	<p class="two">我是第二个段落</p>
  
  	<!-- 2.一个标签只能写一个class属性，因为按照html标签的特性，后写的同名属性无效 -->
  	<p class="one" class="two"></p>
  
  	<!-- 3.要给一个标签写多个类，可以在class的属性值中以空格隔开 -->
  	<p class="one big"></p>
  </body>
  </html>
  ```

* 注意点

  * 元素的`class`属性值不带`.`，但`CSS`类选择器要带`.`。

  * `class`值是我们自定义的,按照标准：

    ```sh
    1.不要使用纯数字--也推荐数字开头
    2.不要使用中文
    3.尽量使用英文和数字的组合，若多个单词组成，使用"-"做连接，例如："left-menu"，也可以使用下划线，甚至陀峰，短杆只是一个规范
    ```

  * 一个元素不能写多个class属性

    ```html
    <!-- 2.一个标签只能写一个class属性，因为按照html标签的特性，后写的同名属性无效 -->
    	<p class="one" class="two"></p>
    ```

  * 一个元素的class属性，能写多个值，要用空格隔开

    ```html
    <!-- 3.要给一个标签写多个类，可以在class的属性值中以空格隔开 -->
    	<p class="one big"></p>
    ```

  * 如果一个元素的class属性有多个值，且值中样式有冲突，后来者居上,这里的后来者是根据样式表

    ```html
    <style>
        .one{
            font-size:10px;
        }
        .big{
            font-size:20px;
        }
    </style>
    <p class="big one"></p>
    ```

    由于样式表中后来者居上，所以最终样式为

    ```css
    {
        font-size:20px;
    }
    ```

    即与我们在class属性中所写样式顺序无关，根据样式表里面的顺序

### id选择器

* 作用：根据元素的id属性值，来精准的选中某个元素

* 语法

  ```css
  #id值 {
      属性名: 属性值;
  }
  ```

* 举例

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
  	<meta charset="UTF-8">
  	<meta http-equiv="X-UA-Compatible" content="IE=edge">
  	<meta name="viewport" content="width=device-width, initial-scale=1.0">
  	<title>Document</title>
  	<style>
  		/* 
  			id选择器 #id名
  		*/
  		#earthy {
  			color:blue;
  		}
  		#two {
  			font-size: 100px;
  		}
  		/* 
  			注意事项：
  			1. css的id属性不能以数字开头
  			2. 多个元素的 id值不能重复，，重复了会影响一些我们想要的实现
  			3.一个元素不能有多个id值
  			4.一个元素可以同时拥有id和class，且class允许和id同名
  		
  		*/
  	</style>
  </head>
  <body>
  	<!-- 
  		任意html标签都可以加id属性 
  		不同元素的id值不能重复
  		
  		重复了并不会报错，只是样式就是同一个，js拿元素也是同一个，超链接跳转也是
  	-->
  	<h1 id="earthy">我是标题</h1>
  	<p id="two">我是段落</p>
  	<span></span>
  	<p>我是第二个段落</p>
  </body>
  </html>
  ```

* 注意

  * id属性值:尽量由字母、数字、下划线（_）、短杠（-）组成，最好以字母开头，不要包含空格、**区分大小写**。

  * 一个元素只能拥有一个id属性，多个元素的id属性值不能相同

    ```sh
    重复了并不会报错，只是样式就是同一个，js拿元素也是同一个，超链接跳转也是
    ```

  * 一个元素可以同时拥有id和class属性

## CSS复合选择器

简单来说就是组合的意思，对CSS的基本选择器进行组合，大致分为以下几类

```sh
1.交集选择器
2.并集选择器
3.后代选择器
4.子代选择器
5.兄弟选择器
6.属性选择器
7.伪类选择器
```

### 交集选择器

* 作用：选中同时符合多个条件的元素。

  ```sh
  交集有并且的含义(通俗理解：既...又... 的意思)，例如：p元素且类名为rich
  
  关键思维：and 且
  ```

* 语法：

  ```css
  选择器1选择器2...选择器n {}
  ```

* 举例

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
  	<meta charset="UTF-8">
  	<meta http-equiv="X-UA-Compatible" content="IE=edge">
  	<meta name="viewport" content="width=device-width, initial-scale=1.0">
  	<title>交集选择器</title>
  	<style>
  		.rich {
  			color: gold;
  		}
  		.beauty {
  			color: red;
  		}
  		/* 
  			p元素且类名为beauty
  
  			二者连在一起写
  		*/
  		/* 1.元素名写在类名之前 */
  		p.beauty{
  			color: aqua;
  		}
  
  		/* 条件可以写的很多,元素在最前面，后面的连着写就可以，class和id无序 */
  		p.rich#wc{
  			color: blueviolet;
  		}
  
  		/* 
  		可以没有元素选择器
  
  		类名包含rich和beauty的元素
  		*/
  		.rich.beauty{
  			color:orange;
  		}
  		/* 
  			注意事项：
  			1.元素名写在类名之前
  			2.条件可以写的很多,元素在最前面，后面的连着写就可以，class和id无序
  			3.一般交集选择器不拼接id，因为id唯一，既然有id了，就可以直接用，不需要交集选择器了
  			4.交集选择器至多有一个元素，即也可以没有元素
  
  			开发中 元素.类名 的使用较多
  		*/
  	</style>
  </head>
  <body>
  	<h2 class="rich">土豪</h2>
  	<h2 class="beauty">明星</h2>
  
  	<p class="beauty">
  		学习交集选择器
  	</p>
  	<p class="rich" id="wc">多条件交集选择器</p>
  	<p class="rich beauty">大土豪</p>
  </body>
  </html>
  ```

* 注意

  * 有标签名，标签名必须写在前面

  * id选择器，理论上可以作为交集的条件，但实际应用中几乎不用 -- 因为没有意义

  * 交集选择器中不可能出现两个元素选择器，因为一个元素，不可能既是p元素又是span元素

  * 用的最多的交集选择器是：元素选择器配合类名选择器

    ```css
    p.rich {
        
    }
    ```

### 并集选择器

* 作用：选中多个选择器对应的元素，又称：**分组选择器**

  ```sh
  所谓并集就是"或者"的含义（通俗理解：要么...要么...的意思）
  
  关键思维：or 或
  ```

* 语法：

  ```sh
  选择器1,选择器2,...,选择器n {}
  ```

  ```sh
  多个选择器通过","连接，此处","的含义就是：或
  ```

* 举例

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
  	<meta charset="UTF-8">
  	<meta http-equiv="X-UA-Compatible" content="IE=edge">
  	<meta name="viewport" content="width=device-width, initial-scale=1.0">
  	<title>并集选择器</title>
  	<style>
  		.rich {
  			color: gold;
  		}
  		.beauty {
  			color: red;
  		}
  		.pig{
  			color:green;
  		}
  		/* 
  			在原来三个选择器的基础上做扩展，这是他们三的并集
  
  			.rich 或 .beauty 或 .pig
  
  			中间的或我们改成','就可以了,最后一个选择器后面不能加逗号
  			一般为了美观，我们会竖着写
  
  			.rich,
  			.beauty,
  			.pig,
  			#sux {
  				font-size: large;
  				background-color: gray;
  				width: 160px;
  			}
  		*/
  		.rich,.beauty,.pig,#sux{
  			font-size: large;
  			background-color: gray;
  			width: 160px;
  		}
  		/* 
  			注意事项：
  			1.我们用逗号连接选择器表示或
  			2.最后一个选择器不加逗号，加了就会报错
  		*/
  	</style>
  </head>
  <body>
  	<h2 class="rich">土豪</h2>
  	<h2 class="beauty">明星</h2>
  	<p class="pig">猪</p>
  	<p id="sux">小羊肖恩</p>
  </body>
  </html>
  ```

* 注意

  * 并集选择器，我们一般竖着写
  * 任何形式的选择器都可以作为并集选择器的一部分
  * 并集选择器，通常用于集体声明，可以缩小样式表体积。

### HTML元素之间的关系

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>HTML元素之间的关系</title>
</head>
<body>
	<!-- 
		父元素 ：直接包裹某个元素的元素，就是该元素的父元素 
		例如：
		1.ul是四个li的父元素
		2.div是ul和h1的父元素
	-->
	<!-- 
		子元素 : 被父元素直接包含的元素(简记:儿子元素)
		例如:
		1.h1是div的子元素
		2.ul是div的子元素
		3.li是ul的子元素
	 -->
	 <!-- 
		祖先元素 : 父亲(的父亲...),一直往外找,都是祖先
		例如:
		1.div是li和span的祖先元素
		2.ul是UI的祖先元素
		备注:父元素,也算是祖先元素的一种,但是我们一般直接称父元素
	  -->
		<!-- 
			后代元素:儿子(的儿子...),一直往里面找,都是后代
			例如:
			1.span是ul的后代元素
			2.span与li都是div的后代元素
			备注:子元素,也算是后代元素的一种,但是我们一般直接称子元素
		 -->
		 <!-- 
			兄弟元素:具有相同父元素的元素,互为兄弟元素
			例如:
			1.ul和h1是兄弟元素
		  -->
	<div>
		<h1>学习使我快乐</h1>
		<ul>
			<li>前端</li>
			<li>后端</li>
			<li>大数据</li>
			<li>
				<span>UI</span>
			</li>
		</ul>
	</div>
</body>
</html>
```

>拆解

```html
<div>
    <h1>学习使我快乐</h1>
    <ul>
        <li>前端</li>
        <li>后端</li>
        <li>大数据</li>
        <li>
            <span>UI</span>
        </li>
    </ul>
</div>
```

* 父元素

  ```sh
  父元素 ：直接包裹某个元素的元素，就是该元素的父元素 
  例如：
  1.ul是四个li的父元素
  2.div是ul和h1的父元素
  ```

* 子元素

  ```sh
  子元素 : 被父元素直接包含的元素(简记:儿子元素)
  例如:
  1.h1是div的子元素
  2.ul是div的子元素
  3.li是ul的子元素
  ```

* 祖先元素

  ```sh
  祖先元素 : 父亲(的父亲...),一直往外找,都是祖先
  例如:
  1.div是li和span的祖先元素
  2.ul是UI的祖先元素
  备注:父元素,也算是祖先元素的一种,但是我们一般直接称父元素
  ```

* 后代元素

  ```sh
  后代元素:儿子(的儿子...),一直往里面找,都是后代
  例如:
  1.span是ul的后代元素
  2.span与li都是div的后代元素
  备注:子元素,也算是后代元素的一种,但是我们一般直接称子元素
  ```

* 兄弟元素

  ```sh
  兄弟元素:具有相同父元素的元素,互为兄弟元素
  例如:
  1.ul和h1是兄弟元素
  ```

### 后代选择器

* 作用:选中指定元素中,符合要求的后代元素.

* 语法:

  ```sh
  选择器1 选择器2 ... 选择器n {}
  ```

  先写祖先,再写后代

  ```sh
  选择器之间,用空格隔开,空格可以理解为:"xxx中的",其实就是后代的意思.
  选择器可以是任意选择器,例如之前的交集选择器,并集选择器都可以
  ```

* 举例

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
  	<meta charset="UTF-8">
  	<meta http-equiv="X-UA-Compatible" content="IE=edge">
  	<meta name="viewport" content="width=device-width, initial-scale=1.0">
  	<title>后代选择器</title>
  	<style>
  		/* 
  			ul 中的li
  
  			这样用空格隔开,就表示 ul中的所有后代li
  		*/
  		ul li {
  			color: red;
  		}
  		/* 
  			ol中的li中的a标签;
  		*/
  		ol li a {
  			color:blue;
  		}
  
  		/* 
  			类名为subject的元素里面的li
  		*/
  		.subject li {
  			color: aqua;
  		}
  
  		/* 
  				类名为subject的元素里面的li且类名为name
  		*/
  		.subject li.name{
  			color:gold;
  		}
  
  		/* 
  				类名为subject的元素里面的div且类名为name
  		*/
  		.subject div.name{
  			color:orange;
  		}
  	</style>
  </head>
  <body>
  	<ul>
  		<li>学习</li>
  		<li>炒币</li>
  		<li>研发</li>
  		<div>
  			<li>踢球</li>
  		</div>
  	</ul>
  	<ol>
  		<li>张三</li>
  		<li>李四</li>
  		<li>
  			<a href="#">王五</a>
  		</li>
  	</ol>
  
  	<ol class="subject">
  		<li class="name">张三</li>
  		<div class="name">我爱学习</div>
  		<li>李四</li>
  		<li>
  			<a href="#">王五</a>
  		</li>
  	</ol>
  </body>
  </html>
  ```

* 注意

  * 后代选择器,最终选择的是后代,不选中祖先

  * 儿子、孙子、重孙子都是后代

  * 结构一定要符合HTML嵌套要求，例如：p中不能嵌套h1～h6

    ```html
    <p>
    	<h1></h1>
    </p>
    ```

    最终会解析为

    ```html
    <p></p>
    <h1></h1>
    </p></p>
    ```

    所以写

    ```css
    p h1{}
    /*无效*/
    ```

### 子代选择器

* 作用：选中指定元素中，符合要求的子元素（儿子元素），先写父，再写子

  ```sh
  子代选择器又称：子元素选择器、子选择器
  ```

* 语法：选择器1>选择器2>...>选择器n {}

  ```sh
  选择器之间，用">"隔开，">"可以理解为:"xxx的子代"，其实就是儿子的意思。
  选择器可以是任意选择器
  ```

* 举例

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
  	<meta charset="UTF-8">
  	<meta http-equiv="X-UA-Compatible" content="IE=edge">
  	<meta name="viewport" content="width=device-width, initial-scale=1.0">
  	<title>子代选择器</title>
  	<style>
  		/* 
  			让div的子元素a标签变成红色
  		*/
  		div>a {
  			color:red;
  		}
  		/* 可以紧密的写，也可以中间加空格 */
  		p > a {
  			color: aqua;
  		}
  
  		.qi > a {
  			color: chocolate;
  		}
  	</style>
  </head>
  <body>
  	<div>
  		<a href="#">张三</a>
  		<a href="#">里斯</a>
  		<a href="#">王五</a>
  		<p>
  			<a href="#">赵六</a>
  		</p>
  		<div class="qi">
  			<a href="#">孙七</a>
  		</div>
  	</div>
  </body>
  </html>
  ```

* 注意

  * 子代选择器，最终选择的是子代，不是父级
  * 子、孙子、重孙子、...统称后代，子就是儿子。

### 兄弟选择器

```sh
兄弟选择器主要有两种：
相邻兄弟选择器 +
通用兄弟选择器 ~

特点：都选中的是"后面的兄弟元素"，前面的兄弟元素不受影响
```

* 相邻兄弟选择器

  * 作用：选中指定元素后面的紧挨着的满足条件的兄弟元素

    ```sh
    所谓相邻，就是紧挨着他的下一个
    1.紧挨着的下一个
    2.满足选取条件
    
    二者缺一不可
    ```

  * 语法：

    ```sh
    选择器1+选择器2+选择器3...{}
    ```

* 通用兄弟选择器

  * 作用：选中指定元素后面所有的满足条件的兄弟元素

  * 语法：

    ```sh
    选择器1~选择器2~选择器3...{}
    ```

* 举例

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
  	<meta charset="UTF-8">
  	<meta http-equiv="X-UA-Compatible" content="IE=edge">
  	<meta name="viewport" content="width=device-width, initial-scale=1.0">
  	<title>兄弟选择器</title>
  	<style>
  		/* 
  			+ 相邻兄弟选择器
  			紧紧相邻的后一位兄弟元素
  
  			这里div+p，找到与div紧紧相邻的后一位兄弟元素，且该兄弟元素需要为p元素
  		*/
  		div+p {
  			color:aqua;
  		}
  
  		/* 
  			找到与类test紧紧相邻的后一位兄弟元素，且该元素需要为p元素
  			由于 类test紧紧相邻的后一位兄弟元素为 h1,所以无效
  
  			注意顺序：
  			1.找到类test
  			2.找到后一位兄弟元素，判断是不是需要的元素
  		*/
  		.test+p {
  			color:brown;
  		}
  
  		/* 
  			~ 通用兄弟选择器
  			后面所有的兄弟元素
  
  		*/
  		h1~p {
  			color: blue;
  		}
  
  		/* 
  			效果：主页是黑色，其他几个li都变成了橙色
  			理解：
  			1.对于主页，li后紧紧相邻的li即秒杀，所以秒杀变色
  			2.对于秒杀，li后紧紧相邻的li即订单，所以订单变色
  			3.对于订单，li后紧紧相邻的li即我的，所以我的变色
  			4. 主页没有被选中，自然不会变色
  		*/
  		li+li{
  			color: orange;
  		}
  
  		/* 
  			效果：主页是黑色，其他几个li都变成了橙色
  			理解：
  			1.对于主页，li后的所有兄弟变色
  			2.对于秒杀等同理
  			2.主页没有被选中，自然不会变色
  		*/
  		li~li{
  			color:pink;
  		}
  	</style>
  </head>
  <body>
  	<p>人工智能</p>
  	<div>学习</div>
  	<p>前端</p>
  	<p>后端</p>
  	<p>大数据</p>
  	<p>UI</p>
  	<p class="test">测试</p>
  	<h1>活到老学到老</h1>
  	<p>自立更生</p>
  	<p>老当益壮</p>
  	<ul>
  		<li>主页</li>
  		<li>秒杀</li>
  		<li>订单</li>
  		<li>我的</li>
  	</ul>
  </body>
  </html>
  ```

* 注意点：

  ```sh
  兄弟选择器，选中的都是后面的兄弟元素
  ```

### 属性选择器

* 作用：选中属性值符合一定要求的元素。

* 语法：

  ```sh
  1.[属性名]
  选中具有某个属性的元素
  ```

  ```sh
  2.[属性名='值']
  选中包含某个属性，且属性值等于指定值的元素
  ```

  ```sh
  3.[属性名^='值']
  选中包含某个属性，且属性值以指定值开头的元素
  ```

  ```sh
  4.[属性名$='值']
  选中包含某个属性，且属性值以指定值结尾的元素
  ```

  ```sh
  5.[属性名*='值']
  选中包含某个属性，且属性值包含指定值的元素
  ```

  ```sh
  6.[属性名~='值']
  选中包含某个属性，属性值列表中含有指定的值的元素
  ```

  ```sh
  7.[属性名|='值']
  选中包含某个属性，属性值为指定值或者前缀为"值-"的元素
  ```

  ```sh
  8.[属性名 运算符 值 i]
  运算符任意，i或者I均可，表示后面的值不区分大小写，对type属性无效
  ```

  ```sh
  9.[属性名 运算符 值 s]
  运算符任意，s或者S均可，表示后面的值严格区分大小写
  ```

  

* 举例

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
  	<meta charset="UTF-8">
  	<meta http-equiv="X-UA-Compatible" content="IE=edge">
  	<meta name="viewport" content="width=device-width, initial-scale=1.0">
  	<title>属性选择器</title>
  	<style>
  		/* 
  			根据html标签的属性进行选取
  			注意，属性是可以自定义的，这就是以后项目开发中动态改变样式的原理
  		*/
  		/*	
  			语法1：[属性名]
  
  			例如：
  			选择页面中有title属性的所有元素
  		*/
  		[title] {
  			color:red;
  		}
  
  		/* 
  			语法2：[属性名 = 属性值]
  			元素不仅要有这个属性，属性的值还得满足要求
  
  			例如：
  			选中页面中有aaa属性且属性值为xxx的所有元素
  		*/
  		[abc="xxx"]{
  			color:blue;
  		}
  
  		/* 
  			语法3：[属性名 ^= 值]
  			元素不仅要有这个属性，属性的值还得以指定值开头
  
  			例如：
  			选中页面中有aoe属性且属性值以"b"开头的所有元素
  		*/
  		[aoe^='b']{
  			color:pink;
  		}
  		
  		/* 
  		语法4：[属性名 $= 值]
  		元素不仅要有这个属性，属性的值还得以指定值结尾
  
  		例如：
  		选中页面中有aoe属性且属性值以"jk"结尾的所有元素
  		*/
  		[aoe$='jk']{
  			color:blueviolet;
  		}
  
  		/* 
  		语法5：[属性名 *= 值]
  		元素不仅要有这个属性，属性的值还得包含指定值
  
  		例如：
  		选中页面中有aoe属性且属性值包含‘a’的所有元素
  		*/
  		[aoe*='a']{
  			color:greenyellow;
  		}
  
  		/* 
  			语法6：[属性名 ~= 值]
  			选中包含某个属性，属性值列表中含有指定的值的元素
  		*/
  		[shenqi~='pkq']{
  			color: darkorange;
  		}
  
  		/* 
  			语法7：[属性名 |= 值]
  			选中包含某个属性，属性值为指定值或者前缀为"值-"的元素
  		*/
  		[hello|='xix']{
  			color:deeppink;
  		}
  
  		/* 
  			语法8：[属性名 运算符 值 i]
  			运算符任意，i或者I均可，表示后面的值不区分大小写，对type属性无效
  		*/
  		/* 
  			语法9：[属性名 运算符 值 s]
  			运算符任意，s或者S均可，表示后面的值严格区分大小写
  		*/
  	</style>
  </head>
  <body>
  	<div title="learn">学习快乐1</div>
  	<div abc="xxx">学习快乐2</div>
  	<div aoe="bilibili">学习快乐3</div>
  	<div aoe="ccjk">学习快乐4</div>
  	<div aoe="abc">学习快乐5</div>
  	<div shenqi="pkq lxl">学习使我快乐6</div>
  	<div hello="xix-pkg">学习使我快乐7</div>
  </body>
  </html>
  ```

  >一些案例

  ```css
  a {
    color: blue;
  }
  
  /* 以 "#" 开头的页面内部链接 */
  a[href^="#"] {
    background-color: gold;
  }
  
  /* 包含 "example" 的链接 */
  a[href*="example"] {
    background-color: silver;
  }
  
  /* 包含 "insensitive" 的链接，不区分大小写 */
  a[href*="insensitive" i] {
    color: cyan;
  }
  
  /* 包含 "cAsE" 的链接，区分大小写 */
  a[href*="cAsE" s] {
    color: pink;
  }
  
  /* 以 ".org" 结尾的链接 */
  a[href$=".org"] {
    color: red;
  }
  
  /* 以 "https" 开始，".org" 结尾的链接 */
  a[href^="https"][href$=".org"] {
    color: green;
  }
  ```

  ```css
  /* 将所有包含 `lang` 属性的 <div> 元素的字重设为 bold */
  div[lang] {
    font-weight: bold;
  }
  
  /* 将所有语言为美式英语的 <div> 元素的文本颜色设为蓝色 */
  div[lang~="en-us"] {
    color: blue;
  }
  
  /* 将所有语言为葡萄牙语的 <div> 元素的文本颜色设为绿色 */
  div[lang="pt"] {
    color: green;
  }
  
  /* 将所有语言为中文的 <div> 元素的文本颜色设为红色
     无论是简体中文（zh-CN）还是繁体中文（zh-TW） */
  div[lang|="zh"] {
    color: red;
  }
  
  /* 将所有 `data-lang` 属性的值为 "zh-TW" 的 <div> 元素的文本颜色设为紫色 */
  /* 备注：和 JS 不同，CSS 可以在不使用双引号的情况下直接使用带连字符的属性名 */
  div[data-lang="zh-TW"] {
    color: purple;
  }
  ```

### 伪类选择器

#### 伪类的概念

* 作用:选中特殊状态的元素

  ```sh
  如何理解伪？-- 虚假的，不是真的
  如何理解伪类？-- 像类，但不是类，是元素的一种特殊状态
  ```

* 举例

  `html`

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
  	<meta charset="UTF-8">
  	<meta http-equiv="X-UA-Compatible" content="IE=edge">
  	<meta name="viewport" content="width=device-width, initial-scale=1.0">
  	<title>伪类选择器概念</title>
  	<style>
  		/* 
  			是分类，但是没有用class属性，所以叫伪类
  			什么是伪类？
  			很像类，但不是类，是元素特殊状态的一种描述
  			类用”.“,伪类用":"
  		*/
  		/* 
  			没有访问过的a元素
  		*/
  		a:link{
  			color:orange;
  		}
  		/* 
  			访问过的a元素
  		*/
  		a:visited{
  			color:aqua;
  		}
  	</style>
  </head>
  <body>
  	<a href="#">链接1</a>
  	<a href="#">链接2</a>
  </body>
  </html>
  ```

#### 动态伪类

跟随动作触发的伪类

```sh
":link"
a元素独有，表示超链接未被访问

":visited"
a元素独有，表示超链接被访问过

":hover"
全部元素共有，鼠标悬停在元素上的状态

":active"
全部元素共有，元素激活的状态

":focus"
获取焦点元素
表单元素才能使用:focus伪类。
当用户点击元素、触摸元素、或者通过键盘上的"tab"键等方式，选择元素时，只要让元素处于输入状态就是获得焦点
```

>什么是激活

```sh
元素激活 -- 按下鼠标不松开
```

>注意

```sh
伪类就是状态，一个元素可以同时具备多个状态，按照样式表中伪类顺序决定哪个状态生效，实现最终的样式
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>动态伪类</title>
	<style>
		/* 
		没有访问过的元素，a元素独有的伪类
		*/
		a:link{
			color:orange;
		}
		/* 
			访问过的元素，a元素独有的伪类
		*/
		a:visited{
			color:aqua;
		}
		/* 
			选中鼠标悬浮状态的元素
		*/
		a:hover{
			color:blue;
		}
		/* 
			选中激活状态的元素，
			a元素的话就是鼠标按下不松手
		*/
		a:active{
			color:green;
		}

		/* 
			a元素上面四种伪类乱序不生效的原理
			未被访问时是 link状态
			鼠标移入时有两个状态 link hover
			鼠标按下时有三个状态 link hover active
			访问过后状态为 visited
			移入访问后的a有两个状态 visited hover
			鼠标按下时访问后的有三个状态 visited hover active

			根据样式表的书写顺序来决定生效的样式
		*/

		/* 
			:hover是所有元素都有的伪类，表示鼠标悬浮
			选中的鼠标悬浮的元素
		*/
		p:hover{
			color:blue;
		}
		/* 
			:active是所有元素都有的伪类，表示鼠标按下不松手
			选中的是激活的元素
		*/
		p:active{
			color:red;
		}

		/* 
			获取焦点--在编码层面就是正在输入
			:focus伪类只有表单类元素才具备,或者说只有能输入内容的元素才具备
        	当用户点击元素、触摸元素、或者通过键盘上的"tab"键等方式，选择元素时，只要让元素处于输入状态就是获得焦点
		*/
		input:focus{
			color: orange;
			background-color: green;
		}
		select:focus{
			color: orange;
			background-color: green;
		}

	</style>
</head>
<body>
	<a href="#">链接1</a>
	<a href="#">链接2</a>
	<p>到我上面</p>
	<br>
	<input type="text">
	<br>
	<input type="text">
	<br>
	<select>
		<option value="beijing">北京</option>
		<option value="shanghai">上海</option>
	</select>
</body>
</html>
```

#### 结构伪类1

```sh
:first-child
兄弟中排第一个
父级的所有儿子中排老大

xx-child都是按照所有兄弟或者父级的所有子元素计算的
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>结构伪类1</title>
	<style>
		/* 
			div的子代p元素，且是第一个儿子
			选中的是div的第一个儿子且是p元素 -- 看结构1
		*/
		/* div>p:first-child{
			color:red;
		} */

		/* 
			结构2
			也就是说要同时满足两个条件
			>p  子代p元素
			:first-child 所有儿子中的第一个
		*/
		/* div>p:first-child{
			color:green;
		} */


		/* 
			结构3
			和结构2类似，第一个儿子是marquee
		*/
		div>p:first-child{
			color:green;
		}
		/* 
		结构3
		div的所有后代p元素
		只要p 是第一个儿子就生效

		张三所在的p元素是marquee的第一个儿子且是p标签，所以生效
		测试所在的p元素是div的地一个儿子，所以也生效

		选中的是div的后代p元素，且p的父级是谁无所谓，但p必须是其父亲的第一个儿子
		*/
		div p:first-child{
			color:blueviolet;
		}

		/* 
		不论父级是谁，只要是父亲的第一个儿子，且是p元素
		
		注意body也算父级*/
		p:first-child{
			color:pink;
		}

		/* 
				总结：
				xxx-child都是按照所有兄弟计算的，对于父级来说，就是按照所有子元素计算的
		*/
	</style>
</head>
<body>
	<!-- 结构1 -->
	<!-- <div>
		<p>张三:85分</p>
		<p>里斯:90分</p>
		<p>王五:77分</p>
		<p>赵六:77分</p>
	</div> -->

	<!-- 结构2 -->
	<!-- <div>
		<span>张三:85分</span>
		<p>里斯:90分</p>
		<p>王五:77分</p>
		<p>赵六:77分</p>
	</div> -->

	<!-- 结构3 -->
	<p>我是大儿子</p>
	<div>
		<p>测试</p>
		<marquee>
			<p>张三:98分</p>
		</marquee>
		<p>里斯:90分</p>
		<p>王五:77分</p>
		<p>赵六:77分</p>
	</div>
</body>
</html>
```

#### 结构伪类2--child

>总结

```sh
-child为后缀，都是针对所有兄弟或者父级的所有儿子计算的，针对所有子元素
是针对选择器的
:first-child 所有兄弟元素中的第一个
:last-child 所有兄弟元素中的最后一个
:nth-child(an+b) 所有兄弟元素中的第an+b个,a与b是任意数字，n是变量，代表0～无穷，
```

> 举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>结构伪类2--child</title>
	<style>
		/*
			-child为后缀，都是针对所有兄弟或者父级的所有儿子计算的，针对所有子元素
			是针对选择器的
			:first-child 所有兄弟元素中的第一个
			:last-child 所有兄弟元素中的最后一个
			:nth-child(an+b) 所有兄弟元素中的第an+b个,a与b是任意数字，n是变量，代表0～无穷，
		*/

		div>p:last-child{
			color: aqua;
		}
		/* 
			详解
			:nth-child(an+b)
		*/
		/* 谁都选不中，因为是按照自然计数，和数组下标不一样 */
		div>p:nth-child(0){
			color: blueviolet;
		}
		/* 
		直接写n会选中全部
		留空会什么都不选
		 */
		div>span:nth-child(n){
			color:blue;
		}

		/* 
			由上面我们可以知道，实际上n代表0～无穷，
			所以就可以写公式来获得一些特殊的位置

			例如偶数位
		*/
		div>p:nth-child(2n){
			color:pink;
		}
		/* 
			用公式可以解决很多问题，例如选择前五个
			:nth-child(-n+5)
		*/
		div>p:nth-child(-n+5){
			font-size: 20px;
		}
		/* 
			里面有一些特殊单词来选中奇数和偶数
			:nth-child(even) <=> :nth-child(2n)
			:nth-child(odd) <=> :nth-child(2n+1)
		*/
	</style>
</head>
<body>
	<!-- 结构1 -->
	<div>
		<p>张三:85分</p>
		<p>里斯:90分</p>
		<p>王五:77分</p>
		<p>赵六:77分</p>
		<p>孙七:55分</p>
		<span>我是span1</span>
		<span>我是span2</span>
	</div>

</body>
</html>
```

#### 结构伪类3--type

>总结

```sh
-type为后缀，根据类型，相同类型,这里的类型，可以理解为同选择器
:first-of-type 所有同类型兄弟元素中的第一个
:last-of-type 所有同类型兄弟元素中的最后一个
:nth-of-type(an+b) a和b为数字，n为0到无穷，所有同类型兄弟元素中的第n个
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>结构伪类3--type</title>
	<style>
		/* 
			-type为后缀，根据类型，相同类型,这里的类型，可以理解为同选择器
			:first-of-type 所有同类型兄弟元素中的第一个
			:last-of-type 所有同类型兄弟元素中的最后一个
			:nth-of-type(an+b) a和b为数字，n为0到无穷，所有同类型兄弟元素中的第n个
		*/

		/* 
			选中的是div的第一个儿子p元素(按照所有同类型兄弟计算)
		*/
		div>p:first-of-type{
			color: red;
		}
		/* 
			选中的是div的最后一个儿子p元素(按照所有同类型兄弟计算)
		*/
		div>p:last-of-type{
			color:blue;
		}

		div>p:nth-of-type(2n){
			font-size: 100px;
		}

		/* 验证选择器 */
		.haha:last-of-type{
			color:aqua;
		}
	</style>
</head>
<body>
	<div>
		<span class="haha">我是span1</span>
		<p>张三:85分</p>
		<p>里斯:90分</p>
		<p>王五:77分</p>
		<p>赵六:77分</p>
		<p>孙七:55分</p>
		<span class="haha">我是span2</span>
		<p>王八:562分</p>
	</div>
</body>
</html>
```

#### 结构伪类4

>总结

```sh
一些不常用的伪类
```

```sh
:nth-last-child(an+b)
所有兄弟元素中的倒数第an+b个

:nth-last-of-type(an+b)
所有同类型兄弟元素中的倒数第an+b个

:only-child
选择没有兄弟的元素

:only-of-type
选择没有同类型兄弟的元素

:root
根元素，单独写，等价于html

:empty
内容为空元素(空格也算内容)
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>结构伪类</title>
	<style>
		/* 
		正序
			:nth-child(an+b)
			:nth-of-type(an+b)
		
		倒序
			:nth-last-child(an+b)
			:nth-last-of-type(an+b)

		特殊
			:only-child 唯一子元素，没有兄弟
			:only-of-type 唯一同类子元素，没有同类兄弟

			:root  选中整个html文档的跟元素，相当于 html
			:empty 选中空的元素，即没有标签体的元素
		*/
		/* 选中div中倒数第n个儿子p元素(按照所有兄弟) */
		div>p:nth-last-child(3){
			color:red;
		}
		/* 选中div中倒数第n个儿子p元素(按照所有同类型的兄弟) */
		div>p:nth-last-of-type(3){
			color:red;
		}
		/* 选中唯一元素span */
		div>span:only-child{
			color:darkgreen;
		}
		/* 选中唯一同类元素 */
		div>span:only-of-type{
			color:gold;
		}

		/* 整个html文档的根元素，和直接写html效果一样 */
		:root{
			font-size: 16px;
		}

		/* 
		选中没有标签体的空的div
		空格也算标签体
		 */
		div:empty{
			height: 40px;
			width: 20px;
			background-color: blueviolet;
		}
	</style>
</head>
<body>
	<div>
		<span>我是span1</span>
		<p>张三:85分</p>
		<p>里斯:90分</p>
		<p>王五:77分</p>
		<p>赵六:77分</p>
		<p>孙七:55分</p>
		<span>我是span2</span>
		<p>王八:562分</p>
	</div>
	<div>
		<span>没有兄弟</span>
	</div>
	<div>
		<span>没有同类兄弟</span>
		<p>我不是span</p>
	</div>
	<!-- 没有标签体的div -->
	<div></div>
</body>
</html>
```

#### 否定伪类

* 作用：

  ```sh
  :not(选择器)
  在当前条件下，排除满足括号中条件的元素
  ```

* 举例

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
  	<meta charset="UTF-8">
  	<meta http-equiv="X-UA-Compatible" content="IE=edge">
  	<meta name="viewport" content="width=device-width, initial-scale=1.0">
  	<title>否定伪类</title>
  	<style>
  		/* 
  		在当前条件下排除满足某一定条件的
  		选中div的p子元素，排除类名为fail的
  
  		从 div>p 中排除 div>p.fail
  		*/
  		div>p:not(.fail){
  			color: blue;
  		}
  
  		/* 
  			选中的是div的p子元素
  			但是排除title属性值以"你要加油"开头的
  
  			从 div>p 中排除 div>p[title^="你要"]
  		*/
  		div>p:not([title^="你要"]){
  			color: pink;
  		}
  
  		/* 
  			从 div>p 中排除 div>p:first-child
  			选中的是div的p子元素，但是排除第一个p子元素
  		*/
  		div>p:not(:first-child){
  			color:aquamarine;
  		}
  	</style>
  </head>
  <body>
  	<div>
  	
  		<p class="fail">张三:85分</p>
  		<p>里斯:90分</p>
  		<p class="fail">王五:77分</p>
  		<p title="你要加油">赵六:77分</p>
  		<p title="你要努力">孙七:55分</p>
  		
  		<p>王八:562分</p>
  	</div>
  </body>
  </html>
  ```

  #### UI伪类

  >总结

  ```sh
  :checked
  被选中的复选框或单选按钮
  
  :enabled
  可用的表单元素(没有disabled属性)
  
  :disabled
  不可用的表单元素(有disabled属性)
  ```

  >举例

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
  	<meta charset="UTF-8">
  	<meta http-equiv="X-UA-Compatible" content="IE=edge">
  	<meta name="viewport" content="width=device-width, initial-scale=1.0">
  	<title>UI伪类</title>
  	<style>
  		/* 
  			利用动态伪类focus可以实现，当我们勾选时
  			复选框样式发生变化，但是有一个问题，那就是我们取消勾选后不会回去
  		*/
  		#one:focus{
  			width: 100px;
  			height: 100px;
  		}
  
  		/* 
  			UI伪类checked
  			选中单/复选框时样式改变，取消选中，样式回归本初
  
  			注意，复选框和单选框我们只能改变大小，样式是改变不了的
  			大厂的做法：
  			京东-- 将复选框隐藏，用一个div覆盖在他上面实现样式的改变，借助js
  		*/
  		#two:checked,#three:checked{
  			width: 50px;
  			height: 50px;
  		}
  
  		/* 
  		选中的是被禁用的input元素
  
  		UI伪类 :disabled 选中被禁用的表单元素
  		 */
  		input:disabled{
  			background-color: blueviolet;
  		}
  
  		/* 
  			选中的是可用的input元素
  
  			UI伪类 :enabled 可用的表单元素
  		*/
  		input:enabled{
  			background-color: blue;
  		}
  	
  	</style>
  </head>
  <body>
  	<input id="one" type="checkbox">
  	<input  id="two" type="checkbox">
  	<input  id='three' type="radio">
  	<input type="text" disabled>
  	<input type="text">
  </body>
  </html>
  ```

  #### 目标伪类

  >总结

  ```sh
  :target
  选中锚点指向的元素
  ```

  >举例

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
  	<meta charset="UTF-8">
  	<meta http-equiv="X-UA-Compatible" content="IE=edge">
  	<meta name="viewport" content="width=device-width, initial-scale=1.0">
  	<title>目标伪类</title>
  	<style>
  		div{
  			background-color: gray;
  			height: 200px;
  		}
  		/* 
  			目标伪类别 :target
  		
  			选中锚点指向的元素
  			锚点跳转引起地址栏变化，底层自动用地址去匹配对应id
  		*/
  		div:target{
  			background-color: green;
  		}
  	</style>
  </head>
  <body>
  	<!-- 
  		锚点跳转
  		现在想实现，点击锚点往哪跳，哪个div的背景色就变绿
  	-->
  	<a href="#one">去看第1个</a>
  	<a href="#two">去看第2个</a>
  	<a href="#three">去看第3个</a>
  	<a href="#four">去看第4个</a>
  	<a href="#five">去看第5个</a>
  	<a href="#six">去看第6个</a>
  	<div	id="one">第1个</div>
  	<br>
  	<div	id="two">第2个</div>
  	<br>
  	<div	id="three">第3个</div>
  	<br>
  	<div	id="four">第4个</div>
  	<br>
  	<div	id="five">第5个</div>
  	<br>
  	<div	id="six">第6个</div>
  </body>
  </html>
  ```

#### 语言伪类

>总结

```sh
:lang()
根据指定的语言选择元素(本质是看lang属性的值)
```

>举例

```html
<!DOCTYPE html>
<html lang="zh">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>语言伪类</title>
	<style>
		/* 
			选择语言为英文的p标签,变成红色

			准确点来说是选中了有 lang属性且属性值为 en 的
		*/
		p:lang(en) {
			color: red;
		}

		/* 
			根据我们给html所写的lang属性,每个元素身上默认有一个相同的lang属性
		*/
		:lang(zh){
			color: blue;
		}

		/* 
			所以这个标签本身不具备真正的识别功能,根据我们提供的lang属性来识别
		*/
	</style>
</head>
<body>
	<div>社会</div>
	<div>人生</div>
	<p lang="en">前端</p>
	<p>后端</p>
	<p lang="en">UI</p>
	<span>你好</span>
</body>
</html>
```

### 伪元素选择器

* 作用:选中元素中的一些特殊位置

* 常用伪元素:

  ```sh
  ::first-letter 选中元素中的第一个文字
  ::first-line 选中元素中的第一行文字
  ::selection 选中被鼠标选中的内容
  ::placeholder 选中输入框的提示文字
  ::before 在元素最开始的位置,创建一个子元素 (必须用 content 属性指定内容)
  ::after  在元素最后的位置,创建一个子元素(必须用 content 属性指定内容)
  ```

* 举例

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
  	<meta charset="UTF-8">
  	<meta http-equiv="X-UA-Compatible" content="IE=edge">
  	<meta name="viewport" content="width=device-width, initial-scale=1.0">
  	<title>伪元素选择器</title>
  	<style>
  		/* 
  			什么是伪元素?
  			很像元素,但不是元素(element),是元素中的一些特殊位置
  
  			::first-letter 第一个字符
  			::first-line 第一行
  		*/
  		/* 
  			让第一个文字变大,且为红色
  
  			理解为什么叫伪元素?
  			div内部字母或者说文字是div元素的一部分,他严格意义上不算元素,但我们能选中,并且像元素一样操作他,所以叫伪元素
  
  		*/
  		div::first-letter{
  			font-size: 20px;
  			color:red;
  		}
  
  		/* 
  			让第一行发生变化,根据浏览器的宽度变化,行选中也会不一样
  		*/
  		div::first-line{
  			background-color: yellow;
  		}
  
  		/* 
  			让div中被鼠标选中的内容样式发生变化
  		*/
  		div::selection{
  			background-color: green;
  			color: orange;
  		}
  
  		/* 
  			让input的提示文字样式改变
  		*/
  		input::placeholder{
  			color:skyblue;
  		}
  
  		/* 
  			在谁之前添加
  
  			在p元素的内容之前
  
  			::before 选中元素最前面的位置,在前面添加
  		*/
  		p::before{
  			/* 
  			content就是内容
  			与我们直接手写的区别--不可选中 
  			*/
  			content: "$";
  		}
  
  		/* 
  			在谁之后添加
  			在p元素的内容之后
  
  			::after 选中元素最后的位置,在之后添加
  		*/
  		p::after{
  			content: ".00";
  		}
  
  		/* 
  			除了 ::selection 和 ::placeholder 这些css3提出的新的伪元素选择器,其他的都可以只写两个点,和伪类一样,但是随着css越来越规范,建议完整书写
  
  			还有就是伪元素选择器的内容在解析后会直接显示为伪元素标签
  		*/
  	</style>
  </head>
  <body>
  	<!-- 输入 lorem 会生成一串随机长文 -->
  	<!-- 输入 lorem数字 会生成由n个单词组成的一句话,n是你输入的数字 -->
  	<div>
  		Lorem ipsum, dolor sit amet consectetur adipisicing elit. Autem libero amet quibusdam nam, ad eos hic at facere magni quia veritatis incidunt qui provident culpa maiores pariatur labore sequi vel eaque consequatur temporibus dignissimos. Quos alias nisi aliquam architecto incidunt ipsa corrupti iste nemo? Alias ducimus architecto quae temporibus neque quidem dolores aperiam fugiat aliquam? Explicabo beatae dolore, facilis fugit ratione autem? Magnam obcaecati cum alias voluptas laboriosam exercitationem id expedita nisi commodi ratione libero esse veritatis, saepe quaerat odit repudiandae molestiae atque debitis impedit sed! Eligendi veritatis perferendis non qui reiciendis recusandae, beatae alias, error totam fugiat, rem temporibus.
  	</div>
  
  	<input type="text" placeholder="请输入您的用户名">
  
  	<!-- 
  		如果有多个这样的金额标签,前面我们都要写$,后面都要写.00
  		想要统一快速的生成
  	 -->
  	<p>$99.00</p>
  	<p>100</p>
  	<p>52</p>
  
  </body>
  </html>
  ```

## Css选择器优先级--入门

### 样式表的优先级

```sh
1.行内样式 > 内部样式 = 外部样式
2. 在优先级相同时,后来者居上
3. 同类型优选择器,后来者居上,即如果两个选择器一样,则后来者居上
```

### 优先级比较

根据同优先级的后来者居上的理念,我们可以来进行优先级的比较

* `元素选择器>通配选择器`

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
  	<meta charset="UTF-8">
  	<meta http-equiv="X-UA-Compatible" content="IE=edge">
  	<meta name="viewport" content="width=device-width, initial-scale=1.0">
  	<title>选择器优先级</title>
  	<style>
  		/* 元素选择器大于通配选择器 */
  		h2{
  			color: red;
  		}
  		*{
  			color: green;
  		}
  	</style>
  </head>
  <body>
  	<h2>世上无难事</h2>
  </body>
  </html>
  ```

* `类选择器>元素选择器`

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
  	<meta charset="UTF-8">
  	<meta http-equiv="X-UA-Compatible" content="IE=edge">
  	<meta name="viewport" content="width=device-width, initial-scale=1.0">
  	<title>选择器优先级</title>
  	<style>
  		/* 类选择器>元素选择器>通配选择器 */
  		.slogan{
  			color:green;
  		}
  		h2{
  			color: red;
  		}
  	</style>
  </head>
  <body>
  	<h2 class="slogan">世上无难事</h2>
  </body>
  </html>
  ```

* `ID选择器>类选择器`

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
  	<meta charset="UTF-8">
  	<meta http-equiv="X-UA-Compatible" content="IE=edge">
  	<meta name="viewport" content="width=device-width, initial-scale=1.0">
  	<title>选择器优先级</title>
  	<style>
  		/* ID选择器>类选择器>元素选择器>通配选择器  */
  		#title{
  			color: blueviolet;
  		}
  		.slogan{
  			color: blue;
  		}
  	</style>
  </head>
  <body>
  	<h2 id="title" class="slogan">世上无难事</h2>
  </body>
  </html>
  ```

* `行内样式>ID的选择器`

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
  	<meta charset="UTF-8">
  	<meta http-equiv="X-UA-Compatible" content="IE=edge">
  	<meta name="viewport" content="width=device-width, initial-scale=1.0">
  	<title>Document</title>
  	<style>
  		/* 行内样式 > ID选择器 */
  		/* 
  			原因:所有的选择器实际上都是内部或者外部样式
  		*/
  		#title{
  			color: blueviolet;
  		}
  	</style>
  </head>
  <body>
  	<h2 id="title" style="color: blue;">学无止境</h2>
  </body>
  </html>
  ```

### 总结

```sh
行内样式 > 内部样式 = 外部样式
ID选择器 > 类选择器 > 元素选择器 > 通配选择器
```

```sh
通过"不同的选择器",选中"相同的元素",并且为"相同样式名"设置"不同的值"时,就发生了样式的冲突,到底要应用哪个样式,此时就需要看优先级了
```

## Css选择器优先级--原理

### 权重

```sh
1.计算方式：每个选择器，都可以计算出一组权重，格式为：(a,b,c)
"a" ID选择器的个数
"b" 类、伪类、属性 选择器的个数
"c" 元素、伪元素 选择器的个数

例如：
`*`      (0,0,0)
`ul>li`  (0,0,2)
`div ul>li p a span` (0,0,6)
`#test .test`    (1,1,0)
`#test a:hover`  (1,1,1)
```

```sh
2.比较规则：按照"从左到右"的顺序，依次比较大小，当前位胜出，后面的不再比较
权重比较
(a1,b1,c1)
(a2,b2,c2)
一位位比较，相同就看下一位，大的就直接胜出
例如：
a1 == a2 则看b1与b2
a1 > a2  则 a1 直接胜出，不再往后看

权重大的展示，权重一样时后来者居上
```

### 优先级

> 前提

```sh
通过"不同的选择器",选中"相同的元素",并且为"相同样式名"设置"不同的值"时,就发生了样式的冲突,到底要应用哪个样式,此时就需要看优先级了

即优先级是样式冲突时决定最终样式的
```

>总结

```sh
对于样式的最终形态

!important > style > 权重

!important是针对某一样式的，一般不推荐使用，因为写了就很难修改
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>选择器优先级--复杂</title>
	<style>
		/* 
			选择器权重
			格式 (a,b,c)
			a:ID选择器个数
			b:类、伪类、属性 选择器个数
			c：元素、伪元素选择器个数
			通配选择器权重:(0,0,0)

			1.计算权重，就是一个个数，得出 (a,b,c)

			2.权重比较
			(a1,b1,c1)
			(a2,b2,c2)
			一位位比较，相同就看下一位，大的就直接胜出
			例如：
			a1 == a2 则看b1与b2
			a1 > a2  则 a1 直接胜出，不再往后看

			3.权重大的展示，权重一样时后来者居上

			在vscode中把鼠标放到样式上，会有一个 “选择器特定性”/"Selector Specificity"
			这就是选择器权重

			以下两种极少用，尤其是!important会产生极大破坏
			style可以理解为 （1,a,b,c)
			!important 可以理解为（1,?,a,b,c)
		*/
		/* 
			(2,0,0)
		*/
		#test #learn{
			color: aqua;
		}
		/* 
			(1,0,0)
		*/
		#learn{
			color: yellow;
		}
		/* 
			(0,2,1)
		*/
		.container span.slogan{
			color: red;
		}
		/* 
			(0,1,3)
		*/
		div>p>span:nth-child(1){
			color: green;
		}
		/* 
			(0,1,3)
		*/
		div>p>span:first-child{
			color: blue;
		}

		/* 
			(0,1,0)
		*/
		.slogan{
			/* 
				important不是针对选择器，而是针对这一个属性，
				他高于行内和选择器权重
			*/
			color: darkgoldenrod !important;
		}
	</style>
</head>
<body>
	<div class="container" id="test">
		<p>
			<span class="slogan" id="learn">天下没有难学的技术!</span>
			<span>学无止境!</span>
		</p>
	</div>
</body>
</html>
```

## Css三大特性

### 层叠性

>概念

```sh
如果发生了样式冲突，那么会根据一定的规则(一般是选择器优先级)，进行样式的层叠(覆盖)。

通俗的说：就是一层层的往上叠加，上层会覆盖下面的
```

```sh
什么是样式冲突？
元素的同一个样式名，被设置了不同的值，这就是冲突。
```

### 继承性

>概念

```sh
元素会自动拥有其"父元素"、或其"祖先元素"上所设置的"某些样式"。
```

>规则

```sh
就近原则
优先继承"离的近"的
```

>常见的可继承属性

```sh
text-？？
font-？？
line-？？
color
...
```

>备注

```sh
参照MDN网站，可查询属性是否可被继承

#简体中文
Css-参考-Properties-属性-规范/形式定义-是否是继承属性

#英文
Css - Reference - Properties - 属性 - Formal definition - Inherited(是否可继承)

#日文
Css - Reference - Properties - 属性 - 公式定義 - 継承

把鼠标放在样式名上，会自动出现导向MDN的链接 MDN Reference
```

### 优先级

```sh
!important > 行内 > 权重 > 继承的样式

即
继承过来的样式最弱，即使是通配都比他高，可以理解为(-1,-1,-1)
```

>权重

```sh
1.计算方式：每个选择器，都可以计算出一组权重，格式为：(a,b,c)
"a" ID选择器的个数
"b" 类、伪类、属性 选择器的个数
"c" 元素、伪元素 选择器的个数

例如：
`*`      (0,0,0)
`ul>li`  (0,0,2)
`div ul>li p a span` (0,0,6)
`#test .test`    (1,1,0)
`#test a:hover`  (1,1,1)
```

```sh
2.比较规则：按照"从左到右"的顺序，依次比较大小，当前位胜出，后面的不再比较
权重比较
(a1,b1,c1)
(a2,b2,c2)
一位位比较，相同就看下一位，大的就直接胜出
例如：
a1 == a2 则看b1与b2
a1 > a2  则 a1 直接胜出，不再往后看

权重大的展示，权重一样时后来者居上
```

#### 注意

```sh
在计算权重的时候，并集选择器是分开算得
```

```css
div,div>p,#test a:hover{
    color:blue;
}

他们分开计算权重，因为实际上就是多个

div （0,0,1）
div>p (0,0,2)
#test a:hover (1,1,1)
```

## Css像素

```sh
显示器是由一个个发光的小点组成的，这些小点就是像素，也就是我们前端开发常用的px
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>Css像素</title>
	<style>
		/* 
			想想生活中常见的长度单位
			km m dm cm mm um
		*/
		.test1{
			width: 1km;
			height: 1km;
			background-color: blue;
		}
		.test2{
			width: 1m;
			height: 1m;
			background-color: aqua;
		}
		.test3{
			width: 1dm;
			height: 1dm;
			background-color: rgb(43, 226, 119);
		}
		.test4{
			width: 1cm;
			height: 1cm;
			background-color: blueviolet;
		}
		.test5{
			width: 1mm;
			height: 1mm;
			background-color: red;
		}
		.test6{
			width: 1um;
			height: 1um;
			background-color: red;
		}
		/* 
		经过验证 cm 和 mm 是可以生效的
		设计 px 的原因，cm和mm对于网页设计来说不够精细，所以设计出了px

		屏幕实际上是由许多发光的小点组成的，这些小点就是像素，我们用手机拍电脑或者把图片放大数倍看到的一个个小方块就是像素点
		像素是一个相对单位，根据屏幕来的，屏幕像素1980x1024,则1px就是屏幕高度/1980
		所以图片在不同显示器上不一样，是因为像素不一样，或者说分辨率
		 */
		 /* 
		 	截图工具量出来的，以及我们看到的和我们写的大小不一样的原因
			电脑自动开了缩放，所以我们直接用工具去测量会出现问题，需要根据缩放计算出真实像素

			UI设计师会解决这个问题
		 */
	</style>
</head>
<body>
	<div class="test1"></div>
	<br>
	<div class="test2"></div>
	<br>
	<div class="test3"></div>
	<br>
	<div class="test4"></div>
	<br>
	<div class="test5"></div>
</body>
</html>
```

## Css颜色

### 颜色名表达颜色

* 编写方式：直接使用颜色对应的英文单词，编写比较简单，例如

  ```css
  #test {
      color:blue;
  }
  ```

* 注意

  ```sh
  1.颜色名这种方式，表达的颜色比较单一，所以用的并不多。
  2.具体的颜色名参考MDN官方文档
  https://developer.mozilla.org/en-US/docs/Web/CSS/named-color
  ```

* 举例

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
  	<meta charset="UTF-8">
  	<meta http-equiv="X-UA-Compatible" content="IE=edge">
  	<meta name="viewport" content="width=device-width, initial-scale=1.0">
  	<title>Css颜色</title>
  	<style>
  		/* 
  			使用颜色名
  			局限性:
  			1.颜色名不能随便写，
  			2.颜色名有限
  			3.表达不精确
  
  			所以开发时基本不用
  			2.具体的颜色名参考MDN官方文档
  			https://developer.mozilla.org/en-US/docs/Web/CSS/named-color
  		*/
  		.test{
  			color: red;
  		}
  		
  	</style>
  </head>
  <body>
  	<h2 class="test">学无止境！</h2>
  </body>
  </html>
  ```

### 颜色表达之rgb&rgba

#### 取色

>取色器

```sh
FSCapture
Snipaste
```

>微调

```sh
通过idea或者vscode
```

#### 编写方式

```sh
使用红黄蓝这三种光的三原色进行组合。
"r"   表示红色
"g"   表示绿色
"b"   表示蓝色
"a"   表示透明度
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>rgb或rgba</title>
	<style>
		/* 
			rgb(红，绿，蓝)
			光的三原色 红绿蓝，因为我们写的东西是要给显示器发光点用的
			颜料的三原色 红黄蓝

			三个值的范围都是 0～255,不同比例混合，可以实现自然界所有的颜色
			也可以写百分比,不过这样写的少，因为不好算

			要么都写百分比，要么都写数字，混写无效
		*/
		h2 {
			color:rgb(red, green, blue)
		}
		.red {
			color:rgb(255, 0, 0)
		}
		.ziluolan{
			color:rgb(138, 43, 226)
		}
		.blue{
			color: rgb(0%, 0%, 100%);
		}
		/* 
			rgba(红，绿，蓝,透明度)
			a=>alpha
			数字表达：0～1,可以为小数，0为完全透明，1为不透明，0.xx 可以简写为 .xx
			透明了，但是还存在，会展示下一层的颜色，相当于隐身了

			百分比：0%～100%，这个可以和前面混写，说的不能混写指的是红绿蓝三原色必须都是同类表达
		*/
		.red0{
			color: rgba(255, 0, 0, 0.5);
		}
	</style>
</head>
<body>
	<h2>学无止境！</h2>
	<p class="red">纯红色</p>
	<p class="ziluolan">紫罗兰色</p>
	<p class="blue">纯蓝色</p>
	<p class="red0">半透明的纯红色</p>
</body>
</html>
```

>小规律

```sh
1.若三种颜色值相同，呈现的是灰色，值越大，灰色越深
2.rgb(0,0,0)是黑色，rgb(255,255,255)是白色
3.对于rgba来说，前三位的rgb形式要保持一致，要么都是0～255的数字，要么都是百分比。
```

### 颜色表达之HEX&HEXA

就是16进制

HEX的原理与rgb一样，依然是通过：`红`、`绿`、`蓝`进行组合，只不过要有6个数字，分成3组来表达。

格式为：

```sh
"#rrggbb"
每一位数字的取值范围是：0～f
所以每一种光的最小值是00,最大值是ff，就是16进制表示0～255

不区分大小写，但推荐全小写
```

>注意

```sh
IE浏览器不支持HEXA，但支持HEX
```

> 举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>HEX与HEXA</title>
	<style>
		/* 
			本质与rgb和rgba类似
			# 开头，后面有三组值，每组值都由两位组成 #rrggbb
			rr 控制红色，gg控制绿色，bb控制蓝色 值是16进制，00～0f表示0到16,10是17,最大值是ff
		*/
		.red {
			color: #ff0000;
		}
		/* 
			后面再补两位，就是透明度
			#rrggbbaa
			透明度从00～ff，表示从0%～100%
		*/
		.red0{
			color: #ff000088;
		}
		/* 
			IE不支持HEXA但是支持HEX
		*/
		/* 
			简写形式：如果 rrggbb的值都一样，可以缩写为rgb，一旦前三位简写，那么透明度也得简写
		*/
	</style>
</head>
<body>
	<h2>学无止境！</h2>
	<p class="red">纯红色</p>
	<p class="ziluolan">紫罗兰色</p>
	<p class="blue">纯蓝色</p>
	<p class="red0">半透明的纯红色</p>
</body>
</html>
```

### 颜色表达式之HSL与HSLA

```sh
HSL是通过：色相、饱和度、亮度，来表示一个颜色的，格式为hsl(色相,饱和度,亮度)
"色相"
取值范围是0~360edg,具体对应色相环
"饱和度"
取值范围是0%~100%.(向灰色中添加色相对应颜色,0%全灰,100%色相颜色)
"亮度"
取值为0%~100%,(0%亮度没了,所以为黑色,100%亮度太强为白色)

HSLA,就是添加了透明度,hsla(色相,饱和度,亮度,透明度)
透明度值为0%~100%,或者0~1
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>HSL与HSLA</title>
	<style>
		/* 
			hsl(hue, saturation, lightness)
			hsl(色相，饱和度，明度)

			色相，用角度表示颜色，要了解色相环
			饱和度，黑白照片饱和度0%，彩照饱和度100%，色彩的浓郁度，饱和度说高低，理解就是往灰色里面掺色相对应的颜色
			明度/亮度，0%关灯，100%强光，一般用50%，越小黑色越多，越大白色越多
		*/
		.red {
			/* deg可以省略 */
			color:hsl(0deg, 100%, 50%)
		}
		.blue {
			color:hsl(240, 100%, 50%)
		}
		/* 
			hsla(hue, saturation, lightness, alpha)
			alpha是透明度，可以写0～1,也可以写0%～100%
		*/
		.red0 {
			
			color:hsla(0, 100%, 50%, 0.5)
		}
	</style>
</head>
<body>
	<h2>学无止境！</h2>
	<p class="red">纯红色</p>
	<p class="ziluolan">紫罗兰色</p>
	<p class="blue">纯蓝色</p>
	<p class="red0">半透明的纯红色</p>
</body>
</html>
```

## Css字体属性

### 字体大小

* 属性名：`font-size`

* 语法：

  ```css
  p {
      font-size:40px;
  }
  
  /*
  	vscode 快捷指令 fs
  */
  ```

* 注意点

  ```sh
  1.chrome浏览器支持的最小文字为12px，默认文字大小为16px，并且0px会自动消失。
  2.不同浏览器默认的字体大小可能不一致，所以最好给一个明确的值，不要用默认大小。
  3.通常以给body设置font-size属性，这样body中的其他元素就都可以继承了。
  ```

* 举例

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
  	<meta charset="UTF-8">
  	<meta http-equiv="X-UA-Compatible" content="IE=edge">
  	<meta name="viewport" content="width=device-width, initial-scale=1.0">
  	<title>字体大小</title>
  	<style>
  		/* 
  			我们在项目开发时应该明确指出元素里面文字的大小，
  			因为不同浏览器默认文字大小不一样，而且是可变的，所以最好自己控制
  		*/
  		/* 
  			由于所有的元素都在body里，所以这样通过继承性，就可以让他们都有一个字体大小
  			由于继承的优先级最弱，所以我们要修改只需要在合适的地方写其他样式就可以
  		*/
  		body {
  			font-size: 20px;
  		}
  		/* 
  			ctrl + 0 回归100%,去除缩放
  			ctrl + 鼠标滚轮 放大缩小
  		*/
  		/* 
  			调试模式:
  			在元素上选择检查,就可以在控制台的样式表进行调整
  			单击想要修改的内容进入编辑模式,然后再选中数字,用键盘的上下键就可以一点点的加减
  
  			Inherited from xxx
  			就是从xxx继承得来的样式
  		*/
  		.test1 {
  			font-size: 40px;
  		}
  		.test2 {
  			font-size: 30px;
  		}
  		.test3 {
  			font-size: 20px;
  		}
  
  		.test4 {
  			font-size: 20px;
  		}
  		
  		.test5{
  			/* 
  			由于浏览器都有一个最小字号,在外观设置里
  			一旦我们写的数值在0到最小字号之间,默认展示最小字号大小
  			0的话代表不展示,chrome默认最小字号为12px,所以这个10px最终展示时仍然是12px
  			逍遥展示10px,只能呢个去设置里面吧最小字号调的比12px小
  		*/
  			font-size: 10px;
  		}
  
  	
  	</style>
  </head>
  <body>
  	<p class="test1">字体测试1</p>
  	<p class="test2">字体测试2</p>
  	<p class="test3">字体测试3</p>
  	<p class="test4">字体测试4</p>
  	<p class="test5">字体测试5</p>
  	<!-- 不写字体大小，chrome默认就是16px，要调整也需要在浏览器里面进行调整自定义字号 -->
  	<p>字体测试6</p>
  </body>
  </html>
  ```

### 字体族

* 属性名：`font-family`

* 语法

  ```css
  div {
      font-family:"STHupo","STCaiyun","Microsoft YaHei",sans-serif;
  }
  ```

* 注意

  ```sh
  1.使用字体的英文名字兼容性会更好，具体的英文名可以自行查询，或在电脑的设置里去寻找。
  2.如果字体名包含空格，必须使用引号包裹起来。
  3.可以设置多个字体，按照从左到右的顺序逐个查找，找到就用，没有找到就使用后面的，且通常在最后写上serif(衬线)或sans-serif(非衬线)。
  ```

* 举例

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
  	<meta charset="UTF-8">
  	<meta http-equiv="X-UA-Compatible" content="IE=edge">
  	<meta name="viewport" content="width=device-width, initial-scale=1.0">
  	<title>字体组</title>
  	<style>
  		body {
  			font-size: 40px;
  		}
  		/* 
  			font-family:"字体族"
  			建议把族名用双引号引起来，单引号也可以，不加其实也可以，但如果名字里有空格就必须要包起来
  		*/
  		.test1 {
  			font-family: "宋体";
  		}
  		.test2{
  			/* 
  				windows上自带这种字体，
  			*/
  			font-family: "微软雅黑";
  		}
  		.test3 {
  			font-family: "楷体";
  		}
  		.test4 {
  			font-family: "华文彩云";
  		}
  		.test5 {
  			font-family: "华文彩云","楷体","宋体","微软雅黑";
  		}
  		/* 
  			当我们写的字体族不存在时，就会变成默认字体
  			1.在电脑个性化里面搜索字体，可以看到目前这台电脑有哪些字体
  			2.安装字体，下载字体ttf，双击安装即可
  		*/
  		/* 
  			我们一般会把字体分为两大类：衬线字体，非衬线字体
  
  			衬线字体：字棱角清晰
  			非衬线字体：字体几乎没棱角
  
  			在设置字体族的时候，尽量遵循要么都是衬线，要么都是非衬线，不会有bug，就是设计规范而已
  		*/
  		/* 
  			兼容性问题
  			很多时候，我们字体族用中文在一些浏览器上是不认的，所以需要使用英文
  
  			1.由于字体名过于繁杂，所以现用现查最稳妥
  			2.电脑上安装的字体，可以在设置里面查看，这个经常不对
  
  			我们一般会在字体族的最后用衬线或非衬线收尾，非强制
  			衬线 serif
  			非衬线 sans-serif
  			引号推荐不加，表示是一个规范
  			他的作用，当前面都阵亡时，会联系电脑和浏览器，让他们随机拿一个对应类型字体过来用
  		*/
  		.test6 {
  			font-family:"STHupo","STCaiyun","Microsoft YaHei",sans-serif;
  		}
  	</style>
  </head>
  <body>
  	<p class="test1">宋体</p>
  	<p class="test2">微软雅黑</p>
  	<p class="test3">楷体</p>
  	<p class="test4">华文彩云</p>
  	<p class="test5">按照字体族从左到右的顺序，哪个生效用哪个，不再往后边看,如果都没生效就用默认的</p>
  	<p class="test6">为了避免兼容性问题，尽量使用英文字体族</p>
  </body>
  </html>
  ```

### 字体风格

* 属性名：`font-style`

* 常用值：

  ```sh
  "normal"
  正常的
  
  "italic"
  斜体 对于字体族，他先去找字体族里面设置的倾斜的字体，如果有就直接用，如果没有就强制倾斜正常的，主要用这个
  
  "oblique"
  斜体 对于字体族，他直接去找正常的字体，然后做一个强制倾斜
  
  实际开发中，斜体推荐使用"italic"
  ```

* 语法

  ```css
  div {
      font-style:italic;
  }
  ```

* 举例

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
  	<meta charset="UTF-8">
  	<meta http-equiv="X-UA-Compatible" content="IE=edge">
  	<meta name="viewport" content="width=device-width, initial-scale=1.0">
  	<title>字体风格</title>
  	<style>
  		/* 	
  			font-style 控制字体倾斜等等
  			常用值：
  			normal 一般的，正常的
  			italic 斜的，对于字体族，他先去找字体族里面设置的倾斜的字体，如果有就直接用，如果没有就强制倾斜正常的，主要用这个
  			oblique 斜的，对于字体族，他直接去找正常的字体，然后做一个强制倾斜
  		*/
  		.test1 {
  			font-style: normal;
  		}
  		.test2 {
  			font-style: italic;
  		}
  	</style>
  </head>
  <body>
  	<p class="test1">学无止境！！</p>
  	<p class="test2">醉汉</p>
  </body>
  </html>
  ```

### 字体粗细

* 属性名：`font-weight`

* 常用值：

  * 关键词

    ```sh
    lighter 细的
    normal 正常
    bold 粗
    bolder 很粗，多数字体不支持
    ```

  * 数值

    ```sh
    100～1000且无单位，数值越大，字体越粗(或一样粗，具体得看字体设计的精确程度)
    对于微软雅黑：100~300等同于lighter，400～500等同于normal，600及以上等同于bold
    ```

  * 语法

    ```css
    p {
        font-size:bold;
    }
    
    p {
        font-size:600;
    }
    ```

* 举例

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
  	<meta charset="UTF-8">
  	<meta http-equiv="X-UA-Compatible" content="IE=edge">
  	<meta name="viewport" content="width=device-width, initial-scale=1.0">
  	<title>字体粗细</title>
  	<style>
  		/* 
  			font-weight 字体粗细
  			属性值：
  			lighter 细的
  			normal 正常
  			bold 粗的
  			bolder 更粗
  
  			根据字体族，如果字体族没设置，那么就按照就近原则，例如微软雅黑没有设置bolder，那么就以bold展示
  			还可以写数字 100～1000,但是也要看字体族，如果没设置就没有
  
  			对于微软雅黑
  			100～300 相当于 lighter
  			400～500 相当于 normal
  			600～1000 相当于 bold
  		*/
  		.test1 {
  			font-weight: lighter;
  		}
  		.test2 {
  			font-weight: normal;
  		}
  		.test3 {
  			font-weight: bold;
  		}
  	</style>
  </head>
  <body>
  	<p class="test1">瘦子</p>
  	<p class="test2">学无止境！！</p>
  	<p class="test3">胖子</p>
  </body>
  </html>
  ```

### 字体复合属性

* 属性名：`font`，可以把上述字体样式合并成一个属性。

* 编写规则：

  ```sh
  1.字体大小、字体族必须都写上
  2.字体族必须是最后一位，字体大小必须是倒数第二位
  3.各个属性间用空格隔开
  ```

* 举例

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
  	<meta charset="UTF-8">
  	<meta http-equiv="X-UA-Compatible" content="IE=edge">
  	<meta name="viewport" content="width=device-width, initial-scale=1.0">
  	<title>字体复合属性</title>
  	<style>
  		/* 
  			font 统一调整字体的相关属性，参数有顺序要求
  			1. 字体大小 ，放在倒数第二位，必须要写
  			2. 字体族 ，必须放在最后，必须要写
  			3.其他的在前面随意写
  			不同参数用空格隔开
  		*/
  		.test {
  			font:bold italic 100px "微软雅黑","华文彩云",sans-serif;
  		}
  	</style>
  </head>
  <body>
  	<p class="test">
  		统一调整字体
  	</p>
  </body>
  </html>
  ```

## Css常用文本属性

### 文本颜色

* 属性名：`color`

* 可选值：

  ```sh
  1.颜色名
  2.`rgb`或`rgba`
  3.`HEX`或`HEXA`(16进制)
  4.`HSL`或`HSLA`
  ```

* 举例

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
  	<meta charset="UTF-8">
  	<meta http-equiv="X-UA-Compatible" content="IE=edge">
  	<meta name="viewport" content="width=device-width, initial-scale=1.0">
  	<title>文本颜色</title>
  	<style>
  		/* 
  			文本颜色就是 color
  		*/
  		.test1 {
  			color: red;
  		}
  		.test2 {
  			color:rgb(255, 0, 0)
  		}
  		.test3 {
  			color: #f00;
  		}
  		.test4 {
  			color:hsl(0, 100%, 50%)
  		}
  	</style>
  </head>
  <body>
  	<p class="test1">学无止境！</p>
  	<p class="test2">学无止境！</p>
  	<p class="test3">学无止境！</p>
  	<p class="test4">学无止境！</p>
  </body>
  </html>
  ```

### 文本间隔

```sh
字母间距
letter-spacing

单词间距
word-spacing(通过空格识别单词)

属性值为像素(px),正值让间距增大，负值让间距缩小。负到一定程度字母会叠加在一起。
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>文本间距</title>
	<style>
		p {
			font-size: 30px;
		}
		p:nth-of-type(2){
			/* 
			字母之间的间隔，包括汉字
			*/
			letter-spacing: 20px;
		}
		p:nth-of-type(3){
			/* 
			单词之间的间隔，
			以空格来区分是不是单词

			由于中文句子之间一般没有空格，所以可以理解为对中文不起作用，实际上是按照空格
			*/
			word-spacing: 20px;
		}

		/* 属性值为像素(px),正值让间距增大，负值让间距缩小。负到一定程度字母会叠加在一起。 */
	</style>
</head>
<body>
	<p>
		Lorem ipsum dolor sit amet consectetur adipisicing elit.学无止境！
	</p>
	<p>
		Lorem ipsum dolor sit amet consectetur adipisicing elit.学无止境！
	</p>
	<p>
		Lorem ipsum dolor sit amet consectetur adipisicing elit.学无 止境！
	</p>
</body>
</html>
```

### 文本修饰

* 复合属性名:`text-decoration`

* 属性值：

  ```sh
  三组属性值，没有顺序要求
  1.线的位置
  none 没有线
  underline 下划线
  overline   上划线
  line-through 删除线
  
  2.线的样式
  solid   实线
  dotted  虚线
  wavy    波浪线
  double  双线
  
  3.线的颜色
  ```

* 举例

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
  	<meta charset="UTF-8">
  	<meta http-equiv="X-UA-Compatible" content="IE=edge">
  	<meta name="viewport" content="width=device-width, initial-scale=1.0">
  	<title>文本修饰</title>
  	<style>
  		/* 什么是文本修饰,就是类似于上划线、下划线、删除线等等操作 */
  		body{
  			font-size: 40px;
  		}
  		/* 
  		属性名：
  			文本--修饰（没有顺序上的要求）
  			text-decoration:线的位置 线的样式 线的颜色
  		属性值：
  			线的位置：
  				overline  上划线
  				underline 下划线
  				line-through 删除线
  				none       没有线
  			线的样式：
  				dotted 虚线
  				wavy   波浪线
  				solid  实线
  				double 双线
  			线的颜色：
  				哪种颜色表示都可以
  		*/
  		p:nth-of-type(1){
  			/* 上划线 */
  			text-decoration: overline dotted green;
  		}
  		p:nth-of-type(2){
  			/* 下划线 */
  			text-decoration: red wavy underline ;
  		}
  		p:nth-of-type(3){
  			/* 删除线 */
  			text-decoration: line-through yellow double;
  		}
  		a[aoe]{
  			text-decoration: none; 
  		}
  	</style>
  </head>
  <body>
  	<h1>什么是文本修饰?</h1>
  	<p>上划线</p>
  	<p>下划线</p>
  	<p>删除线</p>
  	<a href="#" aoe="999">好好学习</a>
  	<!-- 自带下划线的文本 -->
  	<ins>我的文本有下划线</ins>
  	<!-- 自带删除线的文本 -->
  	<del>我的文本有删除线</del>
  </body>
  </html>
  ```

### 文本缩进

* 属性名：`text-indent`

  ```sh
  text-indent 属性能定义一个块元素首行文本内容之前的缩进量。
  ```

  

* 属性值：`css`中的长度单位

* 举例：

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
  	<meta charset="UTF-8">
  	<meta http-equiv="X-UA-Compatible" content="IE=edge">
  	<meta name="viewport" content="width=device-width, initial-scale=1.0">
  	<title>Document</title>
  	<style>
  		body {
  			font-size: 20px;
  		}
  		/* 
  			文本-缩进
  			text-indent:像素;
  
  			根据文字大小，计算缩进，
  			等到以后学习了其他长度单位会有另一种动态改变的方法
  			
  		*/
  		div {
  			/* 首行缩进2格，由于文字大小是20px，所以首行缩进2格就是40px */
  			text-indent: 40px;
  		}
  	</style>
  </head>
  <body>
  	<div>对于程序员，英语比数学更重要！！对于程序员，英语比数学更重要！！对于程序员，英语比数学更重要！！对于程序员，英语比数学更重要！！对于程序员，英语比数学更重要！！对于程序员，英语比数学更重要！！对于程序员，英语比数学更重要！！对于程序员，英语比数学更重要！！对于程序员，英语比数学更重要！！对于程序员，英语比数学更重要！！对于程序员，英语比数学更重要！！对于程序员，英语比数学更重要！！对于程序员，英语比数学更重要！！对于程序员，英语比数学更重要！！对于程序员，英语比数学更重要！！</div>
  </body>
  </html>
  ```

### 文本对齐_水平

* 属性名：`text-align`

* 常用属性值：

  ```sh
  left
  行内内容向左侧边对齐。
  
  right
  行内内容向右侧边对齐。
  
  center
  行内内容居中。
  
  justify
  文字向两侧对齐，对最后一行无效。
  ```

* 举例

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
  	<meta charset="UTF-8">
  	<meta http-equiv="X-UA-Compatible" content="IE=edge">
  	<meta name="viewport" content="width=device-width, initial-scale=1.0">
  	<title>文本对齐_水平</title>
  	<style>
  		div {
  			font-size: 40px;
  			background-color: orange;
  			text-align: center;
  		}
  		/*
  			文本 - 排列
  			text-align
  			text-align 并不控制块元素自己的对齐，只控制它的行内内容的对齐。
  
  			属性值：
  			start
  			如果内容方向是左至右，则等于left，反之则为right。
  
  			end
  			如果内容方向是左至右，则等于right，反之则为left
  
  			left
  			行内内容向左侧边对齐。
  
  			right
  			行内内容向右侧边对齐。
  
  			center
  			行内内容居中。
  
  			justify
  			文字向两侧对齐，对最后一行无效。
  
  			justify-all
  			和 justify 一致，但是强制使最后一行两端对齐。
  
  			match-parent
  			和inherit类似，区别在于start和end的值根据父元素的direction确定，并被替换为恰当的left或right。
  		*/
  	</style>
  </head>
  <body>
  	<div>学无止境！</div>
  </body>
  </html>
  ```

### 细说font-size

```sh
总结：
1.由于字体设计原因，文字最终呈现的大小，并不一定与font-size的值一致，可能大，也可能小。
例如：font-size设为40px，最终呈现的文字，可能比40px大，也可能比40px小

2.通常情况下，文字想对于字体设计框，并不是垂直居中的，通常都靠下一些
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>细说font-size</title>
	<style>
		/* 
			通过观察我们发现，字体与顶部和底部会有默认的间距，
			这是字体设置时留下的东西，参考字体设置理念，字体会有一个字体设计框，font-size调整的就是这个框的高度
			宽度会随着框的高度自适应

			字体设置一般以小写字母x为基准，
			基线(可以在mdn搜索)与x的下边缘平切

			总结：
			1.由于字体设计原因，文字最终呈现的大小，并不一定与font-size的值一致，可能大，也可能小。
			例如：font-size设为40px，最终呈现的文字，可能比40px大，也可能比40px小

			2.通常情况下，文字想对于字体设计框，并不是垂直居中的，通常都靠下一些
		
		*/
		div {
			font-size: 40px;
		}
	</style>
</head>
<body>
	<div>
		好好学习x
	</div>

	<span style="font-size: 40px;font-family:'微软雅黑'">尚</span>
	<span style="font-size: 40px;font-family:'华文彩云'">尚</span>
</body>
</html>
```

### 行高

* 属性名：`line-height`

  ```sh
  line-height CSS 属性用于设置多行元素的空间量，如多行文本的间距。对于块级元素，它指定元素行盒（line boxes）的最小高度。对于非替代的 inline 元素，它用于计算行盒（line box）的高度。
  ```

* 可选值

  ```sh
  1.normal
  由浏览器根据文字大小决定一个默认值
  
  2.像素px，或其他长度u单位
  
  3.数字：参考自身`font-size`的倍数(推荐)
  
  4.百分比：参考自身`font-size`的百分比
  ```

* 备注

  ```sh
  由于字体设计原因，文字在一行中，并不是绝对居中，若一行中都是文字，不会太影响观感。
  ```

* 举例

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
  	<meta charset="UTF-8">
  	<meta http-equiv="X-UA-Compatible" content="IE=edge">
  	<meta name="viewport" content="width=device-width, initial-scale=1.0">
  	<title>行高</title>
  	<style>
  		/* 
  			行高，控制每一行的高度
  			属性：
  			line-height
  		
  		*/
  		/* 
  			根据字体的知识，由于字体设计的原因，字体有上下间距，还会有超出字体框的现象
  
  			font-size是字体框高度，line-height控制的是文字所在行的高度，如果行高和文字大小一样，那么由于字体设计的原因，就会出现字体重叠
  			因为超出字体框的部分会压到下一行，会发现文字超出了行高区域
  		*/
  		/* 
  			结论：line-height 不要与 font-size一样，且应该大于font-size
  		*/
  		#d1 {
  			font-size: 40px;
  			background-color: skyblue;
  			line-height: 100px;
  		}
  		/* 
  			如果不写 line-height等价于 line-height:normal
  
  			浏览器会根据我们的字体给我们一个合适的行高，刚好让字体不超出
  		*/
  		#d2 {
  			font-size: 40px;
  			background-color: rgb(192, 235, 135);
  			line-height: normal;
  		}
  		/* 
  			当line-height的值为数字时，就是font-size的倍数，例如
  			line-height:1 <=> line-height:1*font-size
  		
  			一般来说行高在 1.5～2 之间合适
  
  			这个是最常用的，也是mdn推荐的
  		*/
  		#d3{
  			font-size: 40px;
  			background-color: rgb(235, 135, 160);
  			line-height: 1;
  		}
  		/* 
  			当line-height的值为百分数时，就是font-size的倍数，例如
  			line-height:200% <=> line-height:200%*font-size
  		*/
  		#d4{
  			font-size: 40px;
  			background-color: rgb(235, 135, 160);
  			line-height: 125%;
  		}
  	</style>
  </head>
  <body>
  	<div id="d1">loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!</div>
  	<div id="d2">loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!</div>
  	<div id="d3">loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!</div>
  	<div id="d4">loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!</div>
  </body>
  </html>
  ```

#### 行高注意事项

* 总结

  ```sh
  1."line-height"过小会怎样？
  文字会产生重叠，且最小值是0,不能为负数
  
  2."line-height"是可以继承的，且为了能更好的呈现文字，最好写数值
  
  3."line-height"和"height"的关系？
  # 设置了height，那么高度就是height的值
  # 不设置height的时候，会根据line-height*行数计算高度
  ```

* 应用场景

  ```sh
  1.对于多行文字：控制行与行之间的距离
  2.对于单行文字：让"height"等于"line-height",可以实现文字垂直居中。
  ```

* 备注

  ```sh
  由于字体设计原因，文字在一行中，并不是绝对的垂直居中，若一行中都是文字，不会太影响观感。
  ```

* 举例

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
  	<meta charset="UTF-8">
  	<meta http-equiv="X-UA-Compatible" content="IE=edge">
  	<meta name="viewport" content="width=device-width, initial-scale=1.0">
  	<title>行高_注意事项</title>
  	<style>
  		/* 
  			像素类型的行高，我们调整行高，从 60px往 0 px调
  			
  			最终：
  			1.多行文字全部都重叠在一起了
  			2.背景色消失了   --在注意点4讲
  			3.文字整体向上偏移了
  		
  
  			针对第一条：
  			行高大，文字垂直间距大;行高小，文字垂直间距小;行高0,文字垂直间距0
  
  			针对第三条
  			因为文字的字体大小不变，文字中心位置和行高中心位置大抵一致，所以会出现整体向上偏移的情况，实际上是中心上移了
  		*/
  		/* 注意点1:行高过小？--- 文字重叠，且最小值是0,不能为负数，一切不符合规范的行高都会变成 line-height:normal */
  		#d1 {
  			font-size: 40px;
  			background-color: skyblue;
  			line-height: 60px;
  		}
  		/* 
  			div#d2是父，span是子，行高被继承了
  			span字体特别大的时候，就产生了遮挡，于是我们需要给span加行高
  
  			最终span所在行的行高变成了150px，因为行高由一行当中行高最高的来决定
  			默认大文字和小文字以基线对齐，输入一个x就知道了
  
  			注意点2：行高是可以继承的，
  			如果我们以像素书写，那么继承后需要对应修改，如果写数字就很少需要修改了
  		*/
  		#d2 {
  			font-size: 40px;
  			background-color: skyblue;
  			/* line-height: 60px; */
  
  			line-height: 1.5;
  		}
  		#d2 span {
  			font-size: 100px;
  			color: red;
  			/* line-height: 150px; */
  		}
  		/* 
  		注意点3
  			line-height 与 height 的关系
  			设置了height属性，高度就是height的值
  			没有设置height，高度就是行高*行数
  		*/
  		#d3 {
  			font-size: 40px;
  			background-color: yellowgreen;
  			line-height: 300px;
  			height: 100px;
  		}
  		/* 
  			注意点4
  			没有设置height，高度就是行高*行数，行高为0,所以div高度就是0
  			这也是背景色消失的原因，因为高度为0
  		*/
  		#d4 {
  			font-size: 40px;
  			background-color: blue;
  			line-height: 0px;
  			
  		}
  
  		/* 
  			总结：行高的应用场景
  			1.调整多行文字的间距 
  				因为行与行之间贴着，而字体在行偏中的文字，大小不变，就实现了间距
  			2.单行文字的垂直居中
  				当line-height和height一样时就实现了单行垂直居中，多行时不能用
  				多行时第一行整个垂直居中，其他行就出去了
  		
  		
  		*/
  	</style>
  </head>
  <body>
  		<div id="d1">loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!</div>
  		<div id="d2">loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!<span>loser</span>从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!</div>
  		<div id="d3">loser从不存在!loser从不存在!</div>
  		<div id="d4">loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!loser从不存在!</div>
  </body>
  </html>
  ```

### 文本对齐_垂直

```sh
1.顶部：无需任何属性，在垂直方向上，默认就是顶部对齐。

2.居中：对于单行文字，让height=line-height即可
多行文字垂直居中用定位实现

3.底部：对于单行文字，目前的临时方案
line-height = (height*2) - (font-size) - x

备注：x是根据字体族，动态决定的一个值，根据字体族
```

>问题

```sh
垂直方向上的底部对齐，更好的解决办法是什么？
-- 后期使用定位实现
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>文本对齐_垂直</title>
	<style>
		/* 
			可以通过行高来挪动字体，因为字体是在行高偏中间的位置，

			1.顶部：无需任何属性，在垂直方向上，默认就是顶部对齐。

			2.居中：对于单行文字，让height=line-height即可
			多行文字垂直居中用定位实现

			3.底部：对于单行文字，目前的临时方案
			line-height = (height*2) - (font-size) - x

			备注：x是根据字体族，动态决定的一个值
		*/
		div {
			font-size: 40px;
			height: 400px;
			background-color: skyblue;
			line-height:750px ;
		}
		
	</style>
</head>
<body>
	<div>好好学习</div>
</body>
</html>
```

### vertical-align

**`vertical-align`** 用来指定行内元素（inline）或表格单元格（table-cell）元素的垂直对齐方式。

>注意

vertical-align 属性可被用于两种环境：

- 使行内元素盒模型与其行内元素容器垂直对齐。例如，用于垂直对齐一行文本内的图片
- 垂直对齐表格单元内容。

注意 `vertical-align` 只对行内元素、行内块元素和表格单元格元素生效：不能用它垂直对齐[块级元素](https://developer.mozilla.org/zh-CN/docs/Glossary/Block-level_content)。

>语法

```css
/* Keyword values */
vertical-align: baseline;
vertical-align: sub;
vertical-align: super;
vertical-align: text-top;
vertical-align: text-bottom;
vertical-align: middle;
vertical-align: top;
vertical-align: bottom;

/* <length> values */
vertical-align: 10em;
vertical-align: 4px;

/* <percentage> values */
vertical-align: 20%;

/* Global values */
vertical-align: inherit;
vertical-align: initial;
vertical-align: unset;
```

#### 值的分类

#### 相对父元素的值

这些值使元素相对其父元素垂直对齐：

- `baseline`

  使元素的基线与父元素的基线对齐。HTML 规范没有详细说明部分[可替换元素](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Replaced_element)的基线，如[``](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/textarea) ，这意味着这些元素使用此值的表现因浏览器而异。

- `sub`

  使元素的基线与父元素的下标基线对齐。

- `super`

  使元素的基线与父元素的上标基线对齐。

- `text-top`

  使元素的顶部与父元素的字体顶部对齐。

- `text-bottom`

  使元素的底部与父元素的字体底部对齐。

- `middle`

  使元素的中部与父元素的基线加上父元素 x-height（译注：[x 高度](https://www.zhangxinxu.com/wordpress/2015/06/about-letter-x-of-css/)）的一半对齐。

- 长度单位

  使元素的基线对齐到父元素的基线之上的给定长度。可以是负数。

- 百分比

  使元素的基线对齐到父元素的基线之上的给定百分比，该百分比是[`line-height`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/line-height)属性的百分比。可以是负数。

#### 相对行的值

下列值使元素相对整行垂直对齐：

- `top`

  使元素及其后代元素的顶部与整行的顶部对齐。

- `bottom`

  使元素及其后代元素的底部与整行的底部对齐。

没有基线的元素，使用外边距的下边缘替代。

#### 总结

* 属性名：`vertical-align`

* 作用：用于指定同一行元素之间，或表格单元格内文字的垂直对齐方式。

* 常用值：

  ```sh
  baseline
  默认值
  使元素的基线与父元素的基线对齐
  
  top
  使元素的顶部与其所在行的顶部对齐
  
  middle
  使元素的中部与父元素的基线加上父元素字母x的一半对齐整
  
  bottom
  使元素的底部与其所在行的底部对齐
  ```

* 注意事项

  ```sh
  1.该属性只能给父元素的子元素加
  2.该属性不能控制块级元素
  3.直接用在表格单元格上可以控制文字位置，不受基线影响，实现真正的居中
  ```

* 举例

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
  	<meta charset="UTF-8">
  	<meta http-equiv="X-UA-Compatible" content="IE=edge">
  	<meta name="viewport" content="width=device-width, initial-scale=1.0">
  	<title>vertical-align</title>
  	<style>
  		/* 
  			vertical-align 
  			用来指定行内元素（inline）或表格单元格（table-cell）元素的垂直对齐方式。
  
  			默认以基线对齐,即x的底线
  
  			常用值：
  			top 贴到顶端
  			bottom 贴到底部
  			baseline 基线，默认值
  			middle   找到父元素的中心点
  		*/
  		div {
  			font-size: 100px;
  			height: 300px;
  			background-color: skyblue;
  		}
  		div span{
  			font-size: 40px;
  			background-color: orange;
  			vertical-align: top;
  		}
  		img{
  			height: 30px;
  			vertical-align: middle;
  			/* 
  				当图片高度小于文字时，图片动
  				当图片高度大于文字时，文字动
  			*/
  		}
  		.test{
  			width: 400px;
  			height: 400px;
  			background-color: green;
  			vertical-align: bottom;
  			/* 
  				无效，
  				注意事项：
  				该属性只能给父元素的子元素加
  			*/
  		}
  		.test1{
  			width: 400px;
  			height: 400px;
  			background-color: gray;
  		}
  		.test2{
  			width: 100px;
  			height: 100px;
  			background-color: green;
  			vertical-align: top;
  			/* 
  				无效：注意事项2
  				该属性不能控制块级元素
  			*/
  		}
  		.san{
  			vertical-align: middle;
  			/* 
  				有用：
  				直接用在表格单元格上可以控制文字位置
  			*/
  		}
  	</style>
  </head>
  <body>
  	<div>
  		justMex<span>x我就是我</span>
  	</div>
  	<hr/>
  	<div>
  		图片x<img src="xxx"/>
  	</div>
  	<hr/>
  	<div class="test">
  		123
  	</div>
  	<hr/>
  	<div class="test1">
  		<div class="test2">
  
  		</div>
  	</div>
  	<hr/>
  	<table border="1" cellspacing="0">
  		<caption>人员信息</caption>
  		<thead>
  			<tr>
  				<td>姓名</td>
  				<td>年龄</td>
  				<td>性别</td>
  			</tr>
  		</thead>
  		<tbody>
  			<tr height="200">
  				<td class="san">张三</td>
  				<td>18</td>
  				<td>男</td>
  			</tr>
  			<tr>
  				<td>李四</td>
  				<td>19</td>
  				<td>男</td>
  			</tr>
  		</tbody>
  	</table>
  </body>
  </html>
  ```

## Css列表相关的属性

可以作用在ul、li、ol上

```sh
list-style-type
设置列表符号

list-style-position
设定列表符号的位置

list-style-image 
自定义列表符号，参数为图片地址

list-style
符合属性，没有数量位置的要求
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>列表相关属性</title>
	<style>
		ul {
			/* 
				list-style-type
				列表符号的样式，默认是个小黑点

				none 没有符号，常用，因为不想用默认样式
				square 方块
				low-roman 小写罗马数
				upper-roman 大写罗马数字
				decimal 列表符号变成数字
			*/
			list-style-type:decimal;
			/* 
				list-style-position
				列表符号的位置，相对li
				inside 里面
				outside 外面
			*/
			list-style-position: inside;
			/* 
				list-style-image
				自定义列表符号
				对图片大小有要求
			*/
			/* list-style-image:url(路径); */

			/* 
				list-style
				复合属性，没有顺序要求，上面的几种属性随便写，空格隔开
			*/
			/* list-style: decimal inside url(路径); */
		}
		li {
			background-color: orange;
		}
		/* 
			list-style-xxx
			可以用在ul、li、ol身上
		*/
	</style>
</head>
<body>
	<ul>
		<li>《西游记》</li>
		<li>《水浒传》</li>
		<li>《三国演义》</li>
		<li>《红楼梦》</li>
	</ul>
</body>
</html>
```

## Css表格相关属性

### 边框相关属性

>边框相关属性

```sh
border-width
边框宽度

border-color
边框颜色

border-style
边框风格
none 无边框 solid 实线 dashed 虚线 dotted 点线 double 双实线

border
边框复合属性
没有数量、顺序的要求
```

>注意

```sh
边框相关的属性不仅仅只有表格能用，其他元素也都能用
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>表格边框</title>
	<style>
		table {
			/* 
				边框宽度
				border-width
				边框颜色
				border-color
				边框线的样式 solid 实线 dashed 虚线 dotted 点线 double 双线
				border-style
				以上三种都要写，才会出现边框

				复合属性,没有顺序要求
				border:1px solid green;

			*/
			border: 1px solid green;
		}
		/* 单元格 */
		td{
			border: 1px double yellow;
		}
		/* 
			选中标签加属性即可，也可以配合其他自定义的选择器使用
		*/
		.san{
			border: 1px dotted red;
		}
		/* 
			边框相关的属性不仅仅只有表格能用，其他元素也都能用
		*/
	</style>
</head>
<body>
	<table>
		<caption>人员信息</caption>
		<thead>
			<tr>
				<td>姓名</td>
				<td>年龄</td>
				<td>性别</td>
				<td>个人价值</td>
			</tr>
		</thead>
		<tbody>
			<tr>
				<td>张三</td>
				<td>18</td>
				<td class="san">男</td>
				<td>很有价值</td>
			</tr>
			<tr>
				<td>李四</td>
				<td>19</td>
				<td>男</td>
				<td>吸血鬼</td>
			</tr>
			<tr>
				<td>王五</td>
				<td>21</td>
				<td>男</td>
				<td>战士</td>
			</tr>
		</tbody>
	</table>
</body>
</html>
```

### 独有属性

只有表格标签才能使用

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>表格独有属性</title>
	<style>
		table {
			border: 1px solid green;
			width: 200px;
			/* 
				独有
				table-layout
				控制表格的宽度
				auto 自动
				fixed 都一样宽

				用了fixed后仍然可以直接去找对应行或列，利用width设置宽度
			*/
			table-layout: auto;
			/* 
				独有
				控制单元格间距
				border-spacing

				生效前提：不能合并边框
			*/
			border-spacing: 0px;
			/* 
				独有
				border-collapse
				合并相邻单元格的边框
				separate 不合并，默认
				collapse 合并

				注意:
				1.一旦合并了单元格的边框，单元格间距将不再生效
				2.表格外边框颜色会被与他合并的单元格边框颜色覆盖

			*/
			border-spacing: collapse;
			/* 
				独有
				empty-cells
				隐藏没有内容的单元格
				show 展示
				hide 隐藏

				验证：我们发现他的边框不见了
			*/
			empty-cells:hide;
			/* 
				独有
				caption-side
				设置表格标题的位置
				top 表格的标题在表格上方
				bottom 表格的标题在表格的下方
			*/
			caption-side: bottom;
		}
		td,th{
			border: 1px solid orange;
		}
	</style>
</head>
<body>
	<!-- 
		rowspan 跨行
		colspan 跨列
		这两个属性只能通过html使用，无法使用css实现
	 -->
	<table>
		<caption>人员信息</caption>
		<thead>
			<tr>
				<td>姓名</td>
				<td>年龄</td>
				<td>性别</td>
				<td>个人价值</td>
			</tr>
		</thead>
		<tbody>
			<tr>
				<td>张三</td>
				<td>18</td>
				<td>男</td>
				<td>很有价值</td>
			</tr>
			<tr>
				<td>李四</td>
				<td>19</td>
				<td>男</td>
				<td>吸血鬼</td>
			</tr>
			<tr>
				<td>王五</td>
				<td>21</td>
				<td>男</td>
				<td>战士</td>
			</tr>
			<tr>
				<td></td>
				<td>21</td>
				<td>男</td>
				<td>医生</td>
			</tr>
		</tbody>
	</table>
</body>
</html>
```

>注意

```sh
我们完全可以通过其他选择器选中某个位置，然后添加其他css样式
```

## Css背景相关的属性

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>背景相关的属性</title>
	<style>
		div {
			width: 400px;
			height: 400px;
			border:2px solid black;
			font-size: 40px;
			/* 
			设置背景色
			1.color的写法都接受
			2.不写的话，默认值为transparent 透明的
			*/
			background-color: skyblue;
			/* 
				设置背景图片
				1.背景颜色会被背景图片压住
				2.内容会在背景上方

				图片的默认展示
				1.小图不够宽高，就会多个铺满 --常用这个平铺特性来实现纹理
				2.大图宽高太大，就只会展示一部分

				路径可以加引号，也可以不加
			*/
			background-image: url(路径);

			/* 
				background-repeat
				设置背景图片的重复方式
				repeat 默认值，允许重复
				no-repeat 不重复
				repeat-x 只在水平方向上重复
				repeat-y 只在垂直方向上重复
			*/
			background-repeat: no-repeat;

			/* 
				background-position
				设置背景图片的位置--写法1:用关键词
				常见位置描述词：x轴 left center right
											y轴 top center bottom
				如果只写一个,他会根据写的内容判断是水平还是垂直，另一个补center

				background-position:水平位置 垂直位置;
			*/
			background-position:left top;

			/* 
				background-position
				设置背景图片的位置--写法2:用具体的像素
				background-position:水平位置 垂直位置;
				图片左上角相对于容器左上角,x轴往左为正，y轴往下为正。

				只写一个就是x轴，y轴默认为中间
			*/
			background-position:10px 100px;

			/* 
				复合属性
				不挑顺序

				有个小坑，复合属性即使没写背景色，也会使用 transparent
				那就会覆盖写在他之前的外面的背景色--解决方案，把背景色写他后面

				当然完全可以写在他里面
			*/
			background:url(路径) no-repeat 100px 300px;
			background-color: red;
		}
	</style>
</head>
<body>
	<div>好好学习</div>
</body>
</html>
```

## Css鼠标相关属性

>小结

```sh
属性名：cursor

作用：改变鼠标样式

常用属性值：
pointer 小手
move 移动图标
text 文字选择器
crosshair 十字架
wait 等待
help 帮助
```

>自定义鼠标样式

```sh
url(图片路径),pointer

# 一定要在后面加pointer才生效
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>鼠标相关的属性</title>
	<style>
		div {
			width: 400px;
			height: 400px;
			background-color: orange;
			/* 
				cursor
				鼠标属性，有非常多的属性

				pointer 小手
				move  拖动
				wait  转圈等待
				crosshair 十字架
				help 小问号
				url(路径),pointer 自定义鼠标光标
			*/
		}
		input {
			cursor: pointer;
		}
	</style>
</head>
<body>
	<div>
		鼠标进来试试
		<input type="text">
		<a href="#">百度</a>
	</div>
</body>
</html>
```

## Css盒子模型

### 常用的长度单位

```sh
"px"
像素

"em"
相对当前元素的font-size(本身没有就用继承的)

"rem"
相对根字体大小，html标签就是根。

"%"
相对父元素计算
```

>注意：

```sh
CSS中设置长度，必须加单位，否则样式无效。
```

### 元素的显示模式

#### 块元素（block）

```sh
又称：块级元素
特点：
1.在页面中独占一行，不会与任何元素共用一行，是从上到下排列的。
2.默认宽度：撑满父元素
3.默认高度：由内容撑开
4.可以通过Css设置宽高
```

#### 行内元素（inline）

```sh
又称：内联元素
特点：
1.在页面中不独占一行，一行中不能容纳下的行内元素，会在下一行继续从左到右排列
2.默认宽度：由内容撑开。
3.默认高度：由内容撑开
4.无法通过css设置宽高
```

#### 行内块元素（inline-block）

```sh
又称：内联块元素
特点：
1.在页面中不独占一行，一行中不能容纳下的行内元素，会在下一行继续从左到右排列。
2.默认宽度：由内容撑开。
3.默认高度：由内容撑开
4.可以通过css设置宽高
```

注意：

```sh
元素早期只分为：行内元素和块级元素，区分条件也只有一条："是否独占一行"，如果按照这种分类方式，汗内块元素应该算作行内元素。
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>元素的显示模式</title>
	<style>
		#d1{
			background-color: aqua;
		}
		#d2{
			background-color: red;
		}
		#d3{
			background-color: blue;
		}
		span {
			background-color: blueviolet;
			margin-left: 10px;
		}
	</style>
</head>
<body>
	<!-- 
		块元素
		1.在页面中独占一行，不会与任何元素共用一行，是从上到下排列的。
		2.默认宽度：撑满父元素
		3.默认高度：由内容撑开
		4.可以通过Css设置宽高
	 -->
	<div id="d1">山回路转不见君</div>
	<div id="d2">雪上空留马行处</div>
	<div id="d3">风雨中我等你，风雨中我等你风雨中我等你风雨中我等你风雨中我等你风雨中我等你风雨中我等你风雨中我等你风雨中我等你风雨中我等你风雨中我等你风雨中我等你风雨中我等你</div>
	 <hr>
	<!-- 
		行内元素
		又称：内联元素特点：
		1.在页面中不独占一行，一行中不能容纳下的行内元素，会在下一行继续从左到右排列
		2.默认宽度：由内容撑开。
		3.默认高度：由内容撑开
		4.无法通过css设置宽高
	 -->
	 <span>你好</span><span>你好</span><span>你好</span><span>你好</span><span>你好</span><span>你好</span><span>你好</span><span>你好</span><span>你好</span><span>你好</span><span>你好</span><span>你好</span><span>你好</span><span>你好</span><span>你好</span><span>你好</span><span>你好</span>
	 <hr>
	 <!-- 
			行内块元素
			又称：内联块元素
			特点：
			1.在页面中不独占一行，一行中不能容纳下的行内元素，会在下一行继续从左到右排列。
			2.默认宽度：由内容撑开。
			3.默认高度：由内容撑开
			4.可以通过css设置宽高
	  -->
		<img src="xxx.png" alt="">
</body>
</html>
```

#### 总结各元素的显示模式

* 块元素

  >主体结构标签

  ```html
  <html> <body>
  ```

  >排版标签

  ```html
  <h1>-<h6>、<hr> 、<p>、<pre>、<div>
  ```

  >列表标签

  ```html
  <ul>、<ol>、<li>、<dl>、<dt>、<dd> 
  ```

  >表格相关标签

  ```html
  <table>、<tbody>、<thead>、<tfoot>、<tr>、<caption>
  ```

  >其他

  ```html
  <form> 与 <option>
  ```

* 行内元素

  >文本标签

  ```html
  <br>、<em>、<strong>、<sup>、<sub>、<del>、<ins>、<span>
  ```

  >其他

  ```html
  <a>、<label>
  ```

* 行内块元素

  >图片

  ```html
  <img>
  ```

  >单元格

  ```html
  <td>、<th>
  ```

  >表单控件

  ```html
  <input>、<textarea>、<select>、<button>
  ```

  >框架标签

  ```html
  <iframe>
  ```

##### 修改元素的显示模式

给元素设置dispaly属性

```css
/*设置为块元素*/
display:block

/*设置为行内元素*/
display:inline

/*设置为行内块元素*/
display:inline-block

/*不要显示模式--不显示，即隐藏*/
dispaly:none
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>修改元素的显示模式</title>
	<style>
		div {
			width: 200px;
			height: 200px;
			font-size: 20px;
			/* 设置显示模式 */
			/* 块级元素 */
			/* display: block; */

			/* 行内块元素 */
			/* display: inline-block; */

			/* 行内元素 */
			display: inline;

			/* 不显示，可以理解为没有显示模式*/
			/* display: none; */
		}
		#d1{
			background-color: skyblue;
		}
		#d2 {
			background-color: orange;
		}
		#d3 {
			background-color: blueviolet;
		}
	</style>
</head>
<body>
	<div id="d1">你好1</div>
	<div id="d2">你好2</div>
	<div id="d3">你好3</div>
</body>
</html>
```

### 盒子模型的组成部分

```sh
从内到外：

内容区 content
内边据 padding，又称补白
边框  border
外边距 margin
```

>解释

```sh
Css会把所有html标签都当作盒模型，即把所有的HTML元素都看成一个盒子，所有的样式都是基于这个盒子
```

```sh
1.margin 外边距
盒子与外界的距离

2.border 边框
盒子的边框

3.padding 内边距
紧贴内容的补白区域

4.content 内容
元素中的文本或后代元素都是他的内容
```

```sh
盒子的大小 = content + padding + border
```

>注意

外边距`margin`不会影响盒子的大小，但会影响盒子的位置。

### 盒子的内容区域

#### 宽度自适应

```html
<style>
    div {
        /* 
            div是一个块级元素，当不设宽的时候会撑满父元素
            由于目前父容器是body，我们这里的body又撑满了整个视口
            所以div也就撑满了视口
        */
        height: 200px;
        background-color: aqua;
    }
</style>
</head>
<body>
<div>Lorem ipsum dolor sit amet consectetur adipisicing elit. Amet, commodi!</div>
</body>
```

随着视口的变化，div的宽度跟着变化

#### 锁定宽/高

```html
<style>
		#d1{
			/* 
				div是一个块级元素，当不设宽的时候会撑满父元素
				由于目前父容器是body，我们这里的body又撑满了整个视口
				所以div也就撑满了视口
			*/
			height: 200px;
			background-color: aqua;
		}

		#d2 {
			/* 
				设定了宽度后，宽度就固定了，一旦父元素宽度小于给定宽度
				就会出现滚动条

				大于给定宽度，就完整呈现，但是不会跟随父级宽度
			*/
			width: 800px;
			height: 200px;
			background-color: blue;
		}
	</style>
</head>
<body>
	<div id="d1">Lorem ipsum dolor sit amet consectetur adipisicing elit. Amet, commodi!</div>

	<div id="d2">
		Lorem ipsum, dolor sit amet consectetur adipisicing elit. Provident maxime distinctio obcaecati dicta labore eligendi, laborum aut facilis voluptatum illum porro quam blanditiis officia. Nemo eos ex nesciunt assumenda officiis.
	</div>
</body>
```

当宽度给定时，一旦父级宽度小于该宽度，就会出现滚动条

#### 最小宽/高

```html
	<style>
		#d1{
			/* 
				div是一个块级元素，当不设宽的时候会撑满父元素
				由于目前父容器是body，我们这里的body又撑满了整个视口
				所以div也就撑满了视口
			*/
			height: 200px;
			background-color: aqua;
		}

		#d2 {
			/* 
				设定了宽度后，宽度就固定了，一旦父元素宽度小于给定宽度
				就会出现滚动条

				大于给定宽度，就完整呈现，但是不会跟随父级宽度
			*/
			width: 800px;
			height: 200px;
			background-color: blue;
		}
		#d3 {
			/* 
				设定了最小宽度，没有上限，父级>=600px,就和父级一样
				一旦父级小于600px，就不跟随，而是出现滚动条
			*/
			min-width: 600px;
			height:200px;
			background-color: red;
		}
	</style>
</head>
<body>
	<div id="d1">Lorem ipsum dolor sit amet consectetur adipisicing elit. Amet, commodi!</div>

	<div id="d2">
		Lorem ipsum, dolor sit amet consectetur adipisicing elit. Provident maxime distinctio obcaecati dicta labore eligendi, laborum aut facilis voluptatum illum porro quam blanditiis officia. Nemo eos ex nesciunt assumenda officiis.
	</div>
	<div id="d3">
		Lorem, ipsum dolor sit amet consectetur adipisicing elit. Nulla omnis, voluptatem accusantium ab odit doloremque perferendis?
	</div>
</body>
```

```sh
"min-width"最小宽度
"min-height"最小高度
没有上限，当父大于给定值的时候，跟随父级变化，小于时出现滚动条
```

#### 最大宽/高

```html
<style>
		#d1{
			/* 
				div是一个块级元素，当不设宽的时候会撑满父元素
				由于目前父容器是body，我们这里的body又撑满了整个视口
				所以div也就撑满了视口
			*/
			height: 200px;
			background-color: aqua;
		}

		#d2 {
			/* 
				设定了宽度后，宽度就固定了，一旦父元素宽度小于给定宽度
				就会出现滚动条

				大于给定宽度，就完整呈现，但是不会跟随父级宽度
			*/
			width: 800px;
			height: 200px;
			background-color: blue;
		}
		#d3 {
			/* 
				设定了最小宽度，没有上限，父级>=600px,就和父级一样
				一旦父级小于600px，就不跟随，而是出现滚动条
			*/
			min-width: 600px;
			height:200px;
			background-color: red;
		}
		#d4 {
			/* 
				设定了最大宽度，没有下限，小于给定值都跟随变化，大于就不跟
				浏览器有个最小宽度 -- 484,每个都不一样
			*/
			max-width: 1000px;
			height: 200px;
			background-color: blueviolet;
		}
	</style>
</head>
<body>
	<div id="d1">Lorem ipsum dolor sit amet consectetur adipisicing elit. Amet, commodi!</div>

	<div id="d2">
		Lorem ipsum, dolor sit amet consectetur adipisicing elit. Provident maxime distinctio obcaecati dicta labore eligendi, laborum aut facilis voluptatum illum porro quam blanditiis officia. Nemo eos ex nesciunt assumenda officiis.
	</div>
	<div id="d3">
		Lorem, ipsum dolor sit amet consectetur adipisicing elit. Nulla omnis, voluptatem accusantium ab odit doloremque perferendis?
	</div>
	<div id="d4">
		Lorem ipsum dolor sit amet consectetur, adipisicing elit. Quia, quos! Velit sequi ad exercitationem quaerat et accusamus numquam dignissimos sed laborum! Voluptatibus velit iure cumque odit molestias eos provident totam?
	</div>
</body>
```

```sh
"max-width"最大宽度
"max-height"最大高度
设置了最大值，没有下限，有上限，超过上限就不再变大

超出的内容不会出现滚动条，而是会直接溢出，即内容区的溢出盒子
```

#### 注意

```sh
"max-width"、"min-width"一般不与"width"一起使用。
"max-height"、"min-height"一般不与"height"一起用
```

#### 关于默认宽度

>margin

```html
<style>
		div {
			height: 200px;
			background-color: aqua;
			/* 
				当div没有给宽度时，撑开父级的宽度 例如1520

				当我们给div加margin后，div与父级就有了距离，挤压了div
				宽度就变为了 1420

				并不是margin改变了div的大小，而是div能撑开的宽度变小了，如果我们不想这样，就需要给div设定个宽度
			*/
			margin: 50px;
		}
	</style>
</head>
<body>
	<div>
		Lorem ipsum, dolor sit amet consectetur adipisicing elit. Reiciendis inventore esse in. Necessitatibus voluptatem in, repellendus facilis praesentium sit alias, quam saepe aperiam voluptatum odio eaque ad omnis quas incidunt.
	</div>
</body>
```

>border与padding

```html
<style>
		div {
			height: 200px;
			background-color: aqua;
			/* 
				当div没有给宽度时，撑开父级的宽度 例如1520

				当我们给div加margin后，div与父级就有了距离，挤压了div
				宽度就变为了 1420

				并不是margin改变了div的大小，而是div能撑开的宽度变小了，如果我们不想这样，就需要给div设定个宽度
			*/
			margin: 50px;
			/* 
				border是盒子的组成部分，现在盒子能撑开的最大宽是1420
				加上边框不会变，那么div就会被挤压，变为 1410
				
				padding同理
			*/
			border: 5px solid #000;

		}
	</style>
</head>
<body>
	<div>
		Lorem ipsum, dolor sit amet consectetur adipisicing elit. Reiciendis inventore esse in. Necessitatibus voluptatem in, repellendus facilis praesentium sit alias, quam saepe aperiam voluptatum odio eaque ad omnis quas incidunt.
	</div>
</body>
```

>总结

所谓默认宽度，就是不设置width属性时，元素所呈现出来的宽度。

```sh
总宽度 = 父的content - 自身的左右margin
内容区的宽度 = 父的content - 自身的左右margin - 自身的左右border-自身的左右padding
```

就是说，当盒子没有设置宽或高时，margin对他们是有影响的

### 盒子的内边距

|   Css属性名    |   功能   |         属性值         |
| :------------: | :------: | :--------------------: |
|  padding-top   | 上内边距 |          长度          |
| padding-right  | 右内边距 |          长度          |
| padding-bottom | 下内边距 |          长度          |
|  padding-left  | 左内边距 |          长度          |
|    padding     | 复合属性 | 长度，可以设置1～4个值 |

`padding`复合属性的使用规则：

1.`padding：10px；`四个方向内边距都是`10px`。

2.`padding：10px 20px；`上下都是`10px`，左右都是`20px`。

3.`padding：10px 20px 30px；`上`10px`，左右`20px`，下`30px`。

4.`padding：10px 20px 30px 40px；`上右下左，顺时针顺序。

```sh
注意点：
1.`padding`的值不能为负数。
2.行内元素的左右内边距是没问题的，上下内边距不能完美的设置。
3.块级元素、行内元素，四个方向内边距都可以完美设置。
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>Document</title>
	<style>
		#d1 {
			width: 400px;
			height: 400px;
			background-color: aqua;

			/* 复合属性 -- 上下左右都是20px */
			/* padding: 20px; */

			/* 复合属性写两个，含义：第一个上下一样  第二个左右一样 */
			/* padding: 10px 20px; */

			/* 复合属性写三个，含义：第一个上  第二个左右 第三个下 */
			/* padding: 10px 5px 20px; */

			/* 复合属性写四个，从上开始，顺时针：上 右 下 左 */
			/* padding: 10px 15px 20px 25px; */

		
			/* 分开设置 */
			/* 上侧内边距 */
			padding-top:10px;
			/* 右侧内边距 */
			padding-right: 20px;
			/* 底部内边据 */
			padding-bottom: 30px;
			/* 左侧内边距 */
			padding-left: 5px;


			/* 注意点 */
			/* 
				1.padding不能为负数，写负数代表未设置
			*/

		}

		span {
			/* 行内元素的padding的注意事项 */
			/* 
				1.行内元素的左右内边距没有问题
				2.行内元素的上下内边距能设置，但是不占位置，就是只是让自己变大，但是不撑开实际宽高，会和其他人叠到一起
			*/
			padding-left: 5px;
			padding-right: 20px;

			padding-bottom: 15px;
			padding-top: 10px;
		}
		/* 总结 */
		/* 
			1.块级元素和行内块元素的padding没问题
			2.行内元素的padding左右正常，上下不实际占位
		*/
	</style>
</head>
<body>
	<div id="d1">你好啊</div>
	<span>我很好</span>
	<div>
		Lorem ipsum dolor sit amet, consectetur adipisicing elit. Aut, aspernatur.
	</div>
</body>
</html>
```

### 盒子的边框

>知识点1

```html
<style>
		div {
			width: 400px;
			height: 400px;
			background-color: aqua;

			/* 
				单独写不生效，需要颜色和样式
			*/
			border-width: 10px;
			/* 
				单独写不生效，需要宽度和样式。
			*/
			border-color: red;
			/* 
				再不设宽度和颜色时，只写这一个属性也能生效
				颜色默认黑色，宽度默认 3px
			*/
			border-style: solid;
		}
	</style>
</head>
<body>
	<div>
		你好啊
	</div>
</body>
```

>整体举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>盒子的边框</title>
	<style>
		#d1 {
			width: 400px;
			height: 400px;
			background-color: aqua;

			/* 
				单独写不生效，需要颜色和样式
			*/
			border-width: 10px;
			/* 
				单独写不生效，需要宽度和样式。
			*/
			border-color: red;
			/* 
				再不设宽度和颜色时，只写这一个属性也能生效
				颜色默认黑色，宽度默认 3px
			*/
			border-style: solid;
		}
		#d2 {
			width: 400px;
			height: 400px;
			background-color: blue;
			/* 复合属性 */
			border: 10px red solid;
		}
		#d3 {
			width: 400px;
			height: 400px;
			background-color: blue;

			/* 边框宽度 */
			border-left-width: 20px;
			border-right-width: 15px;
			border-top-width: 10px;
			border-bottom-width: 5px;

			/* 边框颜色 */
			border-left-color: olive;
			border-right-color: orange;
			border-top-color: blueviolet;
			border-bottom-color: brown;

			/* 边框样式 */
			border-left-style: solid;
			border-top-style: dotted;
			border-right-style: dashed;
			border-bottom-style: double;
		}
		#d4 {
			/* 方向的复合属性 */
			border-left:10px solid red;
			border-right: 20px dotted olive;
			border-top:25px double black;
			border-bottom: 5px dashed blue;
		}
	</style>
</head>
<body>
	<div id="d1">
		你好啊
	</div>
	<div id="d2">
		复合属性
	</div>
	<div id="d3">
		各个方向的属性
	</div>
	<div id="d4">
		各个方向的复合属性
	</div>
</body>
</html>
```

### 盒子的外边距

|   Css属性名   |   功能   |         属性值         |
| :-----------: | :------: | :--------------------: |
|  margin-top   | 上外边距 |          长度          |
| margin-right  | 右外边距 |          长度          |
| margin-bottom | 下外边距 |          长度          |
|  margin-left  | 左外边距 |          长度          |
|    margin     | 复合属性 | 长度，可以设置1～4个值 |

`margin`复合属性的使用规则：

1.`margin：10px；`四个方向内边距都是`10px`。

2.`margin：10px 20px；`上下都是`10px`，左右都是`20px`。

3.`margin：10px 20px 30px；`上`10px`，左右`20px`，下`30px`。

4.`margin：10px 20px 30px 40px；`上右下左，顺时针顺序。

```sh
注意点：
1.`margin`的值不能为负数。
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>盒子的外边距</title>
	<style>
		#d1 {
			width: 400px;
			height: 400px;
			background-color: aqua;
			/* 复合属性 -- 上下左右都是20px */
			/* margin: 20px; */

			/* 复合属性写两个，含义：第一个上下一样  第二个左右一样 */
			/* margin: 10px 20px; */

			/* 复合属性写三个，含义：第一个上  第二个左右 第三个下 */
			/* margin: 10px 5px 20px; */

			/* 复合属性写四个，从上开始，顺时针：上 右 下 左 */
			/* margin: 10px 15px 20px 25px; */

		
			/* 分开设置 */
			/* 上侧外边距 */
			margin-top:10px;
			/* 右侧外边距 */
			margin-right: 20px;
			/* 底部外边据 */
			margin-bottom: 30px;
			/* 左侧外边距 */
			margin-left: 5px;


			/* 注意点 */
			/* 
				1.margin不能为负数，写负数代表未设置
			*/
		}
	</style>
</head>
<body>
	<div id="d1">你好啊</div>
</body>
</html>
```

#### margin的注意事项

##### 事项1

子元素的margin，是参考父元素的content计算的。因为父亲的content中承装着子元素。

>举例

```html
	<style>
		.outer {
			width: 400px;
			height: 400px;
			background-color: gray;

			padding: 50px;
		}

		.inner {
			width: 100px;
			height: 100px;
			background-color: orange;

			/* 从父级的内容区开始算 */
			margin: 100px;
		}
	</style>
</head>
<body>
	<!-- 
		子元素的margin是参考父元素的content计算的。
	 -->
	<div class="outer">
		<div class="inner"></div>
	</div>

</body>
```

##### 事项2

上margin、左margin，影响自己的位置，连带影响下边或右边兄弟的位置。

下margin、右margin，自己不动，影响下边或右边兄弟元素的位置

>举例

```html
<style>
		.box {
			width: 200px;
			height:200px;
		}
		.box1 {
			background-color: skyblue;
		}
		.box2 {
			background-color: orange;
			/* 
			效果：
			box1不动
			box2下移50px
			box3也下移50px

			即动自己，让自己与上方相对50px
			 */
			margin-top: 50px;

			/* 
				效果：
				box1、box2不动
				box3动

				即不动自己，下边的动
			*/
			margin-bottom: 50px;
		}
		.box3 {
			background-color: green;
		}

		/* 行内 */
		.box-I {
			width: 200px;
			height:200px;
			display: inline-block;
		}
		.box4 {
			background-color: red;
		}
		.box5 {
			background-color: yellow;
			/* 
				效果：
				box4不动
				box5、box6动
			*/
			margin-left: 10px;
			/* 
				效果：
				box4、box5不动
				box6动
			*/
			margin-right: 40px;
		}
		.box6 {
			background-color: blue;
		}
	</style>
</head>
<body>
	<div class="box box1">1</div>
	<div class="box box2">2</div>
	<div class="box box3">3</div>

	<hr>

	<div class="box-I box4">1</div>
	<div class="box-I box5">2</div>
	<div class="box-I box6">3</div>

	<!-- 
		总结：
		上margin、左margin 会影响自身和下/右兄弟元素的位置

		下margin会影响下边兄弟元素的位置，自身不动
		右margin会影响右边兄弟元素的位置，自身不动

	 -->
</body>
```

##### 事项3

块级元素、行内块元素，均可以完美地设置四个方向的margin，但行内元素、左右margin可以完美设置，上下margin设置无效。

>举例

```html
	<style>
		#d1 {
			width: 400px;
			height: 400px;
			margin: 50px;
			background-color: deepskyblue;
		}

		#d2 {
			width: 400px;
			height: 400px;
			background-color: blue;
			display: inline-block;
			margin: 50px;
		}

		/* 行内元素 */
		.one {
			background-color: skyblue;
		}
		.two {
			background-color: orange;
			margin-left: 50px;
			margin-right: 50px;

			/* 行内元素设置上下margin无效 */
			margin-top: 100px;
			margin-bottom: 100px;
		}
		.three {
			background-color: green;
		}
	</style>
</head>
<body>
	<div id="d1">我是一个块元素</div>
	<div>我是一段文字</div>
	<hr>
	<div id="d2"></div>
	<div>我是一段文字</div>
	<hr>
	<span class="one">人之初</span><span class="two">性本善</span><span class="three">性相近</span>
	<!-- 
		总结：
		对于块元素或行内块元素，margin一样
		对于行内元素，左右的margin是可以完美设置的，上下的margin设置是无效的
	 -->
</body>
```

##### 事项4

margin的值也可以设置为auto，表示距离该方向最远（目前只有左右有效），如果给一个块级元素设置左右margin都为auto，该块级元素会在父元素中水平居中。

```html
<style>
		div {
			width: 800px;
			height: 100px;
			/* 
				auto 代表距离那一边能有多远就有多远
			*/
			margin-left: auto;

			background-color: deepskyblue;
		}
	</style>
</head>
<body>
	<div>
		你好啊
	</div>
	<!-- 
		总结：
		对于块级元素，左右margin都设成auto就可以实现该元素在其父元素内水平居中

		上下auto无效，
		auto的效果实际上是离该边能有多远就多远，
		margin-left：auto;  离左边最远，自然就紧贴右边

	 -->
</body>
```

##### 事项5

margin的值可以为负值

```html
<style>
		.box {
			width: 200px;
			height: 200px;
		}
		.box1 {
			background-color: skyblue;
		}
		.box2 {
			background-color: orange;
			/* 
				margin可以是负的值，
				top动自己，往上走50px，会压住上面的
			*/
			margin-top: -50px;
		}
	</style>
</head>
<body>
	<div class="box box1">1</div>
	<div class="box box2">2</div>
</body>
```

#### margin塌陷问题

##### 什么是margin塌陷

第一个子元素的上margin会作用到父元素上，最后一个子元素的下margin会作用到父元素上。
>举例

```html
<style>
		.outer {
			width: 400px;
			height: 400px;
			background-color: gray;
		}
		.inner1 {
			width: 100px;
			height: 100px;
			background-color: orange;
			/* 给inner1加一个下外边距 正常 */
			/* margin-bottom: 50px; */

			/*
			 给inner1加一个上外边距
				异常，我们期待的是inner1相对于父元素下移
				但是实际上却是inner1和inner2相对于父元素没动
				父元素相对于自己的父亲元素下移了

				即margin-top没在inner1上生效，在其父元素上生效了
			 */
			 margin-top: 50px;
		}
		.inner2 {
			width: 100px;
			height: 100px;
			background-color: red;

			/* 给inner2加一个上外边距 正常 */
			/* margin-top: 50px; */

			/* 
				我们尝试给inner2加margin-bottom值，但是他没生效
				这个属性又被其父元素抢走了
			*/
			margin-bottom: 50px;
		}

		/* 
			margin塌陷是一个历史遗留问题，w3c在最初设计的时候
			第一个元素的margin-top对自己无效，会加到父元素上
			最后一个元素的margin-bottom对自己无效，会加到父元素上
		
		*/
	</style>
</head>
<body>
	<div class="outer">
		<div class="inner1">inner1</div>
		<div class="inner2">inner2</div>
	</div>
</body>
```

##### margin塌陷问题的解决

>方案1

```sh
给父元素设置不为0的padding
```

```html
<style>
		.outer {
			width: 400px;
			height: 400px;
			background-color: gray;

			/* 
			解决方案2 
				给父元素加任意padding 
				padding 不可为0,为0无效
			*/
			padding: 1px;
		
		}
		.inner1 {
			width: 100px;
			height: 100px;
			background-color: orange;

			 margin-top: 50px;
		}
		.inner2 {
			width: 100px;
			height: 100px;
			background-color: red;


			margin-bottom: 50px;
		}
	</style>
</head>
<body>
	<div class="outer">
		<div class="inner1">inner1</div>
		<div class="inner2">inner2</div>
	</div>
</body>
```

>方案2

```sh
给父元素设置宽度不为0的border
```

```html
<style>
		.outer {
			width: 400px;
			height: 400px;
			background-color: gray;

			/* 
			解决方案1 给父元素加边框
			边框宽度不可为0,为0无效 
			*/
			border:2px solid #000;
		}
		.inner1 {
			width: 100px;
			height: 100px;
			background-color: orange;

			 margin-top: 50px;
		}
		.inner2 {
			width: 100px;
			height: 100px;
			background-color: red;


			margin-bottom: 50px;
		}
	</style>
</head>
<body>
	<div class="outer">
		<div class="inner1">inner1</div>
		<div class="inner2">inner2</div>
	</div>
</body>
```

>方案3

```sh
前两种方式的缺点，会改变盒子大小
给父元素设置css样式overflow:hidden
```

```html
	<style>
		.outer {
			width: 400px;
			height: 400px;
			background-color: gray;

			/* 
			前两种方式的弊端：会影响盒子的大小

			优化
				给父元素身上加overflow:hidden;
			*/
			overflow: hidden;
			/* overflow 溢出之后的显示模式 */
		}
		.inner1 {
			width: 100px;
			height: 100px;
			background-color: orange;

			 margin-top: 50px;
		}
		.inner2 {
			width: 100px;
			height: 100px;
			background-color: red;


			margin-bottom: 50px;
		}
	</style>
</head>
<body>
	<div class="outer">
		<div class="inner1">inner1</div>
		<div class="inner2">inner2</div>
	</div>
</body>
```

#### margin合并问题

##### 什么是margin合并？

上面兄弟元素的下外边距和下面兄弟元素的上外边距会合并，取一个最大的值，而不是相加。

##### 如何规避margin合并？

无需解决，布局的时候上下的兄弟元素，只给一个设置上下边距就可以了

### 处理内容的溢出

```sh
Css属性名：overflow

功能：溢出内容的处理方式

属性值：
visible 显示、默认值
hidden  隐藏
scroll  显示滚动条，不论内容是否溢出
auto    自动显示滚动条，内容不溢出不显示
```

```sh
Css属性名：overflow-x

功能：水平方向溢出内容的处理方式

属性值：
visible 显示、默认值
hidden  隐藏
scroll  显示滚动条，不论内容是否溢出
auto    自动显示滚动条，内容不溢出不显示
```

```sh
Css属性名：overflow-y

功能：垂直方向溢出内容的处理方式

属性值：
visible 显示、默认值
hidden  隐藏
scroll  显示滚动条，不论内容是否溢出
auto    自动显示滚动条，内容不溢出不显示
```

>注意

```sh
1.overflow-x、overflow-y不能是实验性属性，二者要相同时才生效。
2.overflow常用的值是hidden和auto，除了能处理溢出的显示方式，还可以解决很多疑难杂症。
```

### 隐藏元素的两种方式

#### 方式1：visibility属性

```sh
visibility属性默认值是show，如果设置为hidden，元素会隐藏。
元素看不见了，但是还占有原来的位置，元素的大小依然保持。
```

#### 方式2：display属性

```sh
设置display:none,就可以让元素隐藏。
彻底的隐藏，不但看不见，也不占用任何位置，没有大小宽高。
```

#### 举例

```html
<style>
		.box {
			width: 200px;
			height: 200px;
		}
		.box1 {
			background-color: aqua;
			/* 隐藏元素 通过控制元素的显示模式 */
			/* display: none; */

			/* 
			visibility元素显隐性 
			默认show显示 
			可以选值hidden隐藏 
			*/
			visibility: hidden;
		}
		.box2 {
			background-color: orange;
		}
		/* 
			区别：
			display:none 隐藏后，不占位置，但是仍然可以选中

			visibility: hidden; 隐藏后仍然要占位，也可以选中
		*/
	</style>
</head>
<body>
	<div class="box box1">1</div>
	<div class="box box2">2</div>
</body>
```

### 样式的继承

有些样式会继承，元素如果本身设置了某个样式，就使用本身设置的样式，但如果本身没有设置某个样式，会从父元素开始一级一级继承(优先继承离得近的祖先元素)

#### 会继承的css属性

```sh
字体属性、文本属性(除了vertical-align)、文字颜色等
```

#### 不会继承的css属性

```sh
边框、背景、内边距、外边距、宽高、溢出方式等
```

>规律

```sh
能继承的属性，都是不影响布局的，简单说：都是和盒子模型没关系的。
```

#### 观察能否继承

>方式1

```sh
通过开发者工具，在样式的最下方
Inherited from xxx
继承自xxx，暗的表示不可继承，亮的表示继承源
```

>方式2

```sh
通过mdn查看
```

### 样式检查器

>行内/内联样式

```sh
element.style{

}
# 这里记录的是选中元素的内联样式
```

>内部样式
>
>右侧有文件名

```sh
.box {                                          文件名
	height:100px;
}
```

>外部样式
>
>右侧有 xx.css?xxxxx

```sh
.box {                                          指向文字
	height:100px;
}
```

>默认样式
>
>右侧有`user agent stylesheet`

```sh
div {
	display:block;
}
```

>继承样式
>
>Inherit from xxx

### 元素的默认样式

很多元素都有默认样式，默认样式会覆盖继承的样式，

```sh
继承的样式优先级是最低的，可以被任意覆盖
```

相要修改默认样式，只要选中元素，重写样式即可

>注意

```sh
#body的默认样式
body{
	display:block;
	margin:8px;
}
```

优先级：`元素的默认样式>继承的样式`，所以如果要重置元素的默认样式，选择器一定要直接选择到该元素。

### CSS_布局小技巧

#### 技巧1

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>布局技巧1</title>
	<style>
		.outer {
			width: 400px;
			height: 400px;
			background-color: gray;

			/* 要想要子元素的margin生效，需要添加 */
			overflow: hidden;
		}
		.inner {
			width: 200px;
			height: 100px;
			background-color: orange;

			/* 水平居中 */
			margin: 0 auto;

			/* 垂直居中 （父元素总高度-该元素总高度）/2 */
			margin-top: 150px;

			/* 内部文本水平居中 */
			text-align: center;
			/* 
				内部单行文本垂直居中
				行高等于高度
			 */
			line-height: 100px;
		}

	</style>
</head>
<body>
	<div class="outer">
		<div class="inner">
			inner
		</div>
	</div>
</body>
</html>
```

#### 技巧2

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>布局技巧2</title>
	<style>
		/* 
			之前我们已经知道 text-align可以操作 文本

			可以用text-align属性操作行内元素和行内块元素
			1.让一个块里面的行内元素水平居中
				在块元素上使用 text-align:center


			行内元素可以当作文本处理，所以垂直居中也可以用line-height

		*/
		.outer {
			width: 400px;
			height:400px;
			background-color: gray;
			/* 水平居中 */
			text-align: center;

			/* 垂直居中 */
			line-height: 400px;
		}
		span {
			background-color: orange;
			font-size: 20px;
		}
	</style>
</head>
<body>
	<div class="outer">
		<span>出来学习</span>
	</div>
</body>
</html>
```

#### 技巧3

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>布局小技巧3</title>
	<style>
		.outer{
			width: 400px;
			height: 400px;
			background-color: gray;
			/* 水平居中垂直居中 */
			text-align: center;
			line-height: 400px;
			/* 
			父元素的字体大小会影响 内部行内块元素(例如图片的垂直居中) 
			主要原因是基线
			所以将字体调为0
			*/
			font-size: 0px;
		}
		.inner{
			display: inline-block;
			/*文字与图片 垂直居中 */
			vertical-align: middle;
			width: 100px;
			height: 100px;
			background-color: aqua;
		}
		span{
			/* 给文字大小 */
			/* 文字与图片 垂直居中 */
			font-size: 20px;
			vertical-align: middle;
		}
	</style>
</head>
<body>
	<div class="outer">
		<span>x</span>
		<div class="inner"></div>
	</div>
</body>
</html>
```

#### 总结

>行内元素、行内块元素，可以被父元素当做文本处理

```sh
即：可以像处理文本对齐一样，去处理：行内、行内块在父元素中的对齐。
例如：text-align、line-height、text-indent等
```

>如何让子元素，在父元素中水平居中

```sh
1.若子元素为块元素，给父元素加上："margin:0 auto;"
```

```sh
2.若子元素为行内元素、行内块元素，给父元素加上："text-align:center;"
```

>如何让子元素，在父亲中垂直居中

```sh
1.若子元素为块元素，给子元素加上："margin-top"，值为(父元素content-子元素盒子总高)/2
```

```sh
2.若子元素为行内元素、行内块元素：
让父元素的"line-height = height"，每个子元素都加上："vertical-align:middle"
补充：若想绝对垂直居中，父元素"font-size"设置为0
```

### 元素之间的空白问题

#### 产生的原因：

```sh
行内元素、行内块元素，彼此之间的换行会被浏览器解析为一个空白字符。
```

#### 解决方案

##### 方案一

```sh
去掉换行和空格
```

##### 方案二

```sh
给父元素设置"font-size:0",再给需要显示文字的元素，单独设置字体大小。
```

##### 案例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>25_元素之间的空白问题</title>
	<style>
		div{
			height: 50px;
			background-color: gray;
			font-size: 0px;
		}
		.s1 {
			background-color: skyblue;
			font-size: 20px;
		}
		.s2 {
			background-color: orange;
			font-size: 20px;
		}
		.s3 {
			background-color: green;
			font-size: 20px;
		}
	</style>
</head>
<body>
	<div>
		<!-- 由于行内元素或行内块元素换行写，就会产生一个问题，元素之间存在间隙 -->
		<span class="s1">人之初</span>
		<span class="s2">性本善</span>
		<span class="s3">性相近</span>
		<!-- 
			方案1：不换行写，都写在一行

			方案2：空格也是文字，直接给父元素的字体大小设为0,子元素的字体大小自己设置
		 -->
	</div>
</body>
</html>
```

### 行内块的幽灵空白问题

#### 产生原因

行内块元素与文本的基线对齐，而文本的基线与文本最底端之间是有一定距离的。

#### 解决方案

```sh
1.给行内元素设置"vertical"，值不为"baseline"即可，设置为"middel、bottom、top"均可
```

```sh
2.若父元素中只有一张图片，设置图片为"display:block;"
```

```sh
3.给父元素设置"font-size:0"。如果该行内块内部还有文本，则需要将文本用别的标签包裹，并单独设置"font-size".
```

#### 案例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>24_行内块元素的幽灵空白问题</title>
	<style>
		/* 
			幽灵空白：行内块元素不贴着父级的底部，而是与父亲底部有点间距
			原因：在行内块元素后面写个x可以知道，行内块元素的底部与x的底部基线对齐了

			处理方式：给行内块元素加 vertical-align，top/bottom/middle都可以，baseline不行

			当行内块元素比文字大时，行内块就会填满父级，文字相对其运动
		*/
		.box {
			width: 60px;
			background-color: skyblue;
		}
		.kuai {
			display: inline-block;
			vertical-align: bottom;
		}

		/* 
			解决方案2：把行内块元素改为块元素
			缺点：后面不能再有别的元素了
		*/

		/* 
			方案3：这是由于字体的基线导致的，把父级字体大小设为0即可

			小贴士：凡是由文字导致的
		*/
	</style>
</head>
<body>
	<div class="box">
		<div class="kuai"></div>
	</div>
</body>
</html>
```

## Css浮动

### 1.浮动的简介

在最初,浮动是用来实现文字环绕图片效果的,现在浮动是主流的页面布局方式之一.

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>浮动的简介</title>
	<style>
		.box {
			width: 600px;
			height: 400px;
			background-color: skyblue;
		}
		.inner{
			display: inline-block;
			width: 200px;
			height: 200px;
			background-color: blueviolet;

			/* 添加浮动 */
			float: left;
			margin-right: 0.5rem;
		}

		/* 让第一个字母变大,并浮动 */
		.test::first-letter {
			font-size: 80px;
			float: left;
		}
	</style>
</head>
<body>
	<!-- 
		浮动的设计初衷:浮动设计之初并不是像现在一样用来布局的,他的目的是让文字环绕图片
	 -->
	 <!-- 
		在不加浮动之前,文字第一行的基线与行内块的对齐,后续文字换行,不要包p标签
	  -->
	 <div class="box">
			<div class="inner"></div>
			Lorem ipsum dolor sit amet consectetur adipisicing elit. Qui, fugit tempora autem dolore inventore esse adipisci quo laudantium ad libero, ullam nihil, magni perspiciatis hic incidunt voluptates id asperiores nobis fugiat vel minima modi officia. Reiciendis alias, quam omnis obcaecati rem consequuntur! Iusto atque, rem facere tenetur a non enim impedit minima veniam labore provident eaque voluptates laborum deleniti ipsa. Ex quam, nesciunt at odio voluptate porro ipsum excepturi eaque. Excepturi amet nam atque voluptates quaerat quas. Sit, optio dolor ad autem consequuntur doloremque veritatis temporibus alias eos, quidem asperiores suscipit dolores exercitationem repellat neque excepturi maiores minus harum nam?
	 </div>
	 <hr>
	 <!-- 文字环绕文字 -->
	 <div class="test">
		Lorem ipsum dolor sit amet consectetur adipisicing elit. Quae praesentium dignissimos saepe sit placeat labore quam necessitatibus exercitationem temporibus eius, repellat enim adipisci ipsam veritatis corrupti sint autem minus explicabo cumque facere, voluptates iste nobis? Assumenda neque accusantium eos nostrum beatae doloremque veritatis ab voluptatem totam similique facilis non soluta molestias perspiciatis deserunt eius modi in, fugit necessitatibus molestiae quam.
	 </div>
</body>
</html>
```

### 2.元素浮动后的特点

1.脱离文档流

2.不管浮动前是什么元素,浮动后:默认宽与高都是被内容撑开(尽可能小),而且可以设置宽高

3.不会独占一行,可以与其他元素共用一行.

4.不会margin合并,也不会margin塌陷,能够完美的设置四个方向的margin和padding

5.不会像行内块一样被当作文本处理(没有行内块的空白问题)

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>02_元素浮动后的特点</title>
	<style>
		/* 
			元素浮动之后的特点:
			文档流,元素默认的排列方式,紧贴底部白色画布
			1.会脱离文档流,飘起来了,离开了有序画布
			2.不管浮动之前是块/行内块/行,浮动之后宽高默认都是被内容所撑开,但是可以设置的.
			3.可以和其他元素"共用"一个区块,从3D视角,一层一层的,所谓共用指的是在x\y轴上的投影重叠,z轴上独立
			4.浮动后,margin和padding都是完美设置,没有塌陷
			5.浮动前行内块和行内可以被text-*处理,浮动后不行,特性丢失了
		
		*/
		.outer{
			width: 800px;
			height: 400px;
			background-color: gray;
			padding: 10px;
		}
		.box {
			font-size: 20px;
		}
		.box1 {
			background-color: skyblue;
		}
		.box2 {
			float: left;
			/* 
				box2浮动起来了,不占位置,相当于从画布上拿起来了
				box3自动向上顶替原box2的位置,所以box2下面是box3

				box3的文字没有被box2盖住的原因,由于浮动设计的初衷,文字会避开上层的浮动,自动往外边移动
			*/
			background-color: red;
		}
		.box3 {
			background-color: green;
		}
	</style>
</head>
<body>
	<div class="outer">
		<div class="box box1">盒子1</div>
		<div class="box box2">盒子2</div>
		<div class="box box3">盒子3</div>
	</div>
</body>
</html>
```

### 3.浮动小练习

>1

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>03_浮动小练习1</title>
	<style>
		.outer{
			width: 500px;
			background-color: gray;
			/* 父亲加边框的原因:防止抢走子元素的margin-top或margin-bottom */
			border: 1px solid black;
		}
		.box {
			width: 100px;
			height: 100px;
			background-color: skyblue;
			border: 1px solid black;
			margin: 10px;
		}
		.box1 {
			float: right;
		}
		/* 
			表面上看是 box1到了右边

			实际上是box1先飘起来,box2与box3上移补位,box1脱离了平面后飞到右边
			在z轴上看已经不在同一个平面
		*/
	</style>
</head>
<body>
	<div class="outer">
		<div class="box box1">1</div>
		<div class="box box2">2</div>
		<div class="box box3">3</div>
	</div>
</body>
</html>
```

>2

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>04_浮动小练习02</title>
	<style>
			.outer{
			width: 500px;
			background-color: gray;
			/* 父亲加边框的原因:防止抢走子元素的margin-top或margin-bottom */
			border: 1px solid black;
		}
		.box {
			width: 100px;
			height: 100px;
			background-color: skyblue;
			border: 1px solid black;
			margin: 10px;
		}
		.box1 {
			float: left;
		}
		/* 
			看表象 box2的内容与box3重叠了,
			实际上,是box1飘起来后,box2往上补位,但是由于浮动的初衷,box2的文字内容被浮动起来的box1推开,
			而box3补位时占据了box2的位置,box2被box1推开的文字内容叠到了box3上
			
			故本质上,box2在box1下面,只是文字被挤到了box3上
		*/
	</style>
</head>
<body>
	<div class="outer">
		<div class="box box1">1</div>
		<div class="box box2">2</div>
		<div class="box box3">3</div>
	</div>
</body>
</html>
```

>3

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>04_浮动小练习03</title>
	<style>
			.outer{
			width: 500px;
			background-color: gray;
			/* 父亲加边框的原因:防止抢走子元素的margin-top或margin-bottom */
			border: 1px solid black;
		}
		.box {
			width: 100px;
			height: 100px;
			background-color: skyblue;
			border: 1px solid black;
			margin: 10px;
		}
		.box1 {
			float: left;
		}
		.box2 {
			float: left;
		}
		.box3 {
			float: left;
		}
		/* 
			三个盒子排成一条线

			可以理解为三个盒子都飞起来到了第二个平面,按照文档流的顺序起飞
			
			由于在同一个平面,所以不能重叠,只能排队了
		*/
	</style>
</head>
<body>
	<div class="outer">
		<div class="box box1">1</div>
		<div class="box box2">2</div>
		<div class="box box3">3</div>
	</div>
</body>
</html>
```

>4

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>06_浮动小练习04</title>
	<style>
			.outer{
			width: 500px;
			background-color: gray;
			/* 父亲加边框的原因:防止抢走子元素的margin-top或margin-bottom */
			border: 1px solid black;
		}
		.box {
			width: 200px;
			height: 200px;
			background-color: skyblue;
			border: 1px solid black;
			margin: 10px;
		}
		.box1 {
			float: left;
		}
		.box2 {
			float: left;
		}
		.box3 {
			float: left;
		}
		/* 
			box1 box2排成一行,box3排到了第二行

			原因,可以想像成一个3d柱状,底部的平面是固定的,他们飞到了第二个平面
			x\y构筑的面积不变,只是z轴发生了变化,所以当一行放不下时,自然会换行
			相当于在新平面上换行
		*/
	</style>
</head>
<body>
	<div class="outer">
		<div class="box box1">1</div>
		<div class="box box2">2</div>
		<div class="box box3">3</div>
	</div>
</body>
</html>
```

>5

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>07_浮动小练习05</title>
	<style>
			.outer{
			width: 500px;
			background-color: gray;
			/* 父亲加边框的原因:防止抢走子元素的margin-top或margin-bottom */
			border: 1px solid black;
		}
		.box {
			width: 200px;
			height: 200px;
			background-color: skyblue;
			border: 1px solid black;
			margin: 10px;
		}
		.box1 {
			float: left;
			height: 400px;
		}
		.box2 {
			float: left;
		}
		.box3 {
			float: left;
		}
		/* 
			box1 box2排成一行,box3排到了第二行右边

			原因,可以想像成一个3d柱状,底部的平面是固定的,他们飞到了第二个平面
			但x或y不变,只是z轴发生了变化,所以某一个方向放不下时,自然会换行
			相当于在新平面上换行

			1.y存在
			box3在换行的时候,如果y有高度box3的高度加上box1的高度超过了,放不下,就被挤到右边,如果还放不下,box3就会"消失"
			"消失":被挤出显示区了,柱状就是显示区,外边不可见
			2.y不存在
			box3在换行的时候，如果y没有高度，就会按最小体积进行扩充，即在让y变动最小，其他同理

		*/
	</style>
</head>
<body>
	<div class="outer">
		<div class="box box1">1</div>
		<div class="box box2">2</div>
		<div class="box box3">3</div>
	</div>
</body>
</html>
```

### 4.浮动后的影响

>对父元素的影响

```sh
不能撑起父元素的高度，导致父元素高度塌陷；但父元素的宽度依然束缚浮动的元素。
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>08_浮动后的影响1</title>
	<style>
		/* 
			浮动后的影响:
			1.如果父级没有设置高度,他的高度就是由子元素撑开的,当子元素脱离文档流后
			父元素的高度就消失了

			术语：
			造成父元素塌陷
			
	
		*/
		.outer{
			width: 500px;
			background-color: gray;
			border:1px solid black;
		}
		.box {
			width: 200px;
			height: 200px;
			background-color: skyblue;
			border: 1px solid black;
			margin: 10px;
		}
		.box1,.box2,.box3{
			float: left;
		}
	</style>
</head>
<body>
	<div class="outer">
		<div class="box box1">1</div>
		<div class="box box2">2</div>
		<div class="box box3">3</div>
	</div>
	<div style="background-color: orange;">Lorem ipsum dolor, sit amet consectetur adipisicing elit. Est cupiditate quae laudantium voluptate ea, amet accusamus tempore perspiciatis dolor necessitatibus eveniet obcaecati assumenda! Beatae, voluptates neque nam delectus iure vel. Cupiditate, reprehenderit. Itaque hic quod rem voluptates, neque beatae asperiores ab voluptatem, laborum temporibus consequuntur ratione officiis, tenetur repellat adipisci.</div>
</body>
</html>
```

>对兄弟元素的影响

```sh
后面的兄弟元素，会占据浮动元素之前的位置，在浮动元素的下面；对前面的兄弟无影响。
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>09_浮动后的影响2</title>
	<style>
		/* 
			浮动后的影响:
			2.后面的兄弟元素，会占据浮动元素之前的位置，在浮动元素的下面，文字被甩出去
			对前面的兄弟无影响
			
	
		*/
		.outer{
			width: 500px;
			background-color: gray;
			border:1px solid black;
		}
		.box {
			width: 100px;
			height: 100px;
			background-color: skyblue;
			border: 1px solid black;
			margin: 10px;
		}
		.box1,.box2,.box3{
			float: left;
		}
		
	</style>
</head>
<body>
	<div class="outer">
		<div class="box box0">0</div>
		<div class="box box1">1</div>
		<div class="box box2">2</div>
		<div class="box box3">3</div>
		<div class="box box4">4</div>
	</div>

</body>
</html>
```

### 5.解决浮动产生的影响(清除浮动)

>问题

```sh
浮动后：
1.父元素塌陷，高度消失
2.后面兄弟被覆盖
```

#### 方案1

```sh
给父元素指定高度。--解决父元素塌陷
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>10_解决浮动产生的影响1</title>
	<style>
		/* 
			要达到的目的：
			父元素的高度别塌

			方案1：
			给父元素一个高度，算出来的
		*/
		.outer{
			width: 500px;
			background-color: gray;
			border:1px solid black;
			height: 200px;
		}
		.box {
			width: 100px;
			height: 100px;
			background-color: skyblue;
			border: 1px solid black;
			margin: 10px;
		}
		.box1,.box2,.box3{
			float: left;
		}
		
	</style>
</head>
<body>
	<div class="outer">
		<div class="box box1">1</div>
		<div class="box box2">2</div>
		<div class="box box3">3</div>
	</div>
	<div style="background-color: orange;">Lorem ipsum dolor, sit amet consectetur adipisicing elit. Est cupiditate quae laudantium voluptate ea, amet accusamus tempore perspiciatis dolor necessitatibus eveniet obcaecati assumenda! Beatae, voluptates neque nam delectus iure vel. Cupiditate, reprehenderit. Itaque hic quod rem voluptates, neque beatae asperiores ab voluptatem, laborum temporibus consequuntur ratione officiis, tenetur repellat adipisci.</div>
</body>
</html>
```

#### 方案2

```sh
给父元素设置浮动，带来其他影响（极度不推荐）。---解决父元素塌陷
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>11_解决浮动产生的影响2</title>
	<style>
		/* 
			要达到的目的：
			父元素的高度别塌

			方案2：
			让父亲也浮动飘起来，父亲高度不塌陷，因为相当于父亲也到了第二个平面
		*/
		.outer{
			width: 500px;
			background-color: gray;
			border:1px solid black;

			float: left;
		}
		.box {
			width: 100px;
			height: 100px;
			background-color: skyblue;
			border: 1px solid black;
			margin: 10px;
		}
		.box1,.box2,.box3{
			float: left;
		}
		
	</style>
</head>
<body>
	<div class="outer">
		<div class="box box1">1</div>
		<div class="box box2">2</div>
		<div class="box box3">3</div>
	</div>
	<div style="background-color: orange;">Lorem ipsum dolor, sit amet consectetur adipisicing elit. Est cupiditate quae laudantium voluptate ea, amet accusamus tempore perspiciatis dolor necessitatibus eveniet obcaecati assumenda! Beatae, voluptates neque nam delectus iure vel. Cupiditate, reprehenderit. Itaque hic quod rem voluptates, neque beatae asperiores ab voluptatem, laborum temporibus consequuntur ratione officiis, tenetur repellat adipisci.</div>
</body>
</html>
```

#### 方案3

```sh
给父元素设置`overflow:hidden`--解决父级塌陷
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>12_解决浮动产生的影响3</title>
	<style>
		/* 
			要达到的目的：
			父元素的高度别塌

			方案3：
			添加overflow:hidden 也能解决父元素高度塌陷

			通过 overflow:scroll可以知道，兄弟元素还存在只是被hidden截断了
		*/
		.outer{
			width: 500px;
			background-color: gray;
			border:1px solid black;

			overflow:hidden;
		}
		.box {
			width: 100px;
			height: 100px;
			background-color: skyblue;
			border: 1px solid black;
			margin: 10px;
		}
		.box1,.box2,.box3{
			float: left;
		}
		
	</style>
</head>
<body>
	<div class="outer">
		<div class="box box1">1</div>
		<div class="box box2">2</div>
		<div class="box box3">3</div>
	</div>
	<div style="background-color: orange;">Lorem ipsum dolor, sit amet consectetur adipisicing elit. Est cupiditate quae laudantium voluptate ea, amet accusamus tempore perspiciatis dolor necessitatibus eveniet obcaecati assumenda! Beatae, voluptates neque nam delectus iure vel. Cupiditate, reprehenderit. Itaque hic quod rem voluptates, neque beatae asperiores ab voluptatem, laborum temporibus consequuntur ratione officiis, tenetur repellat adipisci.</div>
</body>
</html>
```

#### 方案4

```sh
把后面会被覆盖的兄弟变成行内元素 -- 解决兄弟被覆盖
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>13_解决浮动产生的影响4</title>
	<style>
		/* 
			要达到的目的：
			兄弟不被盖住

			方案1：
			把兄弟设置为display:inline-block,
			会被当成文本元素，甩在外面，就是最初的环绕初衷
		*/
		.outer{
			width: 500px;
			background-color: gray;
			border:1px solid black;

		}
		.box {
			width: 100px;
			height: 100px;
			background-color: skyblue;
			border: 1px solid black;
			margin: 10px;
		}
		.box1,.box2,.box3{
			float: left;
		}
		.box4{
			display: inline-block;
		}
	</style>
</head>
<body>
	<div class="outer">
		<div class="box box1">1</div>
		<div class="box box2">2</div>
		<div class="box box3">3</div>
		<div class="box box4">4</div>
	</div>
	
</body>
</html>
```

#### 方案5

```sh
在所有浮动元素的最后面，添加一个块级元素，并给该块级元素设置`clear:both`
理论上只要给一个非行内元素添加了clear属性，他就可以免除其他元素浮动对他的影响
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>14_解决浮动产生的影响5</title>
	<style>
		/* 
			要达到的目的：
			1.父元素不塌陷
			2.兄弟不被盖住

			方案1：
			把兄弟设置为display:inline-block,
			会被当成文本元素，甩在外面，就是最初的环绕初衷
		*/
		.outer{
			width: 500px;
			background-color: gray;
			border:1px solid black;
			overflow: hidden;
		}
		.box {
			width: 100px;
			height: 100px;
			background-color: skyblue;
			border: 1px solid black;
			margin: 10px;
		}
		.box1,.box2,.box3,.box4{
			float: left;
		}
		.mofa{
			/* 
				消除前面所有左浮动兄弟产生的影响
				clear:left;
				消除前面所有右浮动兄弟产生的影响
				clear:right;
				消除前面所有浮动兄弟产生的影响
				clear:both;
			*/
			clear: both;
		}

		/*
			clear存在的问题，
			1.如果box4不加浮动一切正常，如果box4加了浮动，一切白搭
			不仅如此，clear的影响会让他独占一行，不和其他元素在一行浮动
		
			2.clear不能加给行内元素，因为行内元素没有宽高

			解决方案：
			给一个不占位的块元素设置clear，让他不触犯上述错误
		*/
	</style>
</head>
<body>
	<div class="outer">
		<div class="box box1">1</div>
		<div class="box box2">2</div>
		<div class="box box3">3</div>
		<div class="box box4">4</div>
		<!-- 设立一个不占位的元素，让他去使用clear -->
		<div class="mofa"></div>
	</div>
	
</body>
</html>
```

#### 方案6

```sh
给浮动元素的父元素，设置伪元素，通过伪元素清除浮动，原理同方案5 -- 推荐
```

```css
.parent::after{
    content:'';
    dispaly:block;
    clear:both;
}
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>15_完美解决浮动产生的影响6</title>
	<style>
		/* 
			要达到的目的：
			1.父元素不塌陷
			2.兄弟不被盖住

			完美解决方案本质上就是设立一个空的块元素，使之触发clear:both
			不过写法更优雅
	
		*/
		.outer{
			width: 500px;
			background-color: gray;
			border:1px solid black;
			overflow: hidden;
		}
		.box {
			width: 100px;
			height: 100px;
			background-color: skyblue;
			border: 1px solid black;
			margin: 10px;
		}
		.box1,.box2,.box3,.box4{
			float: left;
		}
		/* 
			完美解决方案本质上就是设立一个空的块元素，使之触发clear:both
			不过写法更优雅

			不过还是存在一个问题，那就是如果存在一个元素不浮动，那么还是会产生覆盖
			所以提出布局原则：
			在一个父元素里面，要么所有元素都浮动，要么所有元素都不浮动
		*/
		.outer::after{
			content: "";
			display: block;
			clear: both;
		}
	</style>
</head>
<body>
	<div class="outer">
		<div class="box box1">1</div>
		<div class="box box2">2</div>
		<div class="box box3">3</div>
		<div class="box box4">4</div>
		<!-- 设立一个不占位的元素，让他去使用clear -->
		<!-- <div class="mofa"></div> -->
	</div>
	
</body>
</html>
```

#### 总结

上述方案只能解决，父元素的子元素都浮动或者末尾部分都浮动的情况，其他情况无法清除，所以引出布局原则：

```sh
设置浮动的时候，兄弟元素要么都浮动，要么全都不浮动
```

## Css定位

### 1.相对定位

#### 1.1如何设置相对定位

* 给元素设置`position:relative`即可实现相对定位，相对他自身在文档流中的原始位置，即使视觉上移动了，它在文档流中的占位仍然没变
* 可以使用`left`、`right`、`top`、`bottom`四个属性调整位置。

#### 1.2相对定位的参考点在哪里

相对自己原来的位置

#### 1.3相对定位的特点

1.不会脱离文档流，元素位置的变化，只是视觉效果上的变化，不会对其他元素产生任何影响。

2.定位元素的显示层级比普通元素高，无论什么定位，显示层级都是一样的。

默认规则是：

* 定位的元素会在普通元素之上。
* 都发生定位的两个元素，后写的元素会盖在先写的元素之上。

3.`left`不能和`right`一起设置,同时设置只有`left`生效，`top`和`bottom`不能一起设置，同时设置只有`top`生效。

4.相对定位的元素，也能继续浮动，但不推荐这样做。

5.相对定位的元素，也能通过`margin`调整位置，但不推荐这样做。

>注意

绝大多数情况下，相对定位，会与绝对定位配合使用。

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>01_相对定位</title>
	<style>
		.outer {
			width: 500px;
			background-color: skyblue;
			border:1px solid black;
		}
		.box {
			width: 200px;
			height: 200px;
		}
		.box1{
			background-color: #888;
		}
		.box2{
			background-color:green;
			/* 开启相对定位 */
			position: relative;
			/* 距离左边100px */
			/* 这里的相对指的是相对其自身的原始位置 */
			left: 100px;
			top: 50px;
			/* 
				从box3和box1没有变化可以看出，
				box2没有脱离文档流，他在文档流的原始位置一直占位，只是在视觉上变化
			*/
			/* 
				注意事项：
				right与left不能同时写，同时写只有left生效
				top与bottom不能同时写，同时写只有top生效
			*/
		}
		.box3{
			background-color: red;
		}
		/* 
			一个元素只有开了定位，层级就比普通元素要高
			如果两个普通元素都开了定位，没设层级，那么后写的层级默认比前面高

			定位最后谁显示只和层级有关，与浮动的漂浮不一样

			漂浮 不同平面，脱离文档流，上天了
			定位 层级，还在地上，只是谁压在上面
		*/
		/* 
			定位与margin和浮动可以一起用
			但是不推荐定位与margin或浮动一起用
		*/

		/* 
			相对定位的优势：
			1.不脱离文档流，对其他兄弟都没影响
			2.可以超出父容器的范围
		*/
	</style>
</head>
<body>
	<div class="outer">
		<div class="box box1">1</div>
		<div class="box box2">2</div>
		<div class="box box3">3</div>
	</div>
</body>
</html>
```

### 2.绝对定位

#### 2.1如何设置绝对定位

```sh
1.给元素设置'position:absolute'即可实现绝对定位
2.可以使用left、right、top、bottom四个属性调整位置
```

#### 2.2 绝对定位的参考点在哪里？

>参考它的包含块

```sh
什么是包含块？
1.对于没有脱离文档流的元素，包含块就是父元素
2.对于脱离文档流的元素：包含块是第一个拥有定位属性的祖先元素，如果所有的祖先都没有定位，那包含块就是整个页面。
```

#### 2.3绝对定位元素的特点

```sh
1.脱离文档流，会对后面的兄弟元素、父元素有影响。
2.left不能和right一起设置，top不能和bottom一起设置，一起设置的化只有left和top会生效。
3.绝对定位、浮动不能同时设置，如果同时设置，浮动失效，以定位为主。
4.绝对定位的元素，也能通过margin调整位置，但不推荐这样做。
5.无论是什么元素(行内、行内块、块级)设置绝对定位之后，都变成了定位元素。
```

#### 2.4定位元素

```sh
1.默认宽、高都被内容撑开
2.可以设置宽高
```

#### 2.5举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>02_绝对定位</title>
	<style>
		.outer {
			width: 500px;
			background-color: skyblue;
			border:1px solid black;
			position: relative;
		}
		.box {
			width: 200px;
			height: 200px;
			font-size: 20px;
		}
		.box1{
			background-color: #888;
		}
		.box2{
			background-color:green;
			position: absolute;
			top:220px;
			left:20px;
			/* 
				脱离文档流
				与浮动的区别：
				1.浮动的时候补位的元素会把文字甩出去，
				2.而绝对定位这个，补位的元素会完整进入
				3.可以通过层级调整实现不同的效果
			*/
			/* 
				包含块的概念：
				1.没有脱离文档流的元素，其父元素就是他们的包含块
				2.脱离文档流的元素，第一个开启定位的祖先元素，就是他的包含块。
			*/
			/* 
				移动的参考点：
					相对于包含块，body和html都没开定位，但html已经到了最外层，如果没有祖先包含块，最终会相对他定位
			*/
			/* 
				绝对定位能与margin的关系，写了top才能用margin-top，其他同理
				但是不推荐二者一起用，因为有些浏览器不认这些规则
			*/
			/* 
				绝对定位的元素和浮动不可一起使用，如果一起使用只有绝对定位生效
			*/
			/* 
				最重要：无论是什么元素--块、行内、行内块,只要进行了绝对定位就会变成一种特殊的元素-- 定位元素

				ps:相对定位的元素还是本来的，不是定位元素
			*/
		}
		.box3{
			background-color: red;
		}
		/* 
			定位元素的特点：
			1.宽与高默认被内容撑开
			2.宽高可以设置
		*/

		.outer:hover .box2 {
			left: 220px;
		}

		/* 
			规范：
			1.子绝父相
			如果子元素有绝对定位，父元素就用相对定位，相对父元素，方便布局
			2.不要放弃浮动
			理论上全部布局使用绝对定位也可以，但是会增加浏览器的运算量，可能会崩溃
		*/
	</style>
</head>
<body>
	<div class="outer">
		<div class="box box1">1</div>
		<div class="box box2">2</div>
		<div class="box box3">3</div>
	</div>
</body>
</html>
```

### 3.固定定位

#### 3.1如何设置为固定定位

```sh
1.给元素设置'position:fixed'即可实现固定定位
2.可以使用'left'、'right'、'top'、'bottom'四个属性调整位置
```

#### 3.2 固定定位的参考点在哪里

>参考他的视口

```sh
什么是视口？
-- 对于PC浏览器来说，视口就是我们看网页的那扇"窗户"
-- 移动端有多个视口
```

#### 3.3 固定定位元素的特点

```sh
1.脱离文档流，会对后面的兄弟元素、父元素有影响。
2.left不能和right一起设置，top和bottom不能一起设置。
3.固定定位和浮动不能同时设置，如果同时设置，浮动失效，以固定定位为主。
4.固定定位的元素，也能通过margin调整位置，但不推荐这样做。
5.无论是什么元素(行内、行内块、块级)设置为固定定位之后，都变成了定位元素。
```

#### 举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>03_固定定位</title>
	<style>
		.outer {
			width: 500px;
			background-color: skyblue;
			border:1px solid black;
			
		}
		.box {
			width: 200px;
			height: 200px;
			font-size: 20px;
		}
		.box1{
			background-color: #888;
		}
		.box2{
			background-color:green;
			position: fixed;
			/* 
				固定定位
				1.脱离文档流
				2.参考点：视口

				与绝对定位的区别，
				绝对定位可以相对html定位达到类似效果，但是当内容过出现滚动条时，我们发现html就会出现滚动，绝对定位的元素和html绑定，定位的元素也会走

				而固定定位由于是参考视口，他会一直在那
			*/
		}
		.box3{
			background-color: red;
		}
		/* 
			固定定位可以使用margin，但有限制
			如果有top就可以用margin-top，其他同理，没有对应的位置，就不能用对应的margin
		*/
		/* 
			固定定位与浮动不能一起用，如果一起用，浮动会失效
		*/
		/* 
			无论是什么元素--块、行内、行内块,只要进行了固定定位就会变成一种特殊的元素-- 定位元素
		*/
	</style>
</head>
<body>
	<div class="outer">
		<div class="box box1">1</div>
		<div class="box box2">2</div>
		<div class="box box3">3</div>
	</div>
	<div>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Repellat itaque eligendi harum vitae, ex omnis ab enim! Fugiat eaque quisquam ducimus vitae provident voluptatem fuga maiores fugit ea. Odio hic facere nemo voluptatibus molestiae quas voluptate inventore et beatae omnis placeat iste magni, consectetur itaque illum reiciendis repellendus, alias asperiores voluptates praesentium harum perferendis soluta repellat id. Atque earum pariatur ipsum rem. Amet adipisci nemo, consequatur repellendus iusto saepe sunt suscipit perspiciatis velit optio eum at! Provident aut modi incidunt! Omnis, veritatis? Maiores consequatur eligendi quae magni, atque esse libero repudiandae, incidunt totam mollitia non eum natus ipsam fugiat officia modi itaque similique magnam iure tempore minima ipsa consequuntur sapiente? Ea similique impedit explicabo minus porro ipsum corrupti nobis, laboriosam hic nostrum libero, velit quod ad, debitis animi. Officia cumque natus odio ex! Provident nam, error architecto quas autem similique a quam sed, velit tempore consequuntur! Odio corporis vitae deserunt necessitatibus nemo ipsum, fugiat labore delectus modi officiis! Nesciunt a nostrum amet atque sit quo, aspernatur suscipit pariatur dolorum nulla. Accusamus illo, tempora sit sapiente eum nobis aliquam animi illum voluptates repellendus nemo nulla deleniti necessitatibus at amet veritatis ipsum maiores a corrupti maxime commodi hic accusantium? Alias fugiat sed delectus provident soluta ex, labore deserunt veniam quidem nam, similique quae quaerat maiores aperiam quam accusamus molestias ipsum quia neque nihil. Perferendis dolor ullam cupiditate quod delectus alias, atque facere neque? Eum, voluptas. Voluptatibus dolore, eveniet sint fugiat fugit nam officiis iste aliquam eum explicabo ea unde dolorum dolorem incidunt nesciunt repellat quidem quam deserunt nulla repudiandae magnam libero ex quasi? Iusto, eligendi voluptates molestiae et nemo officiis hic, architecto delectus, corrupti doloribus aperiam omnis rerum mollitia provident nesciunt quas temporibus eos totam harum vitae quasi optio enim amet! Amet est minus dolorum cumque voluptatem id fugiat, quisquam dignissimos, quas magnam laborum ducimus illum. Aut et delectus, impedit deserunt reiciendis sed ex voluptas commodi. Mollitia minus, atque sint iure eum delectus rem deleniti facere nemo fugiat distinctio earum aspernatur rerum odit, saepe tempora. Iste fugiat dolores placeat! Ex placeat rerum quae nostrum doloremque aperiam libero, iure quas suscipit impedit ea repudiandae culpa officiis, praesentium sed consequuntur alias. Eos tempore ullam eveniet quo dignissimos dolorem nisi quibusdam maiores delectus amet accusamus, accusantium corporis, sint id veritatis esse voluptatibus et? Blanditiis harum odit, dolores ad tempora sint perspiciatis aliquam ipsum provident nam delectus, culpa ab! Temporibus veritatis cumque perferendis vero enim magni nemo excepturi quia! Repudiandae repellendus laboriosam, dicta corporis magnam quidem! Aliquid accusantium praesentium optio sequi, placeat provident, sunt sit qui, magnam quisquam consequatur quam eos ipsam vel libero voluptas reprehenderit! Laboriosam placeat sint deserunt molestias sit enim architecto culpa asperiores sapiente soluta, omnis velit eaque modi laborum commodi ducimus! Maxime hic cumque commodi ab! Excepturi aliquid eos asperiores illo dolorem eaque dolores quibusdam reprehenderit placeat adipisci sequi praesentium incidunt suscipit eligendi impedit modi ab, tenetur nihil tempora a quisquam amet! Illo quisquam aperiam quia veniam tempore officia quibusdam, sint nisi nesciunt non accusantium iste quod mollitia. Libero, nesciunt. Est cumque enim eveniet, dignissimos dolore ea. Vel non modi quam sint hic iure ipsam nesciunt consequatur laudantium corporis facilis saepe impedit tempore cum nihil, culpa quo, odit voluptas aliquam fuga, distinctio aspernatur porro quaerat. Nihil deleniti, tenetur dolorem, aut distinctio quasi in adipisci ad consequatur ducimus fugit ex. Reiciendis voluptate corporis id vel magnam pariatur explicabo quia illo ipsam, placeat cupiditate dolor minima accusantium doloribus! Pariatur mollitia eaque velit facere quisquam accusamus at quidem maiores! Deserunt pariatur dolores laboriosam placeat laborum maxime. Deserunt ullam expedita, aut tempore doloribus reprehenderit! Distinctio ea cumque deserunt. Deleniti aperiam doloremque consequatur temporibus, veritatis provident mollitia iure expedita assumenda. Doloremque, et. Fugiat praesentium error necessitatibus provident perferendis quisquam voluptas distinctio? Quia illo doloribus porro iure maxime quibusdam dolore a ex quaerat hic expedita asperiores ullam omnis ipsa provident minus, saepe alias amet nemo magni magnam deleniti eius nam! Perspiciatis ipsam deleniti veniam quisquam voluptatum facere sint eum quod amet quo quas, quae ut distinctio, id iure dolorem atque, soluta natus sequi est optio ratione qui. Commodi eius itaque incidunt amet, adipisci est molestias aliquam repellendus et rerum quas animi quam, aliquid iusto maiores? Eligendi rerum dolor molestias labore veniam. Error perferendis illum repudiandae, rerum dolorum, nulla ex amet iusto, reprehenderit magni iure nihil optio porro aperiam exercitationem. Sit sapiente reiciendis unde porro natus distinctio est! Provident harum ipsam excepturi voluptatum dolor. Hic nulla voluptatum, aspernatur tempora beatae esse ipsa incidunt, necessitatibus ducimus error dolor modi illo dicta nostrum minus fugiat voluptates iusto sunt voluptas mollitia aperiam repellat. Culpa, atque quas? Nemo, nam quos, quam sint minus inventore at consequatur molestias ipsam rem nostrum tempora, sunt consequuntur fugit dolorem cumque aperiam temporibus iure! Quis animi at, delectus aut optio dignissimos voluptatem quidem aliquid quae doloremque, maxime eligendi voluptates iusto non dolore ullam molestias. Enim rerum sunt aut quisquam corrupti fugiat distinctio, magni dolore voluptatem delectus, porro expedita consequuntur molestias, excepturi nostrum eius aliquam illo itaque possimus dolor nulla totam provident. Itaque, ullam! Repudiandae, officiis impedit magni, ad nulla exercitationem dolorum sint quo rerum numquam repellendus voluptas? Hic consequatur suscipit architecto reiciendis? Necessitatibus eius molestias laboriosam quis. Praesentium quos ullam excepturi itaque deserunt, non consectetur aut ducimus, harum obcaecati officia veniam ipsam quisquam impedit! Praesentium officiis dicta sit quaerat, pariatur ducimus! Ratione quis architecto officia animi dignissimos iure suscipit aspernatur! Dolore accusamus at obcaecati repellat veniam nihil dicta natus ex, aspernatur praesentium. Fuga fugiat odit quam tempora libero modi ratione. Adipisci explicabo illum laudantium ut nesciunt autem accusantium repellendus, dolorem blanditiis natus nam mollitia assumenda ullam ad tempora neque excepturi illo quis sunt animi? Consequuntur in suscipit commodi molestiae sunt, ad dolores ipsam eius nulla provident inventore laudantium, minima totam labore. Rem, laborum recusandae quibusdam quidem iste quos sit deserunt corporis similique impedit quia officia vero odit amet excepturi quaerat fugiat velit error! Illum debitis ut quasi ipsam quo tempora, cumque voluptatibus doloremque quam animi consectetur aliquid omnis incidunt ipsa voluptatem magnam doloribus, sit aliquam odit reiciendis quos? In autem inventore eos ex. Reiciendis itaque illum iure aspernatur.</div>
</body>
</html>
```



### 4.粘性定位

#### 4.1如何设置为粘性定位？

```sh
1.给元素设置'position:sticky'即可实现粘性定位。
2.可以使用'left'、'right'、'top'、'bottom'四个属性调整位置，不过最常用的是'top'值
```

#### 4.2粘性定位的参考点在哪里?

```sh
离它最近的一个拥有"滚动机制"的祖先元素，即便这个祖先不是最近的真实可滚动祖先。
理解：如果我们给一个祖先加了overflow:scroll，那么他就会有滚动条，如果我们不给他高度，那么他的高度将被子元素撑开，自然就不会有滑块，那么也就不能滚动。
这就叫做有滚动机制，但是不是真实可滚动。
```

#### 4.3粘性定位元素的特点

```sh
1.不会脱离文档流，它是一种专门用于窗口滚动时的新的定位方式
2.最常用的值是'top'值
3.粘性定位和浮动可以同时设置，但不推荐这样做
4.粘性定位的元素，也能通过margin调整位置，但不推荐这样做
```

```sh
粘性定位和相对定位的特点基本一致，不同的是：粘性定位可以在元素到达某个位置时将其固定。
```

#### 4.4举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>4_粘性定位</title>
	<style>
		*{
			margin: 0;
			padding: 0;
		}
		/* 给body一个特别大的高度是为了实现滚动 */
		body {
			height: 2000px;
		}
		.page-header {
			/* 文字垂直居中，水平居中 */
			height: 100px;
			text-align: center;
			line-height: 100px;

			background-color: orange;
			font-size: 20px;
		}
		.item{
			background-color: #888;
		}
		.first {
			background-color: skyblue;
			font-size: 40px;
			position: sticky;
			/* 拥有滚动元素的祖先元素，即出现滚动条的祖先元素 */
			top:0px;
			/*
			 出现滚动条：
			 1.内容超出高度
			 2.加上overflow里面的auto或者scroll属性
			 */
		}
		/* 
			1.想要胶水粘住谁，就给谁加粘性定位
			2.加上位置和距离参考点的位置

			参考点是离他最近的一个拥有滚动行为的祖先元素

			胶水生效的时机：参考点的设置
			胶水失效的时机：包含粘性定位的父容器整个要消失的时候
		*/
	</style>
</head>
<body>
	<!-- 头部 -->
	<div class="page-header">
		头部区域
	</div>
	<!-- 内容区 -->
	<div class="content">
		<!-- 每一项 -->
		<div class="item">
			<div class="first">
				A
			</div>
			<h2>A1</h2>
			<h2>A2</h2>
			<h2>A3</h2>
			<h2>A4</h2>
			<h2>A5</h2>
			<h2>A6</h2>
			<h2>A7</h2>
			<h2>A8</h2>
		</div>
		<div class="item">
			<div class="first">
				B
			</div>
			<h2>B1</h2>
			<h2>B2</h2>
			<h2>B3</h2>
			<h2>B4</h2>
			<h2>B5</h2>
			<h2>B6</h2>
			<h2>B7</h2>
			<h2>B8</h2>
		</div>
		<div class="item">
			<div class="first">
				C
			</div>
			<h2>C1</h2>
			<h2>C2</h2>
			<h2>C3</h2>
			<h2>C4</h2>
			<h2>C5</h2>
			<h2>C6</h2>
			<h2>C7</h2>
			<h2>C8</h2>
		</div>
		<div class="item">
			<div class="first">
				D
			</div>
			<h2>D1</h2>
			<h2>D2</h2>
			<h2>D3</h2>
			<h2>D4</h2>
			<h2>D5</h2>
			<h2>D6</h2>
			<h2>D7</h2>
			<h2>D8</h2>
		</div>
	</div>
</body>
</html>
```

### 5定位层级

```sh
1.定位元素的显示层级比普通元素高，无论什么定位，显示层级都是一样的。
2.如果位置发生重叠，默认情况是：后面的元素，会显示在前面的元素之上。
3.可以通过css属性'z-index'调整元素的显示层级。
4.z-index的属性值是数字，没有单位，值越大显示层级越高。
5.只有定位的元素设置z-index才有效。
6.如果z-index值大的元素，依然没有覆盖掉z-index值小的元素，那么请检查其包含块的层级。
```

#### 举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>05_定位的层级</title>
	<style>
		/* 
				1.
				相对、绝对、固定、粘性 无论哪种定位，他们的层级都是一样的
				后出生的压在前生的上面，但层级相同
		
		*/
		/* 
				2. z-index
				代表在z轴的位置，值是一个数字，最大是正无穷
				默认是auto。浏览器一般会给个0，默认值都是0
				只有定位的元素才有 z-index
		*/
		/* 
			3.同包含块内，z-index越大的层级越高，不同包含块，考虑包含块的影响

			如果 box4的z-index为50，在outer外面有个z-index为40的box5
			在outer没有z-index的情况下，box5比box4层级低
			如果outer有z-index，但是值比box5小，那么box5的层级也会比box4高

			蛮绕的：
			核心就是注意一点，如果z-index值大的元素，依然没有覆盖掉z-index值小的元素，那么请检查其包含块的层级
		*/
		.outer {
			width: 500px;
			background-color: skyblue;
			border: 1px solid black;
			padding: 20px;
		}
		.box {
			width: 200px;
			height: 200px;
			font-size: 20px;
		}
		.box1 {
			background-color: #888;
		}
		.box2 {
			background-color: orange;
			position: relative;
			top:-150px;
			left: 50px;
		}
		.box3 {
			background-color: red;
			position:absolute;
			top: 130px;
			left: 130px;
		}
		.box4 {
			background-color: green;
			position: fixed;
			top: 200px;
			left: 200px;
		}
	</style>
</head>
<body>
	<!-- 
	
	 -->
	<div class="outer">
		<div class="box box1">1</div>
		<div class="box box2">2</div>
		<div class="box box3">3</div>
		<div class="box box4">4</div>
	</div>
</body>
</html>
```



### 6.定位的特殊应用

```sh
注意:
1.发生固定定位、绝对定位后,元素都变成了定位元素，默认内容被撑开，且依然可以设置宽高。
2.发生相对定位后，元素依然是之前的显示模式,例块元素还是块元素。
3.以下所说的特殊应用，只针对'绝对定位'和'固定定位'的元素，不包括相对定位的元素。
```

#### 定位可以越过padding

```sh
padding是盒子的一部分，而定位是针对整个盒子的
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>定位可以越过padding</title>
	<style>
		.outer {
			width: 800px;
			height: 600px;
			padding: 20px;
			background-color: #888;
			position: relative;
		}

		.inner {
			width: 200px;
			height: 200px;
			background-color: orange;
			position: absolute;
			top: 0;
			left: 0;
		}
		/* 
			原理：定位是针对盒子的，而padding是盒子的一部分
			所以定位会越过padding
		*/
	</style>
</head>
<body>
	<div class="outer">
		<div class="inner"></div>
	</div>
</body>
</html>
```

#### 让定位元素充满包含块

```sh
1.定位元素宽度要充满包含块，可以给定位元素同时设置'left'和'right'为'0'。
2.定位元素高度想与包含块一致，'top'和'bottom'设置为'0'。

3.'left'与'right'写相同的数字，表示左右都距离多少，如果不一样则'right'失效，上下同理。
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>07_定位的特殊应用1</title>
	<style>
		.outer {
			height: 400px;
			background-color: #888;
			position: relative;
		}
		.inner{
			background-color: orange;
			font-size: 20px;
			padding: 20px;
			border: 10px solid black;

			/* 
				使用绝对定位后就变成了定位元素，定位元素如果没有宽高则由内容撑满宽高
			*/
			position: absolute;
			top: 0;
			left: 0;
			right: 0;
			bottom: 0;
		}

		/* 
			需求：想让一个发生了绝对定位的元素，宽度撑满其整个包含块

			1.包含块没有给宽度 -- 所以想设置一样的宽度不可能
			2.使用width:100%,由于border和padding的存在，超出了包含块
			3.同时使用相同的left和right，表示左边留多少，右边留多少
			4.同时使用相同的top和bottom同理

			ps：只有左右或者上下一样的时候才有这效果，如果不一样，则只保留左和上的效果
		*/
	</style>
</head>
<body>
	<div class="outer">
		<div class="inner"></div>
	</div>
</body>
</html>
```

#### 让定位元素在包含块居中

* 方案一

  ```css
  left:0;
  right:0;
  top:0;
  bottom:0;
  margin:auto;
  ```

  >举例

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
  	<meta charset="UTF-8">
  	<meta http-equiv="X-UA-Compatible" content="IE=edge">
  	<meta name="viewport" content="width=device-width, initial-scale=1.0">
  	<title>08_定位的特殊应用2</title>
  	<style>
  		.outer {
  			height: 400px;
  			width: 800px;
  			background-color: #888;
  			position: relative;
  			
  		}
  		.inner{
  			width: 400px;
  			height: 100px;
  			background-color: orange;
  			position: absolute;
  
  			top: 0;
  			left: 0;
  			right: 0;
  			bottom: 0;
  			margin: auto;
  		}
  		/* 
  			需求：用定位让子元素在父元素中水平居中、垂直居中
  			由于子元素和父元素都有宽高，就不再是填充
  
  			设置位置均为0，加上margin:auto，就实现了完全居中
  		*/
  	</style>
  </head>
  <body>
  	<div class="outer">
  		<div class="inner">你好啊</div>
  	</div>
  </body>
  </html>
  ```

* 方案二

  ```css
  left:50%;
  top:50%;
  margin-left:负的宽度的一半;
  margin-top:负的高度的一半;
  ```

  >举例

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
  	<meta charset="UTF-8">
  	<meta http-equiv="X-UA-Compatible" content="IE=edge">
  	<meta name="viewport" content="width=device-width, initial-scale=1.0">
  	<title>09_定位的特殊应用3</title>
  	<style>
  		.outer {
  			height: 400px;
  			width: 800px;
  			background-color: #888;
  			position: relative;
  			
  		}
  		.inner{
  			width: 400px;
  			height: 100px;
  			background-color: orange;
  			position: absolute;
  
  			top: 50%;
  			left: 50%;
  			/* 
  				再往左边推回宽度的一半，往上边推回高度的一半
  				不同时用right和bottom，因为无效
  			*/
  			margin-left: -200px;
  			margin-top: -50px;
  		}
  		/* 
  			需求：用定位让子元素在父元素中水平居中、垂直居中
  			由于子元素和父元素都有宽高，就不再是填充
  
  			先left和top移动，在用margin回推
  
  			left配合margin-left
  			top配合margin-top
  
  			应用3和应用2效果一样，推荐应用2，因为应用3的调整计算量大
  		*/
  	</style>
  </head>
  <body>
  	<div class="outer">
  		<div class="inner">你好啊</div>
  	</div>
  </body>
  </html>
  ```

>注意

```sh
要实现居中，定位元素必须设置宽高。
如果没设置宽高，就变成铺满了。
```

## 布局

### 1.版心

```sh
1.在PC端网页中，一般都会有一个固定宽度且水平居中的盒子，来显示网页的主要内容，这是网页的版心。
2.版心的宽度一般是960-1200像素之间。
3.版心可以是一个，也可以是多个。
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>版心</title>
	<style>
		/* 
			由于显示器分辨率的不一样，网页设置就需要考虑宽度(高度自由撑开，因为横向滚动条是不能接受的，而纵向是常见的)，这时候就要设置版心

			先用一个大的div，不设置宽度，自动铺满
			然后中间设置一个盒子，宽度给960-1200，根据市场需求变化，这个盒子就是版心

			两边留白的区域，要么设置淡色背景，要么用背景图填充或者使用动态背景填补

			版心可以设置多个，按行来划分，用一个盒子打满屏幕，然后设置版心

			版心的名字可以随意起，一般约定为container


			响应式设置后，就把版心给弱化了
		*/
		.outer {
			border: 2px solid green;
		}
		.container{
			border:2px solid red;
			width: 960px;
			margin: 0 auto;
			text-align: center;
		}
	</style>
</head>
<body>
	<div class="outer">
		<div class="container">
			我是版心
		</div>
	</div>
</body>
</html>
```

### 2.布局_常用类名

|        位置        |          类名          |
| :----------------: | :--------------------: |
|     顶部导航条     |         topbar         |
|        页头        |  header、page-header   |
|        导航        | nav、navigator、navbar |
|       搜索框       |   search、search-box   |
| 横幅、广告、宣传图 |         banner         |
|      主要内容      |     content、main      |
|       侧边栏       |     aside、sidebar     |
|        页脚        |  footer、page-footer   |

### 3.重置默认样式

很多元素都有默认样式，比如：

```sh
1.'p'元素有默认的上下'margin'
2.'h1~h6'标题也有上下'margin'，且字体加粗
3.'body'元素有默认的'8px'外边距
4.超链接有默认的文字颜色和下划线
5.'ul'元素有默认的左'padding'
...
```

在早起，元素的默认样式能帮助开发者快速的绘制网页，但如今网页的设计越来越复杂，内容越来越多，而且很精细，这些默认的样式会给我们绘制页面带来麻烦；而且这些默认样式，在不同的浏览器上呈现出来的效果也不一样，所以我们需要重置这些默认样式。

#### 方案一:使用全局选择器

```css
*{
    margin:0;
    padding:0;
    ....
}
```

```sh
此种方法，在简单案例中可以用一下，但在实际开发中不会使用，因为'*'选择的是所有元素，而并不是所有元素都有默认样式；
当我们重置时，有时候是需要做特定处理的，比如：想让'a'元素的文字是灰色，其他元素文字是蓝色

例如我们想要去除a标签的下划线，如果使用通配选择器，那么页面里面的所有元素都会去除下划线，这明显不符合要求。
```

#### 方案二：reset.css

选择到具有默认样式的元素，清空其默认的样式。

```sh
经过reset后的网页，好似'一张白纸'，开发人员可根据设计稿，精细的去添加具体的样式。
```

可以自由定制，相当于别人写的一个css

#### 方案三：Normalize.css

`Normalize.css`是一种最新方案，它在清除默认样式的基础上，保留了一些有价值的默认样式。

```sh
官网地址：
http://necolas.github.io/normalize.css/
```

相对于`reset.css`,`Normalize.css`有如下的优点：

```sh
1.保护了有价值的默认样式，而不是完全去掉它们。
2.为大部分HTML元素提供一般化的样式。
3.新增对HTML5元素的设置。
4.对并集选择器的使用比较谨慎，有效避免调试工具杂乱。
```

>备注：`Normalize.css`的重置，和`reset.css`相比，更加的温和，开发时可根据实际情况进行选择。
>
>实际开发中，`reset.css`更多，因为`Normalize.css`还在推广阶段

## Css3

### Css3_简介

Css3是Css2的升级版本,他在Css2的基础上，新增了很多强大的新功能，从而解决一些实际面临的问题。

Css3在未来会按照模块化的方式去发展。

Css3的新特性如下：

```sh
新增了更加实用的选择器
新增了更好的视觉效果
新增了丰富的背景效果
新增了全新的布局方案 -- 弹性盒子
新增了Web字体
增强了颜色
增加了2D和3D变换
增加动画和过渡效果
...
```

### Css3_私有前缀

#### 什么是私有前缀

就是在正常属性的前面加个前缀，例如如下代码中的`-webkit-`就是私有前缀

```css
div {
    width:400px;
    height:400px;
    -webkit-border-radius:20px;
}
```

#### 为什么要有私有前缀

W3C标准所提出的某个CSS特性，在浏览器正式支持之前，浏览器厂商会根据浏览器的内核，使用私有前缀来测试该CSS特性，在浏览器正式支持该CSS特性后，就不需要私有前缀了。

>举例

```css
-webkit-border-radius:20px;
-moz-border-radius:20px;
-ms-border-radius:20px;
-o-border-radius:20px;

/*正常属性*/
border-radius:20px;
```

注意：把正常的属性写在最后面，有前缀的写前面



查询CSS3兼容性的网站：

```sh
http://caniuse.com/
```

#### 常见的浏览器私有前缀

```sh
"Chrome"   
-webkit-

"Safari"
-webkit-

"Firefox"
-moz-

"Edge"
-webkit-

"旧Opera"
-o-

"旧IE"
-ms-
```

#### 注意

```sh
我们在编码时，不用过于关注浏览器的私有前缀，不用绞尽脑汁的去记忆，也不用每个都去查询，因为常用的CSS3新特性，主流浏览器都是支持的，即便是为了老浏览器而加前缀，我们也可以借助现代的构建工具，帮我们添加私有前缀。

可以通过webpack配置自动添加
```

### Css3_新增长度单位

```sh
1.'rem'根元素字体大小的倍数，只与根元素字体大小有关。
2.'vw'视口宽度的百分比之多少，'10vw'就是视口宽度的'10%'
3.'vh'视口高度的百分比之多少，'10vh'就是视口高度的'10%'
4.'vmax'视口宽高中多的那个百分之多少
5.'vmin'视口宽高中少的那个百分之多少
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>新增长度单位</title>
	<style>
		*{
			margin: 0;
			padding: 0;
		}
		.box1{
			width: 200px;
			height: 200px;
			background-color: skyblue;
		}
		/* 
			vw 指的是视口宽度的多少
			v viewport  w width
			20vw 即视口宽度的20%

			优势：可以跟着视口变化，在移动端用的多
		*/
		.box2{
			width: 50vw;
			height: 20vw;
			background-color: green;
		}
		/* 
			vh 指的是视口高度的多少
			v viewport  h height
			20vh 即视口高度的20%

			相对来说vw用的比较多
		*/
		.box3{
			width: 50vh;
			height: 20vh;
			background-color: red;
		}
		/* 
			vmax 比较宽高，大的那个的多少
			20vmax  如果宽比高大，那么就是视口宽度的20%

			vmin 与vmax相反，他取小的
		*/
		.box4{
			width: 50vmax;
			height: 20vmax;
			background-color: red;
		}

	</style>
</head>
<body>
	<div class="box1">像素</div>
	<div class="box2">vw</div>
	<div class="box3">vh</div>
	<div class="box4">vmax</div>
</body>
</html>
```



### Css3_新增盒子属性

#### 1.box-sizing

使用`box-sizing`属性可以设置盒模型的两种类型

|   可选值    |                       含义                        |
| :---------: | :-----------------------------------------------: |
| content-box | width和height设置的是盒子内容区的大小。默认值是它 |
| border-box  |   width和height设置的是盒子总大小。(怪异盒模型)   |

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>box-sizing</title>
	<style>
		/* 
			box-sizing
			默认属性：content-box
			我们设置的宽高，控制内容区，不包括边框和padding

			可选属性：border-box
			我们设置的宽高，是盒子的总宽高，包括边框和padding，内容区的大小需要计算
		
		*/
		.box1 {
			width: 200px;
			height: 200px;
			background-color: skyblue;
			padding: 5px;
			border: 5px solid black;
		}
		.box2 {
			width: 200px;
			height: 200px;
			background-color: skyblue;
			padding: 5px;
			border: 5px solid black;
			box-sizing: border-box;
		}
	</style>
</head>
<body>
	<div class="box1"></div>
	<div class=box2></div>
</body>
</html>
```

#### 2.resize调整盒子大小

使用resize属性可以控制是否允许用户调节元素尺寸

|     值     |             含义             |
| :--------: | :--------------------------: |
|    none    | 不允许用户调整元素大小，默认 |
|    both    | 用户可以调节元素的宽度和高度 |
| horizontal |    用户可以调节元素的宽度    |
|  vertical  |    用户可以调节元素的高度    |

#### 3.box-shadow盒子阴影

使用box-shadow属性为盒子添加阴影

>语法

```css
box-shadow:h-shadow v-shoadow blur spread color inset;
```

>各个值的含义

|    值    |                 含义                 |
| :------: | :----------------------------------: |
| h-shadow | 水平阴影的位置，必须填写，可以为负值 |
| v-shadow | 垂直阴影的位置，必须填写，可以为负值 |
|   blur   |            可选，模糊距离            |
|  spread  |          可选，阴影的外延值          |
|  color   |           可选，阴影的颜色           |
|  inset   |     可选，将外部阴影改为内部阴影     |

>默认值

```css
box-shadow:none;
/*表示没有阴影*/
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>盒子阴影</title>
	<style>
		.box1 {
			width: 400px;
			height: 400px;
			background-color: orange;
			margin: 0 auto;
			margin-top: 100px;

			/* 
			1)
				两个值，含义: 水平位置 垂直位置
				第一个值，水平方向阴影的位置
				第二个值，垂直方向阴影的位置
				在原盒子的背后有一个一样大小的投影，通过值控制相对原盒子左边和上边的距离
			
			*/
			/* box-shadow: 10px 10px; */
			/* ****************************************************************************** */

			/* 
				2)三个值，含义:水平位置 垂直位置 阴影的颜色
				···
				第三个值，颜色，默认是黑色
			
			*/
			/* box-shadow: 10px 10px blue; */
			/* ****************************************************************************** */

			/* 
				3)三个值，含义：水平位置 垂直位置 模糊程度
				...
				第三个值模糊程度，值越大越模糊
			*/
			/* box-shadow: 10px 10px 10px; */

			/* ****************************************************************************** */
			/* 
				4）四个值，含义：水平位置 垂直位置 模糊程度 阴影颜色
			*/
			/* box-shadow: 10px 10px 20px blue; */


			/* ****************************************************************************** */
			/* 
				5)五个值，含义：水平位置 垂直位置 模糊程度 阴影的外延 阴影颜色
				阴影的外延 后边阴影外四周延伸的大小
			*/
			/* box-shadow: 10px 10px 20px 10px blue; */

			/* ****************************************************************************** */
			/* 
				6)五个值，含义：水平位置 垂直位置 模糊程度 阴影的外延 阴影颜色 是否内阴影
				最后的值 不写就是外阴影，写inset就是内阴影
				
			*/
			box-shadow: 10px 10px 20px 10px blue inset;

		}
	</style>
</head>
<body>
	<div class="box1"></div>
</body>
</html>
```

#### 4.opacity不透明度

`opacity`属性能为整个元素添加透明效果，值是0到1之间的小数，0是完全透明，1表示完全不透明。

```sh
opacity与rgba的区别？
opacity是一个属性，设置的是整个元素(包括元素里的内容)的不透明度。
rgba是颜色的设置方式，用于设置颜色，他的透明度，仅仅是调整颜色的透明度。
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>不透明性</title>
	<style>
		.box1 {
			width: 200px;
			height: 200px;
			background-color: orange;
			font-size: 40px;
			/* 
				调整整个盒子与里面内容的透明度
				最小值是0，盒子还在，只是隐身了

				取值为0~1，0完全透明，1完全不透明，默认为1
			*/
			opacity: 0.5;
		}
	</style>
</head>
<body>
	<div class="box1">你好啊</div>
</body>
</html>
```

### Css3_新增背景属性

#### 1.background-origin

>作用

```sh
设置背景图的原点
```

>语法

```sh
1.padding-box  从padding区域开始显示背景图像--默认值
2.border-box   从border区域开始显示背景图像
3.content-box  从content区域开始显示背景图像
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>background-origin</title>
	<style>
		/* 
			background-origin 背景图的原点
		*/
		.box1 {
			width: 400px;
			height: 400px;
			background-color: orange;
			margin: 0 auto;
			margin-top: 40px; 
			padding: 50px;
			font-size: 40px;
			border: 50px dashed black;

			/* 
				图片原点：	
				默认，原点从padding左上角开始
				
				纵向排不下，溢出的部分会到最上方，横向也一样，像一个卷轴一样
			*/
			background-image: url('../../img/R-C.jpeg');
			background-repeat: no-repeat;

			/* 
				1.默认值 padding-box 以padding左上角为原点
				2.content-box  以content内容区的左上角为原点
				3.border-box   以border左上角为原点
			*/
			background-origin: padding-box;
		}
	</style>
</head>
<body>
	<div class="box1">你好啊</div>
</body>
</html>
```

#### 2.background-clip

>作用

设置背景图的向外裁剪的区域。

>语法

```sh
1.border-box 从boder区域开始往外裁剪背景，--默认值
2.padding-box 从padding区域开始向外裁剪背景
3.content-box 从content区域开始向外裁剪背景
4.text 背景图只呈现在文字上
# 注意
若为text，那么background-clip要加上-webkit-前缀
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>background-clip</title>
	<style>
		/* 
			background-clip 背景图修剪
		*/
		.box1 {
			width: 400px;
			height: 400px;
			background-color: orange;
			margin: 0 auto;
			margin-top: 40px; 
			padding: 50px;
			font-size: 40px;
			border: 50px dashed black;

			background-image: url('../../img/R-C.jpeg');
			background-repeat: no-repeat;

			/* 
				不仅影响到背景图片还影响到背景色
				1.默认值 border-box 边界之外的背景不可见
				2.padding-box  padding以外的背景不可见
				3.content-box  超出内容区的背景不呈现
				4.text         让背景呈现在文字上，前提，文字的字体颜色得透明

				第4点在实验中，需要前缀，不推荐大量使用
				文字的字体颜色得透明 color:transparent
			*/
			background-clip: border-box;
		}
		/* 
			background-clip和background-origin可以一起用
		*/
	</style>
</head>
<body>
	<div class="box1">你好啊</div>
</body>
</html>
```

#### 3.background-size

>作用

```sh
设置背景图的尺寸
```

>语法

1.用长度值指定背景图片大小，不允许负值

```css
background-size:300px 200px;
```

2.用百分比指定背景图片大小，不允许负值

```css
background-size:100% 100%;
```

3.auto：背景图片的真实大小。--默认值

4.contain:将背景图片等比缩放，使得背景图片的宽或者高，与容器的宽或者高相等，在将完整背景图片包含在容器内，但要注意：可能会造成容器里部分区域没有背景图片

```css
background-size:contain;
```

5.cover：将背景图片等比缩放，直到完全覆盖容器，图片会尽可能全的显示在元素上，但要注意：背景图片有可能显示不完整。--相对比较好的选择。

```css
background-size:cover;
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>background-size</title>
	<style>
		div{
			width: 400px;
			height: 400px;
			border:1px solid black;

			background-image: url('../../img/R-C.jpeg');

			/* 
				1）两个值： 背景图的宽 背景图的高
				缺点：会造成背景图被压缩或者拉伸
			*/
			/* background-size: 400px 400px; */

			/* ****************************************************************************** */

			/* 
				2）两个值： 背景图的宽 背景图的高
				值除了可以写像素还可以写百分比，参考元素的宽高
				缺点：会造成背景图被压缩或者拉伸
			*/
			/* background-size: 100% 100%; */
			/* ****************************************************************************** */
			/* 
				3）contain 把图片进行等比例缩放，把长的都装里面
				等比缩放后，不足的用背景重复来填充，可以用background-repeat来调整是否重复

				特点：不破坏宽高比例
			*/
			/* background-size: contain; */

			/* ****************************************************************************** */
			/* 
				4）cover 
				等比例缩放，按照短边来，

				没有最完美的解决方案，得靠图片和网页设计师设计，目前采用最多的是cover
			*/
			background-size: cover;
			/* 
				默认是auto，不推荐
			*/
		}
	</style>
</head>
<body>
	<div class="box1"></div>
</body>
</html>
```

#### 4.background-复合属性

>语法

```css
background:color url repeat position / size origin clip;
```

>注意

```sh
1.origin和clip的值如果一样，如果只写一个值，则origin和clip都设置；如果设置了两个值，前面的是origin，后面的是clip
2.size必须写在position后面，并且使用'/'分开

# 除了这两个注意事项，其他顺序实际上可以乱，只是不建议乱
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>background-复合属性</title>
	<style>
		.box1 {
			width: 400px;
			height: 400px;
			margin: 0 auto;
			margin-top: 40px; 
			padding: 50px;
			font-size: 40px;
			border: 50px dashed black;

			/* background: 背景颜色 背景url 是否重复 位置/大小 原点 裁剪方式; */
			background:orange url('../../img/R-C.jpeg') no-repeat 10px 10px / 500px 500px border-box content-box  ;
			/* 10px 10px 是位置 斜杆后的 500px 500px 是大小 */
			/* 不是很推荐复合属性，分开写可读性更强，在一起只是减少了代码量 */
		}
	</style>
</head>
<body>
	<div class="box1">你好啊</div>
</body>
</html>
```

#### 5.多背景图

Css3允许设置多个背景图片

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>多背景图片</title>
	<style>
		div{
			width: 400px;
			height: 400px;
			border: 1px solid black;

			/* 多个之间用逗号隔开，可以换行更清晰，只有复合属性支持 */
			background: url('#1') no-repeat left top,
						url('#2') no-repeat right top,
						url('#2') no-repeat left bottom,
						url('#2') no-repeat right bottom;
		}
	</style>
</head>
<body>
	<div></div>
</body>
</html>
```

### CSS3_新增边框属性

#### 1.边框圆角

在CSS3中，使用border-radius属性可以将盒子变为圆角。

同时设置四个角的圆角:

```css
border-radius:10px;
```

分开设置每个角的圆角(几乎不用):

|          属性名           |                             作用                             |
| :-----------------------: | :----------------------------------------------------------: |
|  border-top-left-radius   | 设置左上角圆角半径<br>1.一个值是正圆半径<br>2.两个值分别是椭圆的x半径、y半径 |
|  border-top-right-radius  | 设置右上角圆角半径<br/>1.一个值是正圆半径<br/>2.两个值分别是椭圆的x半径、y半径 |
| border-bottom-left-radius | 设置右下角圆角半径<br/>1.一个值是正圆半径<br/>2.两个值分别是椭圆的x半径、y半径 |
| border-bottom-left-radius | 设置左下角圆角半径<br/>1.一个值是正圆半径<br/>2.两个值分别是椭圆的x半径、y半径 |

分开设置每个角的圆角，综合写法

```css
border-radius：左上角x 右上角x 右下角x 左下角x / 左上角y 右上角y 右下角y 左下角y;
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>边框圆角</title>
	<style>
		div {
			width: 400px;
			height: 400px;
			border:2px solid black;
			margin: 0 auto;
			/* 
				快捷键 borr
				值是半径，从最早产生弧度的地方划线，最后能得到一个扇形

				由原理可知半径最大为边长的一半，再大也会是这个
			*/
			/* border-radius: 50px; */
			

			/* 百分比指的是边长的百分比 */
			/* border-radius: 10%; */

			/* ************************单边圆角************************************/
			/* 单独设置每边的圆角 */
			/* 左上角 用 top-left */
			/*
				border-top-left-radius: 10px;
				border-top-right-radius: 10px;
				border-bottom-left-radius: 10px;
				border-bottom-right-radius: 10px; 
			*/

			/* **************************单边椭圆***********************************/
			/* 设置椭圆，第一个值是x轴，第二个值是y轴 */
			/* border-top-left-radius:10px 20px;
			border-top-right-radius:15px 25px;
			border-bottom-left-radius: 16px 26px;
			border-bottom-right-radius: 19px 29px;  */
			/* **************************复合椭圆***********************************/
			/* 复合时，从左上角开始顺时针开始 */
			/* 斜杆前是 左上 右上 右下 左下的x轴值 斜杠后是对应顺序的y轴值 */
			/* border-radius: 10px 15px 16px 19px / 20px 25px 26px 29px; */

			/* **************************复合圆角***********************************/
			/* 复合时，从左上角开始顺时针开始 */
			border-radius: 10px 15px 16px 19px;
		}
	</style>
</head>
<body>
	<div></div>
</body>
</html>
```

#### 2.边框外轮廓

>外轮廓的宽度

```css
outline-width
```

>外轮廓的颜色

```css
outline-color
```

>外轮廓的风格

```css
outline-style
none 无轮廓
dotted 点状轮廓
dashed 虚线轮廓
solid 实线轮廓
double 双线轮廓
```

>轮廓偏移量

```css
outline-offset
```

```sh
设置外轮廓与边框的距离，正负值都可以设置。
注意:outline-offset不是outline的子属性，是一个独立的属性
```

>outline复合属性
>
>和boder类似

```css
outline: 20px blue solid;
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>02_边框外轮廓</title>
	<style>
		.box1 {
			width: 400px;
			height: 400px;
			padding: 10px;
			border: 10px solid black;
			background-color: gray;
			font-size: 40px;
			margin: 0 auto;
			margin-top: 100px;

			/* 
			外轮廓特点:
				1.外轮廓在盒子border外面，
				2.不参与计算盒子大小，
				3.开发者工具看不到
				4.不占位
				outline-width 外轮廓宽度
				outline-color 外轮廓颜色
				outline-style 虚线、实线..
				outline-offset 偏移量，正值离盒子越来越远，负值在盒子内，不发生挤压
			*/
			/* outline-width: 20px;
			outline-color: blue;
			outline-style: solid;
			outline-offset: 5px; */


			/* ******************************************************************/
			/* 复合属性 */
			outline: 20px blue solid;
			/* 注意：outline-offset不是outline的子属性，所以也就不能写到复合属性中 */
			outline-offset: 5px;

			/* 理解：外轮廓就像盒子发出的光 */
		}
	</style>
</head>
<body>
	<div class="box1"></div>
</body>
</html>
```

### CSS3_新增文本属性

#### 1.文本阴影

>介绍

在Css3中，我们可以使用`text-shadow`属性给文本添加阴影。

>语法

```css
text-shadow:h-shadow v-shadow blur color;
```

|     值     |               描述               |
| :--------: | :------------------------------: |
| `h-shadow` | 必需写，水平阴影的位置，允许负值 |
| `v-shadow` | 必需写，垂直阴影的位置，允许负值 |
|   `blur`   |         可选，模糊的距离         |
|  `color`   |         可选，阴影的颜色         |

默认值:（表示没有阴影）

```css
text-shadow:none;
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>01_文本阴影</title>
	<style>
		/* 与盒子阴影相比没有外延值和内部阴影 */
		h1{
			font-size: 80px;
			text-align: center;
			/* text-shadow:水平位置 垂直位置  模糊值 阴影颜色*/
			text-shadow: 3px 3px 10px red;
		}
		/* 
			场景：白色的背景，白色的文字，通过阴影显示文字
			偏移值都给0px
			text-shadow:0px 0px 10px black;
		*/
		p {
			font-size: 40px;
			color: white;
			text-align: center;
			text-shadow: 0px 0px 10px black;
		}
		/* 
			光晕效果
			把背景色调成黑色，就像关灯了一样，文字调成白色
			通过添加文字阴影实现光晕效果
		*/
		div {
			background-color: black;
			width: 400px;
			height: 400px;
			margin: 0 auto;
			text-align: center;
		}
		div>p{
			color: white;
			text-shadow: 0px 0px 10px red;
		}
	</style>
</head>
<body>
	<h1>你好啊</h1>
	<p>我是白色的</p>
	<div>
		<p>我是光晕</p>
	</div>
</body>
</html>
```

#### 2.文本换行

>介绍

在`Css3`中，我们可以使用`white-space`属性设置文本换行样式。

>常用值如下

|     值     |                             含义                             |
| :--------: | :----------------------------------------------------------: |
|  `normal`  | 文本超出边界自动换行，文本中的换行被浏览器识别为一个空格。默认值 |
|   `pre`    |              原样输出，与`pre`标签的效果类似。               |
| `pre-wrap` |         在`pre`效果的基础上，超出元素边界自动换行。          |
| `pre-line` | 在`pre`效果的基础上，超出元素边界自动换行，且识别文本的换行，始末无效空格会被忽略 |
|  `nowrap`  |                          强制不换行                          |

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>02_文本换行</title>
	<style>
		div {
			width: 400px;
			height: 400px;
			border:1px solid black;
			font-size: 20px;
			/* 
			pre  按原文显示，代码怎么写怎么展示 
			pre-wrap 按原文显示，但是特别长的自动换行
			pre-line 按原文显示，但文字始末无效的空格被清除了，中间的空格保留
			nowrap  不换行
			*/
			white-space: pre-wrap;
		}
	</style>
</head>
<body>
	<!-- 代码里面的换行都会被浏览器认为是空格，多次换行认为是一个空格 -->
	<div>
		床前明月光,
		疑是地上霜,
		举头望明月,
		低头思故乡。
		床前明月光,
		疑是地上霜,
		举头望明月,举头望明月,举头望明月,举头望明月,举头望明月,举头望明月,举头望明月,
		低头思故乡。
		床前明月光,
		疑是地上霜,
		举头望明月,
		低头思故乡。
		床前明月光,
		疑是地上霜,
		举头望明月,
		低头思故乡。
	</div>
</body>
</html>
```

#### 3.文本溢出

>介绍

在`CSS3`中，我们可以使用`text-overflow`属性设置文本内容溢出时的呈现模式。

>常用值

|     值     |                     含义                      |
| :--------: | :-------------------------------------------: |
|   `clip`   |    当内联内容溢出时，将溢出的部分裁切掉。     |
| `ellipsis` | 当内联内容溢出块容器时，将溢出的部分转换为... |

>注意

```sh
要使得text-overflow属性生效，块容器必须显式定义`overflow`为非`visible`值，`white-space`为`nowrap`值。
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>03_文本溢出</title>
	<style>
		ul {
			width: 400px;
			height: 400px;
			border: 1px solid black;
			padding-left: 0;
			list-style: none;
		}
		li {
			margin-bottom: 10px;

			/* 不换行 */
			white-space: nowrap;
			overflow: hidden;
			/* 
				控制文本溢出
				text-overflow
				常用值：(都必须配合overflow:hidden才能生效)
				clip 超出部分的文字截掉
				ellipsis 超出部分截掉，末尾变成省略号
			 */
			 text-overflow: ellipsis;
		}
	</style>
</head>
<body>
	<ul>
		<!-- 故意写的长短不一，方便演示文本溢出 -->
		<li>惺惺惜惺惺休息休息详细信息嘻嘻嘻嘻信息嘻嘻嘻嘻</li>
		<li>惺惺惜惺惺休息休息详细</li>
		<li>惺惺惜惺惺休息休息详细嘻嘻嘻休息啊发的方法按时范德萨发生加法器</li>
		<li>惺惺惜惺惺休息休息详细信息嘻嘻嘻嘻</li>
		<li>惺惺惜惺细信息嘻嘻嘻嘻</li>
	</ul>
</body>
</html>
```

#### 4.文本修饰

>介绍

`Css3`升级了`text-decoration`属性，让其变成了复合属性。

```css
text-decoration:text-decoration-line||text-decoration-style||text-decoration-color
```

>子属性及其含义

```sh
#设置文本装饰线位置
text-decoration-line
#可选值
none 指定文字无装饰线
underline 指定文字的装饰线是下划线
overline 指定文字的装饰线是上划线
line-through 指定文字的装饰线是贯穿线
```

```sh
#文本装饰线条的形状
text-decoration-style
#可选值
solid 实线
double 双线
dotted 点状线条
dashed 虚线
wavy 波浪线
```

```sh
#文本装饰线条的颜色
text-decoration-color
```

#### 5.文本描边

注意：文字描边功能仅`webkit`内核浏览器支持。

```css
/*设置描边的颜色*/
-webkit-text-stroke-color
/*设置描边的宽度*/
-webkit-text-stroke-width
/*设置描边 宽度 颜色*/
-webkit-text-stroke
```

### CSS3新增渐变

#### 1.线性渐变

> 多个颜色之间的渐变，默认从上到下

```css
background-image: linear-gradient(red,yellow,green);
```

>使用关键字设置线性渐变方向

```css
background-image: linear-gradient(to right,red,yellow,green);
```

>使用角度设置线性渐变的方向

```css
background-image: linear-gradient(20deg,red,yellow,green);
```

>调整渐变开始的位置

```css
background-image: linear-gradient(red 50px,yellow 100px,green 150px);
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>线性渐变</title>
	<style>
		/* 
			线性渐变
			给颜色画一条线，颜色是线性变化的
		*/
		.box {
			width: 300px;
			height: 200px;
			border: 1px solid black;
			margin-left: 50px;
			float: left;
		}
		/* 所谓的渐变，本质上就是一个背景图片，不过这个图片是我们用代码构造出来的 */
		.box1 {
			/* 
				linear-gradient(颜色列表) 默认从上到下线性渐变,颜色列表个数无限，以逗号隔开
			*/
			background-image: linear-gradient(red,yellow,green);
		}
		.box2 {
			/* 
				linear-gradient(颜色排列方向，颜色列表)
				颜色排列方向--关键词方法
				to right 颜色列表从左往右
				to left 颜色列表从右往左
				to right top 颜色列表从左下往右上

				to 方向
			*/
			background-image: linear-gradient(to right,red,yellow,green);
		}
		.box3 {
			/* 
				linear-gradient(颜色排列方向，颜色列表)
				颜色排列方向--角度
				整个渐变线的旋转角度，可以画一个轴线，角度就是那个夹角

				可以用定时器实现炫光效果
			*/
			background-image: linear-gradient(20deg,red,yellow,green);
		}
		.box4 {
			/* 
				颜色列表后跟距离，表示到这个节点才变纯色，不加就是均匀分布
				50px 纯红线，50px之前没有别的颜色，故为纯红
				50px~100px 由红变黄，100px为纯黄线
				100px~150px 由黄变绿，150px为纯绿线
				150px之后没有别的颜色，故为纯绿
            
            	距离区间可以是数值也可以是百分比
			*/
			background-image: linear-gradient(red 50px,yellow 100px,green 150px);
		}
		.box5 {
			background-image: linear-gradient(20deg,red 50px,yellow 100px,green 150px);
			font-size: 80px;
			text-align: center;
			line-height: 200px;
			font-weight: bold;
			color: transparent;
			/* 让背景只呈现在文字上 */
			-webkit-background-clip:text;
		}
	</style>
</head>
<body>
	<!-- div.box.box1 生成两个类名-->
	<div class="box box1">默认情况(从上到下)</div>
	<div class="box box2">关键词调节线性渐变方向</div>
	<div class="box box3">角度调节线性渐变方向</div>
	<div class="box box4">调节线性渐变区域</div>
	<div class="box box5">你好啊</div>

</body>
</html>
```

#### 2.径向渐变

>多个颜色之间的渐变，默认从圆心四散。（注意：不一定是正圆，要看容器本身宽高比）

```css
background-image: radial-gradient(red,yellow,green);
```

>使用关键词调整渐变圆的圆心位置

```css
background-image: radial-gradient(at right,red,yellow,green);
```

>使用像素值调整渐变圆的圆心位置

```css
background-image: radial-gradient(at 100px 50px,red,yellow,green);
```

>调整渐变形状为正圆

```css
background-image: radial-gradient(circle,red,yellow,green);
```

>调节形状的半径

```css
background-image: radial-gradient(100px 100px,red,yellow,green);
```

>调节开始渐变的位置

```css
background-image: radial-gradient(red 50px,yellow 100px ,green 150px);
```

>综合写法

```css
background-image: radial-gradient(100px 50px at 150px 150px,red 50px,yellow 100px ,green 150px);
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>径向渐变</title>
	<style>
		/* 所谓径向渐变，就是椭圆或者圆的半径，像套圈一样一圈圈变化 */
		.box {
			width: 300px;
			height: 200px;
			border: 1px solid black;
			margin-left: 50px;
			float: left;
			font-size: 20px;
			margin-top: 20px;
		}
		.box1{
			/* 
				radial-gradient(颜色列表) 
				是椭圆还是圆取决于容器，正方形容器就是圆形
				颜色默认沿着半径从内往外
			*/
			background-image: radial-gradient(red,yellow,green);
		}
		.box2 {
			/* 
				radial-gradient(圆心位置，颜色列表) 
				关键词调整圆心位置
				at left 
				at right top
			*/
			background-image: radial-gradient(at right,red,yellow,green);
		}
		.box3 {
			/* 
				radial-gradient(圆心位置，颜色列表) 
				坐标调整圆心位置，坐标原点是容器左上角
				at x轴 y轴 
				at 50px 50px
			*/
			background-image: radial-gradient(at 100px 50px,red,yellow,green);
		}
		.box4 {
			/* 
				radial-gradient(调节圆形，颜色列表) 
				一般椭圆还是正圆是由容器决定的，但是我们可以通过参数强制改变
			*/
			background-image: radial-gradient(circle,red,yellow,green);
		}
		.box5 {
			/*
				radial-gradient(圆的半径，颜色列表) 
				圆的半径要写两个吗，代表横轴和纵轴，一样则为正圆，不一样就是椭圆
			*/
			background-image: radial-gradient(100px 100px,red,yellow,green);
		}
		.box6 {
			/*
				radial-gradient(颜色列表) 
				颜色列表的颜色后面跟数值或百分比 代表渐变的区域，起点是圆心
			*/
			background-image: radial-gradient(red 10%,yellow 40% ,green 80%);
		}
		.box7 {
			/* 
				综合写法
				radial-gradient(圆形形状，圆心位置，颜色列表) 
			*/
			background-image: radial-gradient(100px 50px at 150px 150px,red 50px,yellow 100px ,green 150px);
		}
	</style>
</head>
<body>
	<div class="box box1">默认情况(从内往外)</div>
	<div class="box box2">关键词调节径向渐变圆心位置</div>
	<div class="box box3">坐标调节径向渐变圆心位置</div>
	<div class="box box4">通过关键字circle调整为正圆</div>
	<div class="box box5">通过像素值调整圆的形状</div>
	<div class="box box6">通过径向渐变的区域</div>
	<div class="box box7">综合写法</div>
</body>
</html>
```

#### 3.重复渐变

>介绍

```sh
就是在线性渐变和径向渐变属性前面加前缀"repeating"
重复渐变本质上：在没有发生渐变的区域，重新开始渐变，就是重复渐变

所以一般只有我们给了渐变区间后才会生效，因为不给区间，默认均匀所有都产生渐变，就不存在未渐变的区域
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>线性渐变</title>
	<style>
		/* 
		重复渐变
		必须建立在线性渐变或径向渐变的基础上
		*/
		.box {
			width: 300px;
			height: 200px;
			border: 1px solid black;
			margin-left: 50px;
			float: left;
		}
		/* 
			所谓的重复渐变，本质上就是修改属性，加上repeating前缀 
			重复渐变的定义：在没有发生渐变的区域，重新开始渐变，就是重复渐变
		*/
		.box1 {
			
			background-image: repeating-linear-gradient(red,yellow,green);
		}
		.box2 {
	
			background-image: repeating-linear-gradient(to right,red,yellow,green);
		}
		.box3 {

			background-image: repeating-linear-gradient(20deg,red,yellow,green);
		}
		.box4 {
			/* 
				重复渐变生效：
				因为我们给定了渐变的区域，没有指定到的区域是纯色补充的，这时候重复渐变就会生效
				50px 是纯红色线，0~50px按照重复渐变就会是 黄到红
				150px是纯绿色线，150px~200px就会是 红到黄
				即重复渐变就是去找他之后的，循环来
			*/
			background-image: repeating-linear-gradient(red 50px,yellow 100px,green 150px);
		}
		.box6 {
			/*
				重复渐变生效
			*/
			background-image: repeating-radial-gradient(red 10%,yellow 40% ,green 80%);
		}
		
	</style>
</head>
<body>
	<!-- div.box.box1 生成两个类名-->
	<div class="box box1">默认情况(从上到下)</div>
	<div class="box box2">关键词调节线性渐变方向</div>
	<div class="box box3">角度调节线性渐变方向</div>
	<div class="box box4">调节线性渐变区域--重复渐变生效</div>
	<div class="box box6">通过径向渐变的区域--重复渐变生效</div>

</body>
</html>
```

#### 4.渐变案例

>行格纸

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>渐变案例1--行格纸</title>
	<style>
		.box1{
			width: 600px;
			height: 800px;
			padding: 20px;
			border: 1px solid black;
			margin: 0 auto;

			/* 第一步，设计渐变 */
			/* background-image: linear-gradient(transparent 0px,transparent 29px,gray 30px); */
			/* 第二步，添加重复渐变 */
			background-image: repeating-linear-gradient(transparent 0px,transparent 29px,gray 30px);
			/* 第三步，添加裁剪 */
			background-clip: content-box;
		}
	</style>
</head>
<body>
	<div class="box1"></div>
</body>
</html>
```

>立体小球

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>渐变案例2</title>
	<style>
		.box2{
			width: 200px;
			height: 200px;

			border-radius: 50%;
			/* 第一步，基础渐变*/
			/* background-image: radial-gradient(white,gray); */

			/* 第二步，加立体感 */
			background-image: radial-gradient(at 80px 80px,white,gray);

			/* 实际上就是视觉欺骗 */

		}
	</style>
</head>
<body>
	<div class="box2"></div>
</body>
</html>
```

### CSS3_Web字体

#### 1.基本用法

可以通过`@font-face`指定字体的具体地址，浏览器会自动下载该字体，这样就不依赖用户电脑上的字体了。

>简易格式

```css
@font-face {
    /* 随意取名，未来要用的就是这个名 */
    font-family:"abc";
    /* url里面的地址可以是本地地址也可以是网络地址 */
    src:url("../../font/Alifont/webfont.ttf")

    /* 
        优点：
        不必下载安装字体，项目上线直接给服务器地址，这里引入即可

        缺点：
        字体文件很大，引入慢，会造成网页崩溃

        解决方案：
        定制字体，字体文件之所以大，是因为他包含所有汉字，如果我们只需支持我们需要的某些汉字，name字体文件就小了
        借助外部网站事先制作定制字体，例如 https://www.iconfont.cn/webfont
    */
}
```

>高兼容性

```css
/* 所以参考其demo写最完整的引入写法，再根据自己的文件路径进行修改 */
/* 推荐使用这种方式，兼容性好 */
@font-face {
    font-family: "myfont";
    font-display: swap;
    /* 支持ie9 */
    src:url("../../font/Alifont/webfont.eot"); 
    /* 支持ie6-ie8 */
    src: url("../../font/Alifont/webfont.eot?#iefix") format("embedded-opentype"),
    url("../../font/Alifont/webfont.woff2") format("woff2"),
    /* chrome\firefox */
    url("../../font/Alifont/webfont.woff") format("woff"),
    /* chrome、firefox、opera、safari、Android 、IOS4.2+*/
    url("../../font/Alifont/webfont.ttf") format("truetype"),
    /* ios 4.1- */
    url("../../font/Alifont/webfont.svg#webfont") format("svg");
}
```

#### 2.定制字体

中文的字体文件很大，使用完整的字体文件不现实，通常针对某几个文字进行单独定制。

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>web字体</title>
	<style>
		/* 
			css2中我们通过字体族font-family控制字体样式，
			缺点：必须得事先安装，否则不生效
		*/
		/* 
			CSS3的做法，下载字体文件ttf或者得到他的链接地址
			使用 @font-face
		*/
		@font-face {
			/* 随意取名，未来要用的就是这个名 */
			font-family:"abc";
			/* url里面的地址可以是本地地址也可以是网络地址 */
			src:url("../../font/Alifont/webfont.ttf")

			/* 
				优点：
				不必下载安装字体，项目上线直接给服务器地址，这里引入即可

				缺点：
				字体文件很大，引入慢，会造成网页崩溃

				解决方案：
				定制字体，字体文件之所以大，是因为他包含所有汉字，如果我们只需支持我们需要的某些汉字，name字体文件就小了
				借助外部网站事先制作定制字体，例如 https://www.iconfont.cn/webfont
			*/
		}
	

		/* 
			字体文件下下来是个压缩包，解压出来是一堆文件
			eot svg ttf woff woff2 都是字体文件
			原因是不同浏览器认的字体格式不一样
		*/
		/* 所以参考其demo写最完整的引入写法，再根据自己的文件路径进行修改 */
		/* 推荐使用这种方式，兼容性好 */
		@font-face {
			font-family: "myfont";
			font-display: swap;
			/* 支持ie9 */
			src:url("../../font/Alifont/webfont.eot"); 
			/* 支持ie6-ie8 */
			src: url("../../font/Alifont/webfont.eot?#iefix") format("embedded-opentype"),
			url("../../font/Alifont/webfont.woff2") format("woff2"),
			/* chrome\firefox */
			url("../../font/Alifont/webfont.woff") format("woff"),
			/* chrome、firefox、opera、safari、Android 、IOS4.2+*/
			url("../../font/Alifont/webfont.ttf") format("truetype"),
			/* ios 4.1- */
			url("../../font/Alifont/webfont.svg#webfont") format("svg");
		}

		h1{
			font-size: 20px;
			/* 使用引入的字体 */
			font-family: "abc";
		}
		h2 {
			font-size: 20px;
			/* 使用引入的字体 */
			font-family: "myfont";
		}
	</style>
</head>
<body>
	<h1>春风得意马蹄疾，一夜看尽长安花</h1>
	<h2>春风得意马蹄疾，一夜看尽长安花</h2>
</body>
</html>
```

### CSS3_字体图标

>优势

```sh
1)相对图片更加清晰
2）灵活性高，更方便改变大小、颜色、风格等
3）兼容性好、IE也能支持，很多文本编辑器也能正常显示
```

>获取方式

```sh
1)利用字体设计软件进行设计
2）利用现成的字体图标，例如阿里图标库
```

>阿里图标库的本地使用

```sh
阿里图标库的使用，推荐登录
登陆后选择icon图标，然后选择中意的图标加入购物车(不要直接下载，直接下载的只是图片)
点开购物车，添加至项目(下载素材--会下载png格式的图片，下载代码--也不推荐)
如果没有项目，就点击弹框右上角添加一个，然后就会到项目页面
```

```sh
下载到本地使用
下载下来会是一个zip压缩包，解压后文件解释
*** ttf、woff、woff2 字体图标文件
*** demo_index.html 使用说明书
*** css文件，外置样式，方案二会用到
*** js文件  引入使用svg，方案三会用到

一般呈现图标使用span或者i标签

在线使用自己去官网看，实际开发用得少
```

>方案1

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>字体图标</title>
	<style>
		/* 
			我们平常理解的字体都是文字，而实际上有一些字体图标，虽然看着像图，但实际上是字
			字体图标的特点：
			1)相对图片更加清晰
			2）灵活性高，更方便改变大小、颜色、风格等
			3）兼容性好、IE也能支持，很多文本编辑器也能正常显示

			如何获得字体图标：
			1)利用字体设计软件进行设计
			2）利用现成的字体图标，例如阿里图标库
		*/
		/* 
			阿里图标库的使用，推荐登录
			登陆后选择icon图标，然后选择中意的图标加入购物车(不要直接下载，直接下载的只是图片)
			点开购物车，添加至项目(下载素材--会下载png格式的图片，下载代码--也不推荐)
			如果没有项目，就点击弹框右上角添加一个，然后就会到项目页面
		*/
		/* 
			下载到本地使用
			下载下来会是一个zip压缩包，解压后文件解释
			*** ttf、woff、woff2 字体图标文件
			*** demo_index.html 使用说明书
			*** css文件，外置样式，方案二会用到
			*** js文件  引入使用svg，方案三会用到

			一般呈现图标使用span或者i标签

			在线使用自己去官网看，实际开发用得少
		*/
		/* 1.引入 */
		@font-face {
			font-family: 'iconfont';
			src: url('../../font/myTools/iconfont.woff2?t=1696297080095') format('woff2'),
					url('../../font/myToolsiconfont.woff?t=1696297080095') format('woff'),
					url('../../font/myToolsiconfont.ttf?t=1696297080095') format('truetype');
		}
		/* 2.样式使用 */
		.iconfont {
			font-family: "iconfont" !important;
			/* 以下都是抗锯齿用的，可用可不用 */
			font-style: normal;
			-webkit-font-smoothing: antialiased;
			-moz-osx-font-smoothing: grayscale;
		}
		/* unicode模式，没有自带颜色，但是样式可调，兼容性最好 */
		.myfont {
			font-size: 100px;
		}
	</style>
</head>
<body>
	<!-- 使用图标 -->
	<span class="iconfont myfont">&#xe767;</span>
</body>
</html>
```

>方案二

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>本地使用_方案二</title>
	<!-- 1.引入字体文件的css -->
	<link rel="stylesheet" href="../../font/myTools/iconfont.css">
	<style>
		/* 由于封装的样式是用类选择器写的，所以要比他优先级高才可以生效 */
		.myfont{
			font-size: 100px;
		}

	</style>
</head>
<body>
	<!-- 2.挑选相应的图标使用，
		与unicode的区别，封装后的，可读性高，其实只是将unicode做了一个抽离
		同样样式可以自定义
	 -->
	 <span class="iconfont icon-a-HadoopHDFSMapreduce myfont"></span>
</body>
</html>
```

>方案三

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>本地使用_方案三</title>
	<!-- 1.引入js代码 -->
	<link rel="stylesheet" href="../../font/myTools/iconfont.js">
	<style>
		/* 2.定义图标风格 自己写就可以*/
		.icon {
			width: 1em;
			height: 1em;
			vertical-align: -0.15em;
			fill: currentColor;
			overflow: hidden;
		}
		/* 
			也可以选中svg标签或者加类来修改样式--一般只能改大小
			方案三用的少--因为svg兼容性差，且渲染比png还慢
		*/
	</style>
</head>
<body>
	<!-- 
		3.使用图标 
		svg和use都是h5的新标签，专门用于呈现矢量图
	-->
	<svg class="icon" aria-hidden="true">
		<!-- 改成想要的图标 -->
		<use xlink:href="#icon-python"></use>
	</svg>
</body>
</html>
```

>注意

```sh
最常用的是方案二
```

### CSS3_2D变换

#### 1.2D位移

2D位移可以改变元素的位置，具体使用方式如下:

* 先给元素添加转换属性`transform`

* 编写`transform`的具体值，相关可选值如下：

|     值     |                             含义                             |
| :--------: | :----------------------------------------------------------: |
| translateX | 设置水平方向位移，需指定长度值，若指定的是百分比，是参考自身宽度的百分比 |
| translateY | 设置水平方向位移，需指定长度值，若指定的是百分比，是参考自身宽度的百分比 |
| translate  |         一个值代表水平方向，两个值代表水平和垂直方向         |

* 注意点

  ```sh
  1.位移和相对定位很相似，都不脱离文档流，不会影响到其他元素。
  2.与相对定位的区别：相对定位的百分比值，参考的是其父元素，定位的百分比值，参考的是自身
  3.浏览器针对位移有优化，与定位相比，浏览器处理位移的效率更高
  4.transform可以链式编写:
  "transform:translateX(50px) translateY(50px);"
  5.位移对行内元素无效，解决方案用display把它变行内块或块
  6.位移配合定位，可以实现元素水平垂直居中
  ```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>01_位移</title>
	<style>
		.outer {
			width: 200px;
			height: 200px;
			border: 2px solid black;
			margin: 0 auto;
			margin-top: 100px;
			position: relative;
		}
		.inner{
			width: 200px;
			height: 200px;
			background-color: skyblue;
			/* 
				css3变换的核心属性 transform
				参考点：最近祖先元素的左上角 百分比是指自身的，x为宽，y为高
				translateX(数值或百分比)  x轴上的移动，由于css不区分大小写，所以x小写也对
				translateY(数值或百分比)  y轴上的移动
				translate(x轴,y轴)   


				不脱离文档流，和相对定位非常像

			*/
			transform: translate(50px,50px);
		}
		/* 实现水平垂直居中 */
		.inner2{
			width: 100px;
			height: 100px;
			background-color: orange;
			position: absolute;
			top: 50%;
			left: 50%;
			transform: translate(-50%,-50%);
		}

	</style>
</head>
<body>
	<div class="outer">
		<div class="inner">你好啊</div>
	</div>
	<div class="outer">
		<div class="inner2"></div>
	</div>
</body>
</html>
```

#### 2.2D缩放

2D缩放是指：让元素放大或者缩小，具体使用方式如下：

* 先给元素添加转换属性`transform`
* 编写`transform`的具体值，相关可选值如下：

|    值    |                             含义                             |
| :------: | :----------------------------------------------------------: |
| `scaleX` | 设置水平方向的缩放比例，值为一个数字，1表示不缩放，大于1放大，小于1缩小 |
| `scaleY` | 设置垂直方向的缩放比例，值为一个数字，1表示不缩放，大于1放大，小于1缩小 |
| `scale`  | 同时设置水平方向、垂直方向的缩放比例，一个值代表同时设置水平和垂直缩放；两个值分别代表水平缩放、垂直缩放。 |

>注意

```sh
1.`scale`的值可以为负数，实现镜像翻转。
2.借助缩放，可实现小于12px的文字。
3.transform可以链式编写:
"transform:sacleX(50px) scaleY(50px);"
4.缩放对行内元素无效，解决方案用display把它变行内块或块
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>缩放</title>
	<style>
		.outer {
			width: 200px;
			height: 200px;
			border: 2px solid black;
			margin: 0 auto;
			margin-top: 100px;
		}
		.inner{
			width: 200px;
			height: 200px;
			background-color: skyblue;

			/* 
				css3变换的核心属性 transform 
				scaleX() x轴上的缩放，里面的数值代表比例，针对的是点到中线的距离
				scaleY() Y轴上的缩放，里面的数值代表比例，针对的是点到中线的距离
				scale(x轴,y轴);
				内容也会跟着缩放，负值相当于翻转,

				理解，对于x轴，从中间画一条线，所谓缩放，指的就是左右的点到中间线的距离的变化

				应用：浏览器有最小大小，例如12px，想要更小，可以用缩放实现
			*/
			transform: scale(0.5,0.5);
		}
	</style>
</head>
<body>
	<div class="outer">
		<div class="inner">你好啊</div>
	</div>
</body>
</html>
```

#### 3.2D旋转

2D旋转是指：让元素在二维平面内，顺时针旋转或者逆时针旋转，具体使用方法如下：

* 先给元素添加转换属性`transform`

* 编写`transform`的具体值，相关可选值如下：

|    值     |                             含义                             |
| :-------: | :----------------------------------------------------------: |
| `rotateZ` | 设置旋转角度，需要一个角度值deg，正值顺时针，负值逆时针，绕Z轴 |
| `rotate`  | 设置旋转角度，需要一个角度值deg，正值顺时针，负值逆时针，只有一个值时是2D旋转，相当于rotateZ |

>注意

```sh
1.旋转对行内元素无效，解决方案用display把它变行内块或块
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>旋转</title>
	<style>
		.outer {
			width: 200px;
			height: 200px;
			border: 2px solid black;
			margin: 0 auto;
			margin-top: 100px;
		}
		.inner{
			width: 200px;
			height: 200px;
			background-color: skyblue;
			/* 
				css3变换的核心属性 transform 
				rotateX、rotateY、rotate3D属于3D的旋转
				rotateZ属于2D的旋转，
				理解，2D处于平面上，所谓旋转，实际上绕着Z轴旋转

				默认旋转的中心是元素正中央
				rotateZ(角度值)  角度值单位deg，正值顺时针转，负值逆时针转
				rotate(角度值)  写一个值时，相当于rotateZ，因为默认2D旋转

				可以用坐标轴辅助查看旋转的角度
			*/
			transform: rotate(30deg);
		}
	</style>
</head>
<body>
	<div class="outer">
		<div class="inner">你好啊</div>
	</div>
</body>
</html>
```

#### 4.2D扭曲

2D扭曲是指:让元素在二维平面内被'拉扯'，进而‘走形’，实际开发几乎不用，了解即可，具体使用方式如下：

* 先给元素添加转换属性`transform`

* 编写`transform`的具体值，相关可选值如下：

  |  值   |                             含义                             |
  | :---: | :----------------------------------------------------------: |
  | skewX | 设置元素在水平方向扭曲，值为角度值，会将元素的左上角、右下角拉扯 |
  | skewY | 设置元素在垂直方向扭曲，值为角度值，会将元素的左上角、右下角拉扯 |
  | skew  |         一个值代表skewX，两个值分别代表skewX、skewY          |

* 注意点:

  ```sh
  1.扭曲对行内元素无效，解决方案用display把它变行内块或块
  2.扭曲文字解释很抽象，推荐直接用代码写一个，然后用开发者工具调角度
  ```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>扭曲</title>
	<style>
		.outer {
			width: 200px;
			height: 200px;
			border: 2px solid black;
			margin: 0 auto;
			margin-top: 100px;
		}
		.inner{
			width: 200px;
			height: 200px;
			background-color: skyblue;

			/* 
				css3变换的核心属性 transform 
				skewX(角度值) 在X方向上扭曲，可以制造平行四边形
				skewY(角度值) 在Y方向上扭曲，可以制造平行四边形
				skew(x角度,y角度) 只写一个值代表X方向
				正负值方向相反
			*/
			transform: skewX(50deg);
		}
	</style>
</head>
<body>
	<div class="outer">
		<div class="inner">你好啊</div>
	</div>
</body>
</html>
```

#### 5.多重变换

多个变换，可以同时使用一个`transform`来编写。

```css
transform: translate(100px,100px) scale(0.5);
```

>注意

```sh
多重变换时，建议最后旋转
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>多重变换</title>
	<style>
		.outer {
			width: 200px;
			height: 200px;
			border: 2px solid black;
			margin: 0 auto;
			margin-top: 100px;
		}
		.inner{
			width: 200px;
			height: 200px;
			background-color: skyblue;

			/* 
				css3变换的核心属性 transform 
				所谓多重变换，实际上就是位移、缩放、旋转、扭曲至少发生两个

				采用transform的链式语法
			*/
			/* ********************************/
			/* 先位移再缩放 */
			/* transform: scale(0.5) translate(100px,100px); */
			/* 变换顺序不一样，最终结果也不一样 */
			transform: translate(100px,100px) scale(0.5);

			/* 
				变换效果不一样的本质是坐标系发生了变化
				缩放，坐标系不变
				位移，坐标系不变
				旋转，坐标系发生了变化，坐标系跟着转了

				所以旋转具有破坏性，所以多重变换需要把旋转放到最后，否则会有各种诡异的bug

			*/
		}
	</style>
</head>
<body>
	<div class="outer">
		<div class="inner">你好啊</div>
	</div>
</body>
</html>
```

#### 6.变换原点

1.元素变换时，默认的原点是元素的中心，使用`transform-origin`可以设置变换的原点。

2.修改变换原点对位移没有影响，对旋转和缩放会产生影响。

3.如果提供两个值，第一个用于横坐标，第二个用于纵坐标。

4.如果只提供一个，若是像素值，表示横坐标，纵坐标取50%，若是关键词，则另一个坐标取50%

```sh
1.transform-origin: 50% 50%;
变换原点在元素的中心位置，百分比是相对于自身的--默认值

2.transform-origin: right bottom;
变换原点在元素的右下角

3.transform-origin: 50px 50px;
变换原点距离左上角50px 50px 的位置

4.transform-origin:0;
只写一个值的时候，第二个值默认为50%;
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>多重变换</title>
	<style>
		.outer {
			width: 200px;
			height: 200px;
			border: 2px solid black;
			margin: 0 auto;
			margin-top: 100px;
		}
		.inner{
			width: 200px;
			height: 200px;
			background-color: skyblue;
			/* 
				变换原点：变换的时候围绕的点就是变换原点
				属性：transform-origin

				1)关键字控制
				transform-origin: right bottom;

				2)像素值(坐标)
				transform-origin:50px 50px;

				3)百分比(和自身宽高计算后得出像素，最后转成坐标)
				transform-origin:5% 5%;

				4)两个值，第一个值是X，第二个值是Y，
				如果只写一个值，
				关键字中left、right等表示X，y则默认在中间
				关键字中top、bottom等表示y，x则默认在中间
				像素值和百分比则为x，y默认在中间
				transform-origin: left;
			*/

			/* ****************变换原点对 旋转 有影响*******************************/
			/* 变换原点的位置对旋转有影响 */
			/* 
				transform-origin: right bottom;
				transform: rotate(30deg);
			*/

			/* ****************变换原点对 缩放 有影响*******************************/
			/* 
				transform-origin: right bottom;
				transform: scale(0.5);
			*/

			/* ****************变换原点对 位移 无影响*******************************/
			/* 
				transform-origin: right bottom;
				transform: translate(50px);
			*/

			/* 坐标原点 ≠ 变换原点 */


		}
	</style>
</head>
<body>
	<div class="outer">
		<div class="inner">你好啊</div>
	</div>
</body>
</html>
```

### CSS3_过渡

过渡可以在不使用`flash`动画，不使用JS的情况下，让元素从一种样式，平滑过渡为另一种样式

#### 1.基本使用

过渡使用的关键字为`transition`,其本身是一个复合属性，有两个重要的子属性

##### 1.1 transition-property

>名称

过渡属性

>作用

定义哪个属性需要过渡，只有在该属性中定义的属性（比如宽、高、颜色等），才会有过滤效果。

>常用值

```sh
"none"
不过渡任何属性

"all"
过渡所有能过渡的属性

"具体的属性名"
例如：width、height，若有多个以逗号隔开
```

```sh
不是所有的属性都能过渡，值为数字、百分比，或者值能转化为数字、百分比的属性，都支持过渡，否则不支持。

```

##### 1.2 transition-duration

>名称

过渡持续时间

>作用

设置过渡的持续时间，即：一个状态过渡到另外一个状态耗时多久

>举例

```css
/* 设置一个时间，所有属性共用，过渡到完成形态耗时 */
transition-duration: 5s;
```

>常用值

```sh
"0"
没有任何过渡时间，默认值

"s或ms"
秒或毫秒

"列表"
1.如果想让所有的属性都持续一个时间，那就写一个值
2.如果想让每个属性持续不同的时间，那就写一个时间列表
`2.1`多对一
    transition-property:A,B;
    transition-duration:1s;
    那么A与B都是1s变化
`2.2`多对多
    transition-property:A,B;
    transition-duration:1s,2s;
    A完成过渡的时间是1s，B完成过渡的时间是2s
```

##### 1.3 举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>01_基本使用</title>
	<style>
		.box1{
			width: 200px;
			height: 200px;
			background-color: orange;

			/* 
				谁想发生过渡，谁就加上属性 transition
				注:不在事件里加的原因：时间一结束就消失了，过渡效果失效
				该属性是个复合属性，所以我们先探索他的子属性


				1)指明发生变化的属性 例如height width等等,也可以用引号引起来，多个属性之间用逗号分隔
				至于是什么属性，根据我们需要给哪种变化加过渡决定
				transition-property

				2)设置过渡的持续时间 持续时间,单位一般用s或者ms
				transition-duration

				3) 对应关系，
					3.1)多对一
					transition-property:A,B;
					transition-duration:1s;
					那么A与B都是1s变化
					3.2）多对多
					transition-property:A,B;
					transition-duration:1s,2s;
					A完成过渡的时间是1s，B完成过渡的时间是2s

				4）能过渡的属性
				属性值能用或者转换成数字或百分比表示才能过渡，即属性的值要能计算才能实现过渡
				例如 background-color color 即使我们写纯色，但他底层可以转16进制或rgb所以可以过渡
				
				由于属性繁多，所以一般
				transition-property:all;
				意为：让所有能过渡的属性都过渡

			*/
			transition-property:height;
			transition-duration: 2s;
		}
		/* 
			过渡生效的前提：有属性发生了变化
		*/
		.box1:hover{
			height: 400px;
		}
	</style>
</head>
<body>
	<div class="box1"></div>
</body>
</html>
```

#### 2.高级使用

高级使用也是两个属性

##### 2.1   transition-delay

>作用

指定开始过渡的延迟时间，单位:s或ms

>举例

```css
/* 过渡的延迟 即事件触发多长时间后才进行过渡 */
transition-delay: 2s;
```

##### 2.2 transition-timing-function

>作用

```sh
设置过渡的类型
```

>常用值

```sh
ease 
平滑过渡，默认值

linear 
线性过渡，匀速

ease-in
慢--> 快

ease-out
快-->慢

ease-in-out
慢-->快-->慢

step-start
等同于steps(1,start),过渡起初直接瞬移到完成体

step-end
等同于steps(1,end),过渡时间结束后瞬移到完全体

steps(int,?)
接受两个参数的步进函数。第一个参数必须为正数，指定函数的步数。第二个参数取值可以是start或end，指定每一步的值发生变化的时间点，第二个参数默认值为end

cubic-bezie(number,number,number,number)  特定的贝塞尔曲线的类型

在线制作贝塞尔曲线：https://cubic-bezier.com
```

##### 2.3举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>02_高级使用</title>
	<style>
		.outer {
			width: 1300px;
			height: 900px;
			border: 1px solid black;
		}
		.outer:hover .box{
			width: 1300px;
		}
		.box{
			width: 200px;
			height: 100px;
			background-color: orange;
			opacity: 0.5;
			/* 让所有能过渡的属性都能过渡 */
			transition-property:all;
			/* 设置一个时间，所有属性共用，过渡到完成形态耗时 */
			transition-duration: 5s;
			/* 过渡的延迟 即事件触发多长时间后才进行过渡 */
			transition-delay: 2s;
			/* 
				默认的过渡效果：
				平滑过渡：起初很慢，中间变快，收尾又变慢

				要修改过渡的效果，或者说类型，需要用到属性 transition-timing-function
			*/
		}
			/* 
				transition-timing-function
				属性值：
				ease 平滑过渡，默认值
				linear 匀速
				ease-in 先慢后快
				ease-out 先快后慢
				ease-in-out 先慢再快再慢，但慢的比ease更慢
				step-start 闪现到过渡结束,可以理解为过渡时间开始前执行
				step-end  维持初始形态不变，过渡时间一到立刻为过渡完全形态，可以理解为过渡时间结束后执行
				steps(①，②)  ①是一个数字，分成n小份，每次突一点  ②选值start和end，start第一次冲刺一下，end第一次后冲刺一下

				贝塞尔曲线，通过坐标系去描述物体运动的曲线

			*/
		.box1 {
			background-color: skyblue;
		
			transition-timing-function:ease;
		}
		.box2{
			background-color: orange;
			transition-timing-function:linear;
		}
		.box3{
			background-color: gray;
			transition-timing-function: ease-in;
		}
		.box4{
			background-color: tomato;
			transition-timing-function: ease-out;
		}
		.box5{
			background-color: green;
			transition-timing-function: ease-in-out;
		}
		.box6{
			background-color: purple;
			transition-timing-function: step-start;
		}
		.box7{
			background-color: skyblue;
			transition-timing-function: step-end;
		}
		.box8{
			background-color: chocolate;
			
			transition-timing-function:steps(20) ;
		}
		.box9{
			background-color: black;
			/* 
				贝塞尔曲线，通过坐标系去描述物体运动的曲线
				参考地址：https://cubic-bezier.com

				横轴时间，纵轴距离，得到一个运动曲线
				横轴的时间代表过渡的每个时间点
				纵轴距离代表对应时间点，距离最终形态的距离

				使用：去这个网站调一个贝塞尔曲线值，粘贴过来即可，当然大佬也可以自己写
			*/
			transition-timing-function: cubic-bezier(.88,1.03,.78,1.24);
			/* 
				前两个值代表一组坐标，后两个值也是一组坐标
			*/
		}
	</style>
</head>
<body>
	<div class="outer">
		<div class="box box1">ease(慢->快->慢)</div>
		<div class="box box2">linear(匀速)</div>
		<div class="box box3">ease-in(先慢后快)</div>
		<div class="box box4">ease-out(快->慢)</div>
		<div class="box box5">ease-in-out(慢->快->慢)</div>
		<div class="box box6">step-start(不考虑过渡时间，直接闪现到完全形态)</div>
		<div class="box box7">step-end(考虑过渡时间，但无过渡效果，过渡时间到了以后，瞬间到达终点)</div>
		<div class="box box8">steps分步过渡</div>
		<div class="box box9">无敌的贝塞尔曲线</div>
	</div>
</body>
</html>
```

#### 3.复合属性

如果设置了一个时间，表示`duration`;如果设置了两个时间，第一个是`duration`,第二个是`delay`;其他值没有顺序要求

```css
transition: 3s all 1s linear ;
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>复合属性</title>
	<style>
		.outer {
			width: 1000px;
			height: 100px;
			border:1px solid black;
		}
		.outer:hover .inner{
			width: 1000px;
		}
		.inner {
			width: 100px;
			height: 100px;
			background-color: orange;
			/* 
				过渡的复合属性
				常规顺序： 过渡时间 过渡属性 过渡延迟 过渡效果

				第一个出现的时间一定是过渡时间，第二个是延迟时间，其他属性随意写

				即我们只要写了时间，第一个就会被当做过渡时间，第二个如果有才是延迟时间，不需要我们指明
			*/
			transition: 3s all 1s linear ;
		}
	</style>
</head>
<body>
	<div class="outer">
		<div class="inner"></div>
	</div>
</body>
</html>
```

#### 4.过渡小案例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>图片蒙层提示效果</title>
	<style>
		/* 
			思路：两个框，A框是图片，B框是透明度为0的蒙层，
			鼠标移入图片，B框定位到A上面，透明度变0.5

			还有图片旋转缩放，文字浮现，鼠标变小手
		*/
		/* 最外层容器和遮罩层应该与图片一样大 */
		.outer{
			width: 350px;
			height: 525px;
			position: relative;

			/* 防止图片缩放超过父容器 */
			overflow: hidden;
		}
		.mask {
			width: 350px;
			height: 525px;
			background-color: black;
			cursor: pointer;
			/* 文字样式 */
			color: white;
			text-align: center;
			line-height: 525px;
			font-size: 80px;

			/* 
				定位
			*/
			position: absolute;
			top: 0;
			left: 0;

			/* 遮罩透明 */
			opacity: 0;

			/* 过渡 */
			transition: 1s all;
		}
		img {
			transition: 1s all;
		}
		.outer:hover .mask{
			/* 鼠标移上去，显示遮罩 */
			opacity: 0.5;
		}
		.outer:hover img{
			transform: scale(1.1,1.1) rotate(30deg);
		}
	</style>
</head>
<body>
	<div class="outer">
		<img src="../../img/R-C.jpeg" alt="">
		<div class="mask">老司机</div>
	</div>
</body>
</html>
```

### Css3_动画

#### 0 动画基础

>什么是帧

一段动画，就是一段时间连续播放n个画面。每一张画面，我们管他们叫做“帧”。一定时间内连续快速播放若干个帧，就成了人眼中锁看到的动画。同样时间内，播放的帧数越多，画面看起来越流畅。人眼1秒看24帧就会觉得画面不卡顿，1080P就是1秒60帧

>什么是关键帧

关键帧指的是，在构成一段动画的若干帧中，起到决定性作用的2~3帧。

#### 1基本使用

>第一步定义关键帧(定义动画)

1.简单定义方式

```css
/* 
    定义一个动画(一组关键帧)
    浏览器会根据 animation-name 来寻找关键帧

    from...to简易模式
*/
@keyframes 动画名 {
    /* 第一帧 */
    from {
        /* 没有要写的就空着 */
    }
    /* 
        最后一帧
    */
    to {
        /* 帧里面可以写很多操作 */
        transform: translate(900px);
        /* 
            如果发现颜色转换生硬，需要把浏览器开硬件加速模式
            或者给动画加延迟
        */
        background-color: red;
    }
}
```

2.完整定义方式

```css
/* 
    和from...to的简易模式相比，这种更精细
    定义一个动画(一组关键帧)
    浏览器会根据 animation-name 来寻找关键帧
*/
@keyframes 动画名 {
    /* 第一帧 */
    0% {

    }
    /* 中间帧 */
    30%{
        background-color: orange;
    }
    /* 最后一帧 */
    100% {
        transform: translate(900px) rotate(360deg);
        background-color: chocolate;
        border-radius: 50%;
    }
}
```

```sh
百分比和from...to是可以混用的，form就是0%，to就是100%
建议不混用
```

>第二步：给元素应用动画

```sh
"animation-name"
给元素指定具体的动画(具体的关键帧)

"animation-duration"
设置动画所需时间

"animation-delay"
设置动画延迟
```

```css
.inner {
    width: 100px;
    height: 100px;
    background-color: deepskyblue;
    /* 应用动画到元素 */
    animation-name:动画名;
    /* 动画持续时间 */
    animation-duration: 3s;
    /* 动画延迟时间 */
    animation-delay: 0.5s;
}
```

##### 3.1.1举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>基本使用--基础动画1</title>
	<style>
		/* 
			用CSS3做动画，只需要写好关键帧，CSS3就会为我们补帧，也叫插帧技数
			实际上动画也是一样的，先写关键帧，再插帧补帧
		*/

		.outer {
			width: 1000px;
			height: 100px;
			border:1px solid black;
		}
		.inner {
			width: 100px;
			height: 100px;
			background-color: deepskyblue;

			/* 
				想要让谁做动画就给他加 animation 属性，
				和过渡一样，这也是个复合属性，所以拆分子属性
			
				animation-name 给动画取名字,给元素绑定动画
				animation-duration 动画持续时间

				给一个元素绑定动画和指定了持续时间，一个基本动画才能实现
			*/
			/* 应用动画到元素 */
			animation-name:wangyoudong;
			/* 动画持续时间 */
			animation-duration: 5s;
		}

		/* 
			定义一个动画(一组关键帧)
			浏览器会根据 animation-name 来寻找关键帧

			from...to简易模式
		*/
		@keyframes wangyoudong {
			/* 第一帧 */
			from {
				/* 没有要写的就空着 */
			}
			/* 
				最后一帧
			*/
			to {
				/* 帧里面可以写很多操作 */
				transform: translate(900px);
				/* 
					如果发现颜色转换生硬，需要把浏览器开硬件加速模式
					或者给动画加延迟
				*/
				background-color: red;
			}
		}
	</style>
</head>
<body>
	<div class="outer">
		<div class="inner"></div>
	</div>
</body>
</html>
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>基本动画2</title>
	<style>
		/* 
			用CSS3做动画，只需要写好关键帧，CSS3就会为我们补帧，也叫插帧技数
			实际上动画也是一样的，先写关键帧，再插帧补帧
		*/

		.outer {
			width: 1000px;
			height: 100px;
			border:1px solid black;
		}
		.inner {
			width: 100px;
			height: 100px;
			background-color: deepskyblue;

			/* 
				想要让谁做动画就给他加 animation 属性，
				和过渡一样，这也是个复合属性，所以拆分子属性
			
				animation-name 给动画取名字,给元素绑定动画
				animation-duration 动画持续时间
				animation-delay    动画延迟时间
			
			*/
			/* 应用动画到元素 */
			animation-name:wangyoudong;
			/* 动画持续时间 */
			animation-duration: 3s;
			/* 动画延迟时间 */
			animation-delay: 0.5s;
		}

		/* 
			和from...to的简易模式相比，这种更精细
			定义一个动画(一组关键帧)
			浏览器会根据 animation-name 来寻找关键帧
		*/
		@keyframes wangyoudong {
			/* 第一帧 */
			0% {

			}
			/* 中间帧 */
			30%{
				background-color: orange;
			}
			/* 最后一帧 */
			100% {
				transform: translate(900px) rotate(360deg);
				background-color: chocolate;
				border-radius: 50%;
			}
		}
	</style>
</head>
<body>
	<div class="outer">
		<div class="inner"></div>
	</div>
</body>
</html>
```

#### 2进阶属性

##### 2.1 animation-timing-function

>作用

设置动画的类型

>常用值

```sh
ease 
平滑过渡，默认值

linear 
线性过渡，匀速

ease-in
慢--> 快

ease-out
快-->慢

ease-in-out
慢-->快-->慢

step-start
等同于steps(1,start),过渡起初直接瞬移到完成体

step-end
等同于steps(1,end),过渡时间结束后瞬移到完全体

steps(int,?)
接受两个参数的步进函数。第一个参数必须为正数，指定函数的步数。第二个参数取值可以是start或end，指定每一步的值发生变化的时间点，第二个参数默认值为end

cubic-bezie(number,number,number,number)  特定的贝塞尔曲线的类型

在线制作贝塞尔曲线：https://cubic-bezier.com
```

##### 2.2 animation-iteration-count

>作用

指定动画的播放次数

>常用值

```sh
"整数"
动画循环的次数

"infinite"
无限循环
```

##### 2.3 animation-direction

>作用

指定动画方向

>常用值

```sh
"nomal"
正常方向，从0%~100%

"reverse"
反方向运行，从100%~0%

"alternate"
动画先0%~100%，再100%~0%，交替

"alternate-reverse"
动画先100%~0%，再0%~100%，交替
```

##### 2.4 animation-fill-mode

>作用

设置动画之外的状态

>常用值

```sh
"forwards"
设置对象状态为动画结束时的状态

"backwards"
设置对象状态为动画开始时的状态
```

##### 2.5 animation-play-state

>作用

设置动画的播放状态

>常用值

```sh
"running"
运动

"paused"
暂停
```

##### 2.6 举例

>提示

一卡一卡的，是因为我们设置了`steps(20)`

>案例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>其他属性</title>
	<style>
		.outer {
			width: 1000px;
			height: 100px;
			border:1px solid black;
		}
		.inner {
			width: 100px;
			height: 100px;
			background-color: deepskyblue;

			/* 
				想要让谁做动画就给他加 animation 属性，
				和过渡一样，这也是个复合属性，所以拆分子属性
			
				animation-name 给动画取名字,给元素绑定动画
				animation-duration 动画持续时间
				animation-delay    动画延迟时间
			
				animation-timing-function 动画效果

				animation-iteration-count 动画播放的次数
				animation-direction 动画的方向
				animation-fill-mode 动画结束后的状态
				animation-play-state 动画播放的状态
			*/
			/* 应用动画到元素 */
			animation-name:wangyoudong;
			/* 动画持续时间 */
			animation-duration: 3s;
			/* 动画延迟时间 */
			animation-delay: 0.5s;

			/* **************动画效果********************* */
			/* 
				和过渡效果的特性一样，属性值
				ease 
				平滑效果--默认值

				linear 
				线性过渡，匀速

				ease-in
				慢--> 快

				ease-out
				快-->慢

				ease-in-out
				慢-->快-->慢

				step-start
				等同于steps(1,start),过渡起初直接瞬移到完成体

				step-end
				等同于steps(1,end),过渡时间结束后瞬移到完全体

				steps(int,?)
				接受两个参数的步进函数。第一个参数必须为正数，指定函数的步数。第二个参数取值可以是start或end，指定每一步的值发生变化的时间点，第二个参数默认值为end

				cubic-bezie(number,number,number,number)  特定的贝塞尔曲线的类型

				在线制作贝塞尔曲线：https://cubic-bezier.com 
			*/
			/* 设置动画的方式 */
			animation-timing-function: steps(20);
			/* ********************************************** */

			/* 
				动画播放的次数 
				值:
				整数，代表播放次数
				infinite 无限
			*/
			animation-iteration-count:3;

			/* 
				动画的方向
				值：
				normal 从0%~100%，默认
				reverse 从100%~0%

				往复运动是根据次数来的，每次跑完算一次，
				所以当次数为1时，往复失效
				alternate 往复运动，从0%~100%~0%...
				alternate-reverse 交替的往复运动,从100%~0%~100%...
			*/
			animation-direction: reverse;

			/* 
				动画以外的状态(不发生动画的时候停在哪里)
				值：
				forwards 静止在最后一帧，动画结束停在最后一帧
				backwards 静止在第一帧，动画结束回到第一帧，默认
			*/
			animation-fill-mode:backwards;

			/* 
				动画的播放状态
				值：
				paused 暂停
				running 播放
			*/
			/* animation-play-state: paused; */
		}

		@keyframes wangyoudong {
			/* 第一帧 */
			from {

			}
			/* 最后一帧 */
			to {
				transform: translate(900px) rotate(360deg);
				background-color: chocolate;
				border-radius: 50%;
			}
		}
		/* 鼠标移入，动画暂停 */
		.outer:hover .inner{
			animation-play-state: paused;
		}
	</style>
</head>
<body>
	<div class="outer">
		<div class="inner"></div>
	</div>
</body>
</html>
```

#### 3 复合属性

如果设置了一个时间，表示`duration`;如果设置了两个时间，第一个是`duration`,第二个是`delay`;其他值没有顺序要求

>备注

```sh
animation-play-state 一般单独使用，不进入复合属性
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>复合属性</title>
	<style>
		.outer {
			width: 1000px;
			height: 100px;
			border:1px solid black;
		}

		@keyframes wangyoudong {
			/* 第一帧 */
			from {
				/* 没有要写的就空着 */
			}
			/* 
				最后一帧
			*/
			to {
				transform: translate(900px) rotate(360deg);
				background-color: chocolate;
				border-radius: 50%;
			}
		}

		.inner {
			width: 100px;
			height: 100px;
			background-color: deepskyblue;

			/* 
				animation 复合属性
				animation: name duration timing-function delay iteration-count direction fill-mode;
				和过渡类似，没有顺序，时间写一个代表持续时间，写两个，第一个是持续时间，第二个是延迟
				
				动画的播放状态不用复合属性，一般结合事件使用
			*/
			animation: wangyoudong 1s linear 0.5s 2 reverse forwards;
		}


	</style>
</head>
<body>
	<div class="outer">
		<div class="inner"></div>
	</div>
</body>
</html>
```

#### 4 动画和过渡的区别

```sh
主要区别：
① 动画不需要触发条件，过渡需要
② 动画从开始到结束，可以通过关键帧去精细的设置，过渡只关注始末，过程中无法控制
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>动画与过渡的区别</title>
	<style>
		.outer {
			width: 1000px;
			height: 200px;
			border: 1px solid black;
		}
		.inner {
			width: 100px;
			height: 100px;
		}
		/* 用过渡，实现inner1跑到右边 */
		.inner1{
			background-color: orange;
			transition: 3s linear;
		}
		.outer:hover .inner1{
			transform: translate(900px);
		}


		/* 用动画，实现inner2跑到右边 */
		.inner2{
			background-color: green;
			animation: inner2 3s linear forwards;
		}
		@keyframes inner2 {
			0%{}
			100%{
				transform: translate(900px);
			}
		}

		/* 
			主要区别：
			① 动画不需要触发条件，过渡需要
			② 动画从开始到结束，可以通过关键帧去精细的设置，过渡只关注始末，过程中无法控制
		*/
	</style>
</head>
<body>
	<div class="outer">
		<div class="inner inner1">
			研究过渡
		</div>
		<div class="inner inner2">
			研究动画
		</div>
	</div>
</body>
</html>
```

### CSS3_多列布局

#### 1.多列布局属性

一般用于实现报纸类的布局，常用属性如下:

```sh
"column-count"
指定列数，值是数字

"column-width"
指定列宽，值是长度

"columns"
同时指定列宽和列数，复合属性；值没有数量和顺序要求

"column-gap"
设置列边距

"column-rule-style"
设置列与列之间边框的风格，和边框一样

"column-rule-width"
设置列与列之间边框的宽度

"column-rule-color"
设置列与列之间边框的颜色

"column-rule"
设置列边框，复合属性

"column-span"
指定是否跨列；值：none、all
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>01_多列布局</title>
	<style>
		.outer{
			width: 1000px;
			margin: 0 auto;

			/* 直接指定列数，分成几列 */
			/* column-count: 3; */

			/* 指定每一列的宽度，会自动计算列数
			由于列与列之间间隙的存在，所以这里不是4列哦 */
			/* column-width: 250px; */

			/* 
			复合属性，能同时指定列宽和列数
				指定了3列
				用220px算出来是4列
				
				取小的那个，最终3列
			*/
			columns:3 220px;

			/* 
				调整列间距
				即使写0px，也还是有缝隙的，会自动计算一个极小值
			*/
			column-gap: 20px;

			/* 列边框 */
			column-rule-width: 2px;
			column-rule-style: dashed;
			column-rule-color: brown;
			/* 复合属性 */
			/* column-rule: 2px dashed brown; */
		}

		h1 {
			/* 
				column-span 是否跨列，只有两个值
				none 不跨列
				all 跨所有列
			*/
			column-span: all;
			text-align: center;
		}
		/* 插入图片，写在列与列之间，设置宽度100%即可 */
		img {
			width: 100%;
		}
	</style>
</head>
<body>
	<div class="outer">
		<h1>《自由来临》</h1>
		<p>【开始】Lorem ipsum dolor sit amet, consectetur adipisicing elit. Dignissimos maiores blanditiis enim expedita nobis dicta veniam voluptas, temporibus voluptates odio eum autem ipsam! Rerum nesciunt animi, est enim minus et laborum saepe cumque nisi ea temporibus voluptatem iste modi optio? Incidunt excepturi et beatae earum nam, qui enim vero aliquam, possimus assumenda doloribus dolore illum. Nemo rerum modi nesciunt officiis?【结束】</p>
		<p>【开始】Lorem ipsum dolor sit, amet consectetur adipisicing elit. Odio recusandae quasi deserunt velit eum soluta, ad fuga autem. Magnam sunt accusamus eveniet vero quisquam ullam? Corrupti accusamus minus libero iste inventore amet laudantium mollitia, dolor, sapiente repellendus veniam eveniet possimus iure omnis, quam dicta recusandae eum nostrum impedit. Nesciunt asperiores alias hic dolores, eveniet omnis nihil vitae, excepturi corrupti velit tempora quae facere unde accusantium veritatis illum saepe tenetur modi est. Nisi dolor vitae tenetur? Facere laboriosam vitae iure architecto. Incidunt repudiandae odio quam odit esse saepe in explicabo quis, eveniet ipsum. Tenetur, autem unde dolorem ipsa reprehenderit eveniet sapiente ipsum nisi vel deserunt quae cupiditate obcaecati pariatur, modi cum est at facere vitae aut id molestias. Molestias accusamus aperiam vitae perspiciatis labore consequuntur corrupti? Commodi quos aliquam, nobis dignissimos accusantium fugit quasi accusamus maxime, veritatis similique ea corporis quibusdam? Rem magni, tempora impedit odit modi officiis, aliquam velit quisquam mollitia nam illum qui totam, doloremque sapiente voluptas veritatis esse. Deserunt beatae animi, atque laborum, aliquam hic cumque veritatis quidem voluptas placeat, aut error. Quos, quis inventore! Sint reiciendis eveniet voluptatem aperiam suscipit, mollitia tempora voluptatum nesciunt sed repellendus, dolore aliquid, saepe adipisci doloribus delectus fugit. Perferendis quos necessitatibus iusto?【结束】</p>
		
		<p>【开始】Lorem ipsum dolor sit amet consectetur adipisicing elit. Natus, placeat, porro nostrum fugit cupiditate excepturi impedit ab rerum facilis, possimus voluptatibus. Nemo debitis repellendus, velit sapiente, quo quis modi enim placeat minima, cum numquam repudiandae laborum esse rerum facilis dolore. Veritatis, reiciendis nisi totam pariatur perferendis numquam iure quae itaque accusantium accusamus, dicta et inventore ad nihil ratione consectetur id corporis? Sequi aliquam accusantium adipisci praesentium voluptatem, vitae eum nulla molestiae maxime reprehenderit, ullam quaerat pariatur ad consequuntur labore impedit mollitia. Dolore ab tenetur quam hic minus vel dignissimos enim! Porro officia eligendi voluptates nemo eum sit distinctio, ipsam laudantium pariatur error quod at nobis deleniti minima quasi, vel cum soluta. Perferendis reiciendis reprehenderit quaerat sunt iure nesciunt quasi iusto quod a nihil aspernatur ea vel, at culpa nostrum! Velit perspiciatis corrupti doloribus dolore obcaecati assumenda suscipit natus exercitationem hic veniam, ullam ab molestiae doloremque optio dignissimos rerum similique quidem esse! Aperiam neque harum corporis quo recusandae qui a ad consequuntur beatae animi, non in libero commodi iusto quia tenetur blanditiis maxime sapiente, sequi provident quas quis unde est eius. Hic suscipit doloribus voluptas commodi totam fugit porro, est consequuntur.【结束】</p>
		<img src="../../img/R-C.jpeg" alt="">
		<p>【开始】Lorem ipsum dolor sit amet consectetur adipisicing elit. Quos minima, commodi eveniet cum totam et quas asperiores corrupti magni modi recusandae exercitationem deleniti sint aperiam ipsum expedita? Alias vel quos rem labore, iure quod ab necessitatibus voluptates fugit accusamus enim ipsam delectus maxime dolore consequuntur corporis ex sapiente molestiae. Iste corrupti rerum numquam et! Aut iste voluptatum perferendis, inventore quaerat vero voluptas, incidunt sed harum quasi dolorem recusandae qui unde saepe itaque vitae. Earum impedit explicabo dolorem, quidem dignissimos numquam autem sint. Tempore eos numquam iusto quisquam fugit eum a at optio id, nostrum illo recusandae ab alias vero saepe dolorum provident, nobis nihil! Temporibus voluptatum illum saepe sit, facere consectetur, eos dolores laboriosam deleniti laudantium sint corrupti et possimus excepturi, nam atque adipisci doloremque quae? Error dicta asperiores laudantium voluptatibus, non debitis. Harum, ab dolorum voluptates quidem architecto alias minus praesentium repellendus animi ad placeat deleniti qui recusandae numquam quod vel rem doloremque quo fugiat blanditiis debitis cupiditate. Ratione, iste repellat magni perspiciatis eum repudiandae ullam nam voluptates nobis facere quaerat esse, est maiores magnam culpa, illo veritatis itaque. Impedit ratione, laborum perspiciatis nam consequuntur temporibus tenetur quibusdam sed error, magni quo qui repudiandae nulla reiciendis consectetur et maiores odit vel cum sit unde optio exercitationem. Ipsum quaerat dolorem inventore! Cum sit architecto recusandae incidunt totam omnis autem consequatur vel, facilis unde enim cumque, eaque est voluptatibus fugiat minima praesentium cupiditate placeat eveniet dolorum rerum reiciendis, sed exercitationem voluptatum! Necessitatibus voluptatibus, vitae repellendus praesentium ducimus officiis corrupti aliquam sed mollitia cupiditate commodi, earum suscipit! Nesciunt nemo numquam deleniti doloribus placeat ut alias vitae amet, itaque totam nihil error soluta qui cum laborum incidunt quae voluptate eaque quo, modi perspiciatis nisi voluptates asperiores. Corrupti optio ullam illo similique illum expedita, accusantium impedit delectus suscipit porro soluta necessitatibus autem rerum architecto itaque id voluptatem sapiente eos quaerat ipsa consectetur placeat asperiores ea! Sapiente officia rerum, molestiae placeat laboriosam labore aliquid vel quo quod reprehenderit esse eaque quibusdam quas fugit architecto amet optio debitis omnis! Error impedit repellendus voluptate, fugiat quisquam velit rem esse, asperiores temporibus voluptatem eligendi deleniti adipisci sunt iusto animi sapiente porro ut incidunt consequuntur dolore! Qui, minus pariatur tempore eius aut officiis enim molestias earum velit, aliquam, eum magnam natus eaque facere quia laboriosam sapiente in fugit asperiores iste? Rem eos reiciendis tempora odio, similique laboriosam eligendi maiores aut dolorum nisi, fugit cum officia numquam voluptas dolores voluptatum vel id exercitationem assumenda asperiores repellendus. Ab, harum repudiandae consequuntur reprehenderit numquam dignissimos in vel asperiores beatae cumque porro illo at cupiditate sit sunt obcaecati qui et. Eius repellendus voluptates quia maxime sed placeat, sapiente soluta perspiciatis, iusto ipsum commodi, maiores tempore ab hic pariatur deleniti veritatis tempora error? Quaerat libero eos repudiandae neque sequi velit quod repellendus minus, iure voluptate officiis soluta esse ad et reiciendis voluptatibus ipsa dolores nemo cumque reprehenderit dolore enim! Eum at asperiores totam. Aperiam, possimus harum aut amet consequatur alias architecto. Ipsum molestiae ex atque, neque, rerum quasi tempore ipsam odio illo corporis molestias hic. Libero tempore omnis esse dolor dignissimos, saepe molestiae quia illum voluptas qui repellendus nobis sunt mollitia laboriosam cumque exercitationem placeat numquam molestias excepturi doloribus aut ullam nihil possimus inventore. Maiores atque optio veritatis nisi facilis. Sequi odio aspernatur dolor ducimus? Rem est doloremque earum similique doloribus totam ab velit fuga. Expedita beatae recusandae rerum sunt praesentium minus dignissimos iure veritatis. Recusandae at corrupti aspernatur porro, excepturi rem aperiam ea eaque omnis autem voluptate in vero veritatis sint qui quisquam repudiandae reiciendis delectus dolorem numquam ex molestiae. Ea perferendis harum delectus temporibus ut nisi obcaecati amet, incidunt est asperiores similique.【结束】</p>
		<p>【开始】Lorem ipsum dolor sit, amet consectetur adipisicing elit. Laboriosam soluta delectus quae fugiat atque ipsum exercitationem aliquam nam aperiam perspiciatis placeat, dolore autem tempore deserunt sit repudiandae numquam magni iure! Iusto minus, maiores corrupti beatae ratione consequuntur quos. Voluptates minima ipsum, mollitia exercitationem consectetur aliquid cupiditate voluptatum atque expedita, veniam ea illo ipsam est inventore delectus illum impedit voluptate. Maxime saepe quo id provident praesentium illo aspernatur officia magnam ullam dolores earum, consectetur quibusdam velit? Illo architecto placeat ipsam adipisci cumque natus quasi, neque eaque veniam dolores, culpa impedit expedita, quibusdam eos sequi iusto commodi doloribus? Velit, reprehenderit officiis.【结束】</p>
	</div>
</body>
</html>
```

#### 2.多列布局图片

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>02_多列图片案例</title>
	<style>
		.outer{
			/* 图片显示不全，是因为图片超出了所在列 */
			column-count: 5;
		}
		img {
			/* 加上宽度100%，就可以实现完全显示图片了 */
			width: 100%;
			transition: 0.2s linear;
			cursor: pointer;
		}

		/* 
			很多壁纸网站就是这么做的
		*/
		/* 还可以加各种事件 */
		img:hover{
			box-shadow: 0px 0px 20px black;
			transform: scale(1.02);
		}
</style>
</head>
<body>
	<div class="outer">
		<img src="../../img/img1.jpg" alt="">
		<img src="../../img/img2.jpg" alt="">
		<img src="../../img/img3.jpg" alt="">
		<img src="../../img/img4.jpg" alt="">
		<img src="../../img/img5.jpg" alt="">
		<img src="../../img/img6.jpg" alt="">
		<img src="../../img/img7.jpg" alt="">
		<img src="../../img/img8.jpg" alt="">
		<img src="../../img/img9.jpg" alt="">
		<img src="../../img/img10.jpg" alt="">
		<img src="../../img/img11.jpg" alt="">
		<img src="../../img/img12.jpg" alt="">
		<img src="../../img/img13.jpg" alt="">
		<img src="../../img/img14.jpg" alt="">
	</div>
</body>
</html>
```

### CSS3_伸缩盒模型

#### 1.伸缩盒模型简介

* 2009年，W3C提出了一种新的盒子模型--`Flexible Box`(伸缩盒模型，又称弹性盒子)
* 他可以轻松的控制：元素分布方式、元素对齐方式、元素视觉顺序...
* 截止目前，除了在部分IE浏览器不支持，其他浏览器均已全部支持
* 伸缩盒模型的出现，逐渐演变出了一套新的布局方案--flex布局

```sh
传统布局是指:基于传统盒模型，主要靠:display属性+position属性+float属性。
flex布局目前在移动端应用比较广泛，因为传统布局不能很好的呈现在移动设备上。
```

#### 2.伸缩容器、伸缩项目

##### 2.1伸缩容器

开启了flex的元素就是伸缩容器

```sh
1.给元素设置:"display:flex"或"display:inline-flex",该元素就变为了伸缩容器。
2."display:inline-flex"很少使用，因为可以给多个伸缩容器的父容器，也设置为伸缩容器。
3.一个元素可以同时是：伸缩容器、伸缩项目
```

##### 2.2伸缩项目

伸缩容器所有子元素自动成为了:伸缩项目。

```sh
1.仅伸缩容器的子元素成为了伸缩项目，其他后代元素并不是。
2.无论原来是哪种元素(块、行内块、行内)，一旦成为了伸缩项目，全都会"块状化"。
```

##### 2.3举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>01_伸缩容器_伸缩项目</title>
	<style>
		/* 
				对比浮动的优势:
				① 没有脱离文档流
		*/
		.outer {
			width: 600px;
			height: 600px;
			background-color: #888;

			/* 给outer元素开启了flex布局，outer元素就变成了伸缩容器 */
			/* 伸缩容器里面的所有的子元素都是伸缩项目--注意是子元素，不是所有后代元素 */
			display: flex;
			
			/* 
				开启flex布局变成伸缩容器，再变成行内块，这样就可以排在一行了
				不过一般不用，而是去找两个outer的父元素，这里的body
				给他开flex，也可以实现同样效果
			*/
			/* display: inline-flex; */

		}
		.inner {
			/* 
				只要一个元素变成了伸缩项目，之前无论是块、行内、行内块都会块状化
				即变成一个块
			*/
			width: 200px;
			height: 200px;
			background-color: skyblue;
			border: 1px solid black;
			box-sizing: border-box;
		}
	</style>
</head>
<body>
	<div class="outer">
		<div class="inner">1</div>
		<div class="inner">2</div>
		<div class="inner">3</div>
	</div>
	<div class="outer">
		<div class="inner">1</div>
		<div class="inner">2</div>
		<div class="inner">3</div>
	</div>
</body>
</html>
```

#### 3.主轴与侧轴

##### 3.1基本概念

>主轴

```sh
伸缩项目沿着主轴排列，主轴默认是水平的，默认方向是:从左往右。
```

>侧轴

```sh
侧轴与主轴垂直，侧轴默认是垂直的，默认方向:从上往下。
```

##### 3.2主轴方向

>属性名

```css
flex-direction
```

>常用值

```sh
row  水平从左到右，默认   | 侧轴垂直,从上到下
row-reverse 水平从右到左  | 侧轴垂直,从上到下
column   垂直从上到下     | 侧轴水平，从左到右
column-reverse 垂直从下到上 | 侧轴水平，从左到右
```

##### 3.3举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>02_主轴方向</title>
    <style>
        .outer{
            width: 1000px;
            height: 600px;
            background-color: #888;
            /* 伸缩盒模型相关的属性 */

            display: flex;

            /* 
                伸缩盒模型分主轴和侧轴
                主轴默认是水平方向，从左往右
                侧轴默认是垂直方向，从上往下

                元素默认按主轴排列，从主轴起始点到终点方向
                主轴方向一改动，侧轴就自动跟着改。没有专门的属性修改侧轴，侧轴和主轴垂直

            */
            /* 
                调整主轴方向 flex-direction
                值：
                row  水平从左到右，默认   | 侧轴垂直,从上到下
                row-reverse 水平从右到左  | 侧轴垂直,从上到下
                column   垂直从上到下     | 侧轴水平，从左到右
                column-reverse 垂直从下到上 | 侧轴水平，从左到右

            */
            flex-direction:column-reverse;
        }
        .inner {
            width: 200px;
            height: 200px;
            background-color: skyblue;
            border: 1px solid black;
            box-sizing: border-box;
        }
    </style>
</head>
<body>
    <div class="outer">
		<div class="inner">1</div>
		<div class="inner">2</div>
		<div class="inner">3</div>
	</div>
</body>
</html>
```

#### 4.主轴换行

> 属性名

```css
flex-wrap
```

>常用值

```sh
 主轴换行的方式 flex-wrap
①nowrap  默认值，不换行，当元素多时通过压缩来实现同行或同列排列
        即使我们设定了宽度或者高度，也会被压缩
"1 2 3 4 5 6 7"

        
②wrap    换行，同时要参考侧轴的对齐方式来决定下一行的位置
        从第一行开始，从左往右排，排不下再换行，最后可能溢出显示

"1 2 3 4 5"
"6 7 8"


③wrap-reverse 反向换行，是指从最下面开始排，相当于侧轴反转了
"6 7 8"
"1 2 3 4 5"
```

>所谓参考侧轴

```sh
根据侧轴分配的不同，换行后不一定是贴着的，可能均匀分布或者两侧分布等等...
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>03_主轴换行方式</title>
    <style>
        .outer{
            width: 1000px;
            height: 600px;
            background-color: #888;
            /* 伸缩盒模型相关的属性 */

            display: flex;

            flex-direction:row;
            /* 
                主轴换行的方式 flex-wrap
                ①nowrap  默认值，不换行，当元素多时通过压缩来实现同行或同列排列
                        即使我们设定了宽度或者高度，也会被压缩
                ②wrap    换行，同时要参考侧轴的对齐方式来决定下一行的位置
                        从第一行开始，从左往右排，排不下再换行，最后可能溢出显示

                ③wrap-reverse 反向换行，是指从最下面开始排，相当于侧轴反转了
            */
            flex-wrap: wrap-reverse;
        }
        .inner {
            width: 200px;
            height: 200px;
            background-color: skyblue;
            border: 1px solid black;
            box-sizing: border-box;
        }
    </style>
</head>
<body>
    <div class="outer">
		<div class="inner">1</div>
		<div class="inner">2</div>
		<div class="inner">3</div>
        <div class="inner">4</div>
		<div class="inner">5</div>
		<div class="inner">6</div>
        <div class="inner">7</div>
		<div class="inner">8</div>
		<div class="inner">9</div>
	</div>
</body>
</html>
```

#### 5.flex-flow

```sh
flex-flow是一个复合属性，复合了flex-direction和flex-wrap两个属性。值没有顺序要求。
```

```css
flex-flow:row wrap;
```

#### 6.主轴的对齐方式

>属性名

```sh
justify-content
```

>常用值

```sh
"flex-start"
主轴起点对齐。--默认值

"flex-end"
主轴终点对齐

"center"
居中对齐

"space-around"
均匀分布，两端距离是中间距离的一半

"space-between"
均匀分布，两端对齐(最常用)

"space-evenly"
均匀分布，两端距离与中间距离一致。
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>05.主轴的对齐方式</title>
    <style>
         .outer{
            width: 1000px;
            height: 600px;
            background-color: #888;
            /* 伸缩盒模型相关的属性 */
            display: flex;
            flex-direction:row;
            flex-wrap: wrap;  

            /* 
                主轴上的对齐方式
                属性：justify-content
                注意：是对齐位置改变，排列顺序不变，排列顺序只和轴的方向有关
                常用值:
                ① flex-start 默认值，主轴的起始位置对齐
                ② flex-end   主轴的结束位置对齐
                ③ center     主轴方向上居中
                ④ space-around 项目均匀分布在主轴上，项目与项目之间是2倍的大小，项目和边缘是1倍的大小
                ⑤ space-between  项目均匀分布在主轴上，项目与项目之间距离相等，项目与边缘之间没有距离
                ⑥ space-evenly   项目均匀分布在主轴上，项目与项目之间，项目和边缘之间距离都一样
            */
            justify-content: space-around;
        }
        .inner {
            width: 200px;
            height: 200px;
            background-color: skyblue;
            border: 1px solid black;
            box-sizing: border-box;
        }
    </style>
</head>
<body>
    <div class="outer">
		<div class="inner">1</div>
		<div class="inner">2</div>
		<div class="inner">3</div>
	</div>
</body>
</html>
```

#### 7.侧轴对齐方式--只有一行

>属性值

```css
align-items
```

>常用值

```sh
"flex-start"
侧轴的起始点对齐

"flex-end"
侧轴的终点对齐

"center"
侧轴的中间对齐

"baseline"
伸缩项目的第一行文字的基线对齐(用x)

"stretch"
如果伸缩项目未设置高度，将占满整个容器的高度。--默认值
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>侧轴对齐_一行</title>
    <style>
        .outer{
           width: 1000px;
           height: 600px;
           background-color: #888;
           /* 伸缩盒模型相关的属性 */
           display: flex;
           flex-direction:row;
           flex-wrap: wrap;  
           justify-content:flex-start;

           /* 
                侧轴对齐_一行
                属性:align-items
                值：
                ① flex-start 侧轴的起始位置对齐
                ② flex-end   侧轴的结束位置对齐
                ③ center     侧轴的中间位置对齐
                ④ baseline   文字基线位置对齐，几乎不用
                ⑤ stretch    所有的伸缩项目没有高度时生效，直接充满父容器高度(侧轴如果水平就是宽度)

                注意:
                1.stretch 才是默认值，拉伸到整个父容器，前提所有的伸缩项目没有高度(侧轴垂直)
                2.要所有的
           */
           align-items: flex-start;
       }
       .inner {
           width: 200px;
           height: 200px;
           background-color: skyblue;
           border: 1px solid black;
           box-sizing: border-box;
       }
       .inner2 {
            height: 300px;
            font-size: 80px;
       }
       .inner3 {
            height: 100px;
       }
   </style>
</head>
<body>
    <div class="outer">
		<div class="inner">1</div>
		<div class="inner inner2">2</div>
		<div class="inner inner3">3</div>
	</div>
</body>
</html>
```

#### 8.侧轴对齐方式_多行

>属性名

```css
align-content
```

>常用值

```sh
"flex-start"
侧轴起点对齐。--默认值

"flex-end"
侧轴终点对齐

"center"
居中对齐

"space-around"
均匀分布，两端距离是中间距离的一半

"space-between"
均匀分布，两端对齐(最常用)

"space-evenly"
均匀分布，两端距离与中间距离一致。

"stretch"
所有的伸缩项目没有高度/宽度时生效(根据侧轴方向)，项目都被拉伸，默认值
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>侧轴对齐_多行</title>
    <style>
        .outer{
           width: 1000px;
           height: 900px;
           background-color: #888;
           /* 伸缩盒模型相关的属性 */
           display: flex;
           flex-direction:row;
           flex-wrap: wrap;  
           justify-content:flex-start;

           /* 
            主轴方向上:
            一行的高度根据那一行中最高的那个伸缩项
            同理当主轴为纵向，那么列宽就是最宽的那个
           */
           /* 
                侧轴对齐_多行
                属性:align-content
                值：
                ① flex-start 侧轴的起始位置对齐
                ② flex-end   侧轴的结束位置对齐
                ③ center     侧轴的中间位置对齐
                ④ space-around 项目在侧轴上均匀分布，项目与项目之间距离相等，且是项目与边缘距离的两倍
                ⑤ space-between 项目在侧轴上均匀分布，项目与项目之间距离相等，项目与边缘之间没有距离
                ⑥ space-evenly  项目在侧轴上均匀分布，项目与项目之间，项目和边缘之间距离都一样
                ⑦ stretch  所有的伸缩项目没有高度/宽度时生效(根据侧轴方向)，项目都被拉伸，默认值
           */
           align-content: space-between;
       }
       .inner {
           width: 200px;
           height: 200px;
           background-color: skyblue;
           border: 1px solid black;
           box-sizing: border-box;
       }
       .inner2 {
            height: 300px;
       }
       .inner3 {
            height: 100px;
       }
   </style>
</head>
<body>
    <div class="outer">
		<div class="inner">1</div>
		<div class="inner inner2">2</div>
		<div class="inner inner3">3</div>
        <div class="inner">4</div>
        <div class="inner">5</div>
        <div class="inner">6</div>
        <div class="inner">7</div>
        <div class="inner">8</div>
        <div class="inner">9</div>
        <div class="inner">10</div>
        <div class="inner">11</div>
	</div>
</body>
</html>
```

#### 9.元素水平垂直居中

>方案1

```sh
① 父元素开启弹性盒子
② 使得伸缩项目在水平和垂直方向上对齐
```

>方案2

```sh
① 父元素开启弹性盒子
②子元素添加 margin:auto;
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>元素水平垂直居中</title>
    <style>
        .outer {
            width: 400px;
            height: 400px;
            background-color: #888;
            display:flex;

            /* 
                方案一
                ① 父元素开启弹性盒子
                ② 使得伸缩项目在水平和垂直方向上对齐
             */
            /* 
                justify-content: center;
                align-items: center;
             */
        }
        .inner {
            width: 100px;
            height: 100px;
            background-color: orange;

            /* 
                方案二
                ① 父元素开启弹性盒子
                ②子元素添加 margin:auto;
            */
            margin: auto;
        }
    </style>
</head>
<body>
    <div class="outer">
        <div class="inner">
        </div>
    </div>
</body>
</html>
```

#### 10.项目在主轴上的基准长度

>属性名

```sh
flex-basis
```

>概念

```sh
flex-basis设置的是主轴方向的基准长度,会让宽度或者高度失效
主轴横向,宽度失效;
主轴纵向,高度失效;
```

>作用

```sh
浏览器根据这个属性设置的值，计算主轴上是否有多余空间，默认值auto,即:伸缩项目的宽或高
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>项目在主轴的基准长度</title>
    <style>
        .outer{
           width: 1000px;
           height: 900px;
           background-color: #888;
           /* 伸缩盒模型相关的属性 */
           display: flex;
           flex-direction:row;
           flex-wrap: wrap;  
           justify-content:flex-start;
       }
       .inner {
           width: 200px;
           height: 200px;
           background-color: skyblue;
           border: 1px solid black;
           box-sizing: border-box;
       }
       .inner2 {
        /* 
            设置项目在主轴上的基准长度
            若主轴是横向的，就顶替掉宽度
            若主轴是纵向的，就顶替掉高度

            默认值是auto，这个属性的作用:
            浏览器根据这个属性来计算主轴上是否有富裕空间
        */
        flex-basis:300px ;
       }
   </style>
</head>
<body>
    <div class="outer">
		<div class="inner">1</div>
		<div class="inner inner2">2</div>
		<div class="inner">3</div>
	</div>
</body>
</html>
```

#### 11.伸缩项目_伸

>属性值

```sh
flex-grow
```

>概念

```sh
flex-grow定义伸缩项目的放大比例，默认为0，即
纵使主轴存在剩余空间也不拉伸(放大)
```

>规则

```sh
1.若所有的伸缩项目的flex-grow的值都为1，则:他们将等分剩余空间
2.若三个伸缩项目的flex-grow值分别是:1、2、3，则分别瓜分到:
1/6,2/6,3/6
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>伸缩项目_伸</title>
    <style>
        .outer{
           width: 1000px;
           height: 600px;
           background-color: #888;
           /* 伸缩盒模型相关的属性 */
           display: flex;
           flex-direction:row;
           flex-wrap: wrap;  
           justify-content:flex-start;
       }
       .inner {
           width: 200px;
           height: 200px;
           background-color: skyblue;
           border: 1px solid black;
           box-sizing: border-box;
           /* 
                默认没有拉伸，inner的3个盒子目前宽度
                200px 300px 200px
                通过计算和实际演示我们得出右边还有300px
           */
           /* 
                通过拉伸属性，我们可以实现对剩下300px的瓜分
                属性值：flex-grow
                值:
                参与瓜分的总人数y,每个人自己的数值x，被瓜分的内容z
                每个人瓜分到的 z*(x/y)

                flex-grow是加给伸缩项目
                分母y是所有伸缩项的总份数，flex-grow的和
                分子x是伸缩项flex-grow的值，不写默认0
                瓜分项Z是主轴的剩余空间
           */
           flex-grow: 1;
       }
       .inner2{
        width: 300px;
       }
   </style>
</head>
<body>
    <div class="outer">
		<div class="inner">1</div>
		<div class="inner inner2">2</div>
		<div class="inner">3</div>
	</div>
</body>
</html>
```

#### 12.伸缩项目_缩

>属性值

```sh
flex-shrink
```

>概念

```sh
flex-shrink定义了项目的压缩比例，默认值为1，即
如果空间不足，该项目将会缩小
```

>收缩项目的计算举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>伸缩项目_缩</title>
    <style>
        .outer{
           width: 400px;
           height: 600px;
           background-color: #888;
           /* 伸缩盒模型相关的属性 */
           display: flex;
           flex-direction:row;
           /* flex-wrap: wrap;   */
           justify-content:flex-start;
       }
       /* 
            压缩产生的时机:
            ① 父元素的空间不够了
            前提：
            1.不要换行，换行不会压缩，因为放不下会换行
            2.拿我们的这个举例，我们的盒子总大小为700px，加了flex-grow:1后，只要比700px大就还是拉伸，只是拉伸的没那么大
            3.换行后，主轴的剩余空间会重新计算，每个主轴独立
            4.小于我们给定的700px，在不换行的情况下就是压缩，即对于inner2，只要他小于300px就是压缩，反之拉伸

            ②压缩的计算
            举例:
            设定如下:
            盒子1 主轴上长度200px flex-shrink为1
            盒子2 主轴上长度300px flex-shrink为1
            盒子3 主轴上长度200px flex-shrink为2
            父亲最终变成400px，压缩了300px

            收缩比的分母: 
            (盒子1主轴上长度*盒子1的flex-shrink)+ (盒子2主轴上长度*盒子2的flex-shrink)+ (盒子3主轴上长度*盒子3的flex-shrink) = 900

            收缩比计算:
            盒子1的收缩比:(盒子1主轴上长度*盒子1的flex-shrink)/900
            盒子2的收缩比:(盒子2主轴上长度*盒子2的flex-shrink)/900
            盒子3的收缩比:(盒子3主轴上长度*盒子3的flex-shrink)/900

            最终的收缩结果:
            盒子1的收缩值: 盒子1的收缩比 * 父亲压缩的大小
            盒子2的收缩值: 盒子2的收缩比 * 父亲压缩的大小
            盒子3的收缩值: 盒子3的收缩比 * 父亲压缩的大小

            像素差在0点几，多数是浏览器对边框的计算产生了误差，设定了box-sizing也没用，除非不要边框
            但是这点误差影响不大，所以边框样式最好保留

            flex-shrink 管压缩，默认值为1

            收缩的极限:
            即使父亲的宽度为0了，子元素还是有宽度，保证内容的呈现，由内容撑开宽度
       */
       .inner {
           width: 200px;
           height: 200px;
           background-color: skyblue;
           border: 1px solid black;
           box-sizing: border-box;
       }
       .inner2{
        width: 300px;
       }
       .inner3{
        flex-shrink: 2;
       }
   </style>
</head>
<body>
    <div class="outer">
		<div class="inner">1</div>
		<div class="inner inner2">2</div>
		<div class="inner inner3">3</div>
	</div>
</body>
</html>
```

#### 13.伸缩项目_flex复合属性

```sh
flex: flex-grow flex-shrink flex-basis;
# 有顺序限制
```

>常用的四个简写

```sh
flex: 1 1 auto; 
==>可简写为 flex:auto;
flex: 1 1 0; 
==>可简写为 flex:1;  (基准变为0，我们设定的主轴长度就没意义了，但是会显示，因为拉伸)
flex: 0 0 auto;
==>可简写为 flex:none; (不可压缩)
flex:0 1 auto;
==>默认值，可简写为 flex:0 auto;
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>flex复合属性</title>
    <style>
        .outer{
           width: 1000px;
           height: 600px;
           background-color: #888;
           /* 伸缩盒模型相关的属性 */
           display: flex;
           flex-direction:row;
           flex-wrap: wrap;  
           justify-content:flex-start;
       }
       .inner {
           width: 200px;
           height: 200px;
           background-color: skyblue;
           border: 1px solid black;
           box-sizing: border-box;

            /* ################### */
            /* 拉伸属性 */
            /* flex-grow: 1; */
            /* 压缩属性 */
            /* flex-shrink: 1; */
            /* 基准长度 */
            /* flex-basis: 100px; */
            /* ################# */

            /* 
                flex复合属性，有顺序要求

                flex: flex-grow flex-shrink flex-basis
            */
            flex: 1 1 auto;

            /* 
                flex: 1 1 auto; ==>可简写为 flex:auto;
                flex: 1 1 0; ==>可简写为 flex:1;  (基准变为0，我们设定的主轴长度就没意义了，但是会显示，因为拉伸)
                flex: 0 0 auto;==>可简写为 flex:none; (不可压缩)
                flex:0 1 auto;==>默认值，可简写为 flex:0 auto;
            */
       }
       
   </style>
</head>
<body>
    <div class="outer">
		<div class="inner">1</div>
		<div class="inner">2</div>
		<div class="inner">3</div>
	</div>
</body>
</html>
```

#### 14.伸缩项目排序

>属性值

```sh
order
```

>概念

```sh
属性定义项目的排列顺序，数值越小，排列越靠前，所有项目默认值为0
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>项目排序</title>
    <style>
        .outer{
           width: 1000px;
           height: 600px;
           background-color: #888;
           /* 伸缩盒模型相关的属性 */
           display: flex;
           flex-direction:row;
           flex-wrap: wrap;  
           justify-content:flex-start;
       }
       .inner {
           width: 200px;
           height: 200px;
           background-color: skyblue;
           border: 1px solid black;
           box-sizing: border-box;
           flex: 1 1 0;
       }
       /* 
            需求:
            默认顺序是 1、2、3
            然后根据我们的各种对齐排序

            实际上所有伸缩项的排序order默认是0
            order越大排在后，order越小排在前,order一样按照代码顺序

            我们想要2到1前面
       */
       .inner2{
            order: -1;
       }
   </style>
</head>
<body>
    <div class="outer">
		<div class="inner">1</div>
		<div class="inner inner2">2</div>
		<div class="inner">3</div>
	</div>
</body>
</html>
```



#### 15.伸缩项目单独排序

>属性

```sh
align-self
```

>概念

```sh
1.通过align-self属性，可以单独调整某个伸缩项目的对齐方式
2.默认值为auto，表示继承父元素的align-items属性
```

>举例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>项目排序</title>
    <style>
        .outer{
           width: 1000px;
           height: 600px;
           background-color: #888;
           /* 伸缩盒模型相关的属性 */
           display: flex;
           flex-direction:row;
           flex-wrap: wrap;  
           justify-content:flex-start;
       }
       .inner {
           width: 200px;
           height: 200px;
           background-color: skyblue;
           border: 1px solid black;
           box-sizing: border-box;
           flex: 1 1 0;
       }
       /* 
        单独调节某个项目在侧轴方向上的对齐方式
        属性值和单行侧轴对齐一样
       */
       .inner2{
        align-self: flex-end;
       }
   </style>
</head>
<body>
    <div class="outer">
		<div class="inner">1</div>
		<div class="inner inner2">2</div>
		<div class="inner">3</div>
	</div>
</body>
</html>
```

