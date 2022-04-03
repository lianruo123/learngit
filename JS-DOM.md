# JS-DOM

### Document Object Model

- 文档对象模型，通过DOM可以来任意来修改网页中各个内容
- 文档
	- 文档指的是网页，一个网页就是一个文档
- 对象
	- 对象指将网页中的每一个节点都转换为对象
		转换完对象以后，就可以以一种纯面向对象的形式来操作网页了
- 模型
	- 模型用来表示节点和节点之间的关系，方便操作页面
- 节点（Node）
	- 节点是构成网页的最基本的单元，网页中的每一个部分都可以称为是一个节点
	- 虽然都是节点，但是节点的类型却是不同的
	- 常用的节点
		- 文档节点 （Document），代表整个网页
		- 元素节点（Element），代表网页中的标签
		- 属性节点（Attribute），代表标签中的属性
		- 文本节点（Text），代表网页中的文本内容

### DOM操作

console.dir()可以打印我们获取的元素对象。

##### DOM查询

在网页中浏览器已经为我们提供了document对象，
它代表的是整个网页，它是window对象的属性，可以在页面中直接使用。

**document查询方法：**

- 根据元素的id属性查询一个元素节点对象：
	- document.getElementById("id属性值");
- 根据元素的name属性值查询一组元素节点对象:
	- *document.getElementsByName("name属性值");*
- 根据标签名来查询一组元素节点对象：
  - document.getElementsByTagName("标签名");

- 还可以获取某个元素(父元素)内部所有指定标签名的子元素
  - element.getElementsByTagName('标签名');	

- 通过 HTML5 新增的方法获取

  document.getElementsByClassName(‘类名’)；// 根据类名返回元素对象集合document.querySelector('选择器');        // 根据指定选择器返回第一个元素对象document.querySelectorAll('选择器');     // 根据指定选择器返回

-  获取特殊元素（body，html）

  doucumnet.body  // 返回body元素对象

  document.documentElement  // 返回html元素对象

##### 元素的属性

- 读取元素的属性：
	语法：元素.属性名
	例子：ele.name  
		  ele.id  
		  ele.value 
		  ele.className
	
- 修改元素的属性：
	语法：元素.属性名 = 属性值
	
- innerHTML
	- 使用该属性可以获取或设置元素内部的HTML代码


​				

##### 事件（Event）

​	事件三要素

			1. 事件源 （谁）
			2. 事件类型 （什么事件）
			3. 事件处理程序 （做啥）

- 事件指的是用户和浏览器之间的交互行为。比如：点击按钮、关闭窗口、鼠标移动。。。

- 我们可以为事件来绑定回调函数来响应事件。

- 绑定事件的方式：
	1.可以在标签的事件属性中设置相应的JS代码
		例子：
			<button onclick="js代码。。。">按钮</button>
	2.可以通过为对象的指定事件属性设置回调函数的形式来处理事件
		例子：
			<button id="btn">按钮</button>
	
	<script>
			var btn = document.getElementById("btn");
			btn.onclick = function(){
	            };
	</script>

![image-20220327172624519](../../../../../../AppData/Roaming/Typora/typora-user-images/image-20220327172624519.png)

##### 文档的加载

- 浏览器在加载一个页面时，是按照自上向下的顺序加载的，加载一行执行一行。

- 如果将js代码编写到页面的上边，当代码执行时，页面中的DOM对象还没有加载，
	此时将会无法正常获取到DOM对象，导致DOM操作失败。
	
- 解决方式一：
	- 可以将js代码编写到body的下边
	  
	  <body>
	  <button id="btn">按钮</button>
	  
	  <script>
	  	var btn = document.getElementById("btn");
	  	btn.onclick = function(){
	      };
	  </script>
	  
	  </body>
	  
	  ​	
	
- 解决方式二：
	- 将js代码编写到**window.onload = function(){}**中
	- window.onload 对应的回调函数会在整个页面加载完毕以后才执行，
		所以可以确保代码执行时，DOM对象已经加载完毕了
	<script>
		window.onload = function(){
			var btn = document.getElementById("btn");
			btn.onclick = function(){
	        };
	</script>        

### 改变元素内容

​	**element.innerText**		从起始位置到终止位置的内容, 但它去除 html 标签， 同时空格和换行也会去掉

​	**element.innerHTML**   	起始位置到终止位置的全部内容，包括 html 标签，同时保留空格和换行

**innerHTML 和 innerText**
		- 这两个属性并没有在DOM标准定义，但是大部分浏览器都支持这两个属性
		- 两个属性作用类似，都可以获取到标签内部的内容，
			不同是innerHTML会获取到html标签，而innerText会自动去除标签
		- 如果使用这两个属性来设置标签内部的内容时，没有任何区别的



src、herf、id、alt、title:  element.~~ = new ~~



1. **element.style**     行内样式操作

   - 使用style属性来操作元素的内联样式
   - 读取内联样式：
     语法：元素.style.样式名
     - 例子：
       元素.style.width
       元素.style.height
       - 注意：如果样式名中带有-，则需要将样式名修改为驼峰命名法
         将-去掉，然后-后的字母改大写
       - 比如：background-color --> backgroundColor
         	border-width ---> borderWidth

   - 修改内联样式：
     语法：元素.style.样式名 = 样式值
     - 通过style修改的样式都是内联样式，由于内联样式的优先级比较高，
       所以我们通过JS来修改的样式，往往会立即生效，
       但是如果样式中设置了!important，则内联样式将不会生效

2. **element.className** 类名样式操作

   1. 如果样式修改较多，可以采取操作类名方式更改元素样式。 
   2. class因为是个保留字，因此使用className来操作元素类名属性
   3. className 会直接更改元素的类名，会覆盖原先的类名。

### HTML Input属性

**type**    属性

**value属性**规定输入字段的初始值

**readonly 属性**规定输入字段为只读（不能修改）	readonly 属性不需要值。它等同于 readonly="readonly"				

**disabled 属性**规定输入字段是禁用的。被禁用的元素是不可用和不可点击的。被禁用的元素不会被提交。		
**size 属性**规定输入字段的尺寸（以字符计）		
**maxlength 属性**规定输入字段允许的最大长度

**autocomplete 属性**规定表单或输入字段是否应该自动完成。当自动完成开启，浏览器会基于用户之前的输入值自动填写值。		
	您可以把表单的 autocomplete 设置为 on，同时把特定的输入字段设置为 off，反之亦然。autocomplete 属性适用于 <form> 以及如下 <input> 类型：text、search、url、tel、email、password、datepickers、range 以及 color。	min 和 max 属性规定 <input> 元素的最小值和最大值。

**min 和 max 属性**适用于如需输入类型：number、range、date、datetime、datetime-local、month、time 以及 week。		

### DOM查询

	- 通过具体的元素节点来查询
		- 元素.getElementsByTagName()
		 - 通过标签名查询当前元素的指定后代元素

	- 元素.childNodes
		- 获取当前元素的所有子节点
		- 会获取到空白的文本子节点
	
	- 元素.children
		- 获取当前元素的所有子元素
	
	- 元素.firstChild
		- 获取当前元素的第一个子节点
	
	- 元素.lastChild
		- 获取当前元素的最后一个子节点
	
	- 元素.parentNode
		- 获取当前元素的父元素
	
	- 元素.previousSibling
		- 获取当前元素的前一个兄弟节点
	
	- 元素.nextSibling
		- 获取当前元素的后一个兄弟节点
		

innerHTML和innerText
	- 这两个属性并没有在DOM标准定义，但是大部分浏览器都支持这两个属性
	- 两个属性作用类似，都可以获取到标签内部的内容，
		不同是innerHTML会获取到html标签，而innerText会自动去除标签
	- 如果使用这两个属性来设置标签内部的内容时，没有任何区别的	
	

读取标签内部的文本内容
	<h1>h1中的文本内容</h1>
​	元素.firstChild.nodeValue
​	
- document对象的其他的属性和方法
	document.all
		- 获取页面中的所有元素，相当于document.getElementsByTagName("*");
		
	
	document.documentElement
		- 获取页面中html根元素
		
	
	document.body
		- 获取页面中的body元素
		
	
	document.getElementsByClassName()
		- 根据元素的class属性值查询一组元素节点对象
		- 这个方法不支持IE8及以下的浏览器
		
	
	document.querySelector()
		- 根据CSS选择器去页面中查询一个元素
		- 如果匹配到的元素有多个，则它会返回查询到的第一个元素	
		
	
	document.querySelectorAll()	
		- 根据CSS选择器去页面中查询一组元素
		- 会将匹配到所有元素封装到一个数组中返回，即使只匹配到一个		

### DOM修改

​	document.createElement()
		- 可以根据标签名创建一个元素节点对象
		

document.createTextNode()
	- 可以根据文本内容创建一个文本节点对象
	

父节点.appendChild(子节点)
	- 向父节点中添加指定的子节点
	

父节点.insertBefore(新节点,旧节点)
	- 将一个新的节点插入到旧节点的前边
	

父节点.replaceChild(新节点,旧节点)
	- 使用一个新的节点去替换旧节点
	

父节点.removeChild(子节点)
	- 删除指定的子节点
	- 推荐方式：子节点.parentNode.removeChild(子节点)		

### DOM对CSS的操作

- 读取元素的当前样式
	- 正常浏览器
		- 使用getComputedStyle()
		- 这个方法是window对象的方法，可以返回一个对象，这个对象中保存着当前元素生效样式
		- 参数：
			1.要获取样式的元素
			2.可以传递一个伪元素，一般传null
		- 例子：
			获取元素的宽度
				getComputedStyle(box , null)["width"];
		- 通过该方法读取到样式都是只读的不能修改

	- IE8
		- 使用currentStyle
		- 语法：
			元素.currentStyle.样式名
		- 例子：
			box.currentStyle["width"]
		- 通过这个属性读取到的样式是只读的不能修改

- 其他的样式相关的属性
	注意：以下样式都是只读的

	clientHeight
		- 元素的可见高度，指元素的内容区和内边距的高度
		clientWidth
		- 元素的可见宽度，指元素的内容区和内边距的宽度
		offsetHeight
		- 整个元素的高度，包括内容区、内边距、边框
		offfsetWidth
		- 整个元素的宽度，包括内容区、内边距、边框
		offsetParent
		- 当前元素的定位父元素
		- 离他最近的开启了定位的祖先元素，如果所有的元素都没有开启定位，则返回body
		offsetLeft
		offsetTop
		- 当前元素和定位父元素之间的偏移量
		- offsetLeft水平偏移量  offsetTop垂直偏移量
	
	scrollHeight
	scrollWidth
		- 获取元素滚动区域的高度和宽度
	
	scrollTop
	scrollLeft
		- 获取元素垂直和水平滚动条滚动的距离
		
	
	判断滚动条是否滚动到底
		- 垂直滚动条
			scrollHeight - scrollTop = clientHeight
			
		- 水平滚动	
			scrollWidth - scrollLeft = clientWidth


​		
​				