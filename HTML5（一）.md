#HTML5
##一、attribute和property
### 1.区分attribute和property
* attribute -- html标签的预定义和自定义属性，统称为atribute。
	* 属性节点 
		* var div = document.querySelector("#div")； -- 先获取元素节点。
		* var attr = div.attributes； -- 获取这个元素的属性的集合。
		* attr.name.nodeValue; --获取name属性的值。
		* 这就是attribute。
* property -- js原生对象的直接属性。
		* var name = div.name;
		* 直接调用原生对象的属性。
### 2.区分布尔值属性和非布尔值属性
* property的属性值为布尔值，就是布尔值属性；
* property的属性值为非布尔值的时候，就是非布尔值属性；
### 3.attribute和property的同步关系
* 非布尔值属性：实时同步，要改一起改
* 布尔值属性：
	* property 永远不会同步attribute
	* 在没有动过property的情况下，attribute会同步property
	* 在动过property的情况下，attribute不会同步property
* so ：在操作一些类似checked这样的属性的时候 使用prop 
### 4.用户操作 property
### 5.浏览器只认 property
## 二、html5
### 1.html5新增的属性
* a：新增js中操作html的class属性
	* testNode.className -- 获取class内容
	* testNode.classList -- 获得一个类数组对象
	* testNode.classList.add("") -- 添加class值
	* testNode.classList.remove("") -- 移出某个class值
	* testNode.classList.toggle(""）-- 若有的话就移出，没有的话就添加
* b： 自定义属性  
	* 在html中：自定义属性前面加data-
		* < div id="div1" data-atguigu="xxx">
	* js中获取：.dataset.xxx
		* testNode.dataset.atguigu(可驼峰命名)
		* testNode.dataset.atguigu="xxx" -- 重输值
* c：可编辑
	* 在html中添加属性
	* div id="new" contenteditable="true";
	* 就算是一个div里面也可以编辑了
### 2.HTML5
* a:概念 
	* 定义HTML标准的最新版
	* 是一个新版本的的HTML语言，具有新的元素，属性和行为。
	* 有更大的技术集，允许更多样化和强大的网站和应用程序
	* HTML5 ~= HTML + CSS + JS
* b:优势
	*  跨平台：PC MAC Iphone Android
	*  快速迭代
	*  降低成本
	*  导流入口多
	*  分发效率高
* c:写法
	* < !DOCTYPE HTML> 通知浏览器遵守H5规范
		* 若不写的话会出现问题
		* IE5.5之前 自己渲染的是怪异模式
		* IE6 慢慢支持标准 但是怪异和标准模式的区别最大
		* IE7.8.9基于标准模式，理论上有怪异模式但是没有 
	* < meta charset="UTF-8" >
		* 告诉浏览器使用哪种编码来解析网页
		* 后果：乱码 
	* 怪异盒子模型就是box-sizing：border-box 
* d: 语义化标签  
	* <hgroup> </hgroup> -- 将h1~h6放入里面 通常放到header
	* <header></header> -- 页眉
	* <nav></nav> -- 导航
	* <section></section> -- 节或段
	* <footer></footer> --尾部
	* <article></article>
	* <aside></aside>