# HTML5---canvas
##1.canvas基本用法
* 1.canvas
	* 用js脚本绘制图形
	* 宽高
		* 默认值width-300px；height-150px
		* html属性：只影响画布本身
		* css属性:会影响画布里面的内容等比例缩放
		！ 不能在css中设置宽高
	* < canvas> xxx </canvas>
		* xxx：只是替代内容
		* 当浏览器版本不支持canvas的时候会显示
	
* 2.用法
	* 1.获取画布
		* var canvas = document.querySelector（"canvas"）;
	* 2.获取画笔
		* canvas.getcontext("2d") 
		* 一般情况下使用时先判断是否有画笔
			* if（canvas.getcontext）{}
# 2.绘制矩形 直接画出来
* 1.绘制矩形
	* a:绘制填充矩形 （默认填充黑色）
		* fillRect（x，y，width，height）
	* b:绘制描边矩形（默认描边为1像素的实心边框，有问题） 
		* strokeRect（x,y.width,height）
	* c:清除矩形区域
		* clearRect（x,y,width,height） 
* x/y指的是所画矩形的左上角坐标（相对于原点） 
* width/height设置举行的尺寸
* 2.边框渲染问题
* strokeRect（x，y，width，height）（默认描边为1像素的实心边框，--但是由于它是往两边括0.5px但是js识别不了小数，so实际上为2px，内外各1px） 
* 解决方案：strokeRect（1.5，1.5，width，height）由于浏览器不支持小数点
* 3.添加样式和颜色
	* fillStyle ：填充颜色
	* strokeStyle：描边颜色
	* lineWidth：描边宽度 只能为正值。无单位
	* lineGap: 线断结束的样式
		* butt 方形结束 默认
		* round 以圆形结束
		* square 以方形结束，但是增加了一个宽度和线段相同，高度是线段厚度一半的矩形区域
	* lineJoin：线条之间的结合处的样式
		* round：圆角
		* bevel：斜角
		* miter：直角 （默认）
# 3.绘制路径  --通过线段之类的连起来的
* 1.绘制路径
	* 通过不同颜色和宽度的线段或者曲线相连形成不同形状的点的集合
* 2.步骤
	* 1.创建路径起始点
	* 2.用画图命令画路径
	* 3.封闭路径
	* 4.路径生成，通过描边填充来渲染
* 3.
	* beginPath（） --新建路径
		* 由于路径是由一堆小路径组成的，
		* 使用它可以清空重置
		* 重新绘制
	* moveTo（x，y） 
		* 移动到指定坐标
		* 通过它设置起点
	* lineTo（x,y）
		* 移动到指定的坐标
		* 绘制从当前位置到指定位置的直线
	* closePate（）
		* 闭合路径  
		* fill（）函数会自动闭合 
	* stroke（）
		* 通过线段绘制图形轮廓  
	* fill（）
		* 通过填充
	* rect （x,y,width,height）
		* 绘制矩形  
	* save（）
		*  将当前状态放入栈中，保存各种样式
		*  fillStyle
		*  strokeStyle
		*  lineWidth
		*  lineCap
		*  lineJoin ....
	* restore
		*通过在绘图状态栈中弹出顶端的状态，将canvas恢复到最近的保存状态
* 用法
	* ctx.save();
	* ctx.beginPath();
	* ctx.restore();  
	* 相当于一个块级作用域
	* 成对出现
* 路径容器 -- 每次调用API时都会往路径容器中做登记;
	* 调用beginPath 时清空整个路径容器
* 样式容器
	* 每次调用样式API的时候，都会往样式容器里面做登记
	* 调用save的时候，将样式容器里的状态压入样式栈
	* 调用restore的时候，将样式栈的栈顶状态弹出到样式容器里面，进行覆盖
* 样式栈
	* 调用save的时候，将样式容器里的状态压入样式栈
	* 调用restore的时候，将样式栈的栈顶状态弹出到样式容器里面，进行覆盖 
* 样式容器
# 4.绘制圆形
* 用法
	* arc（x,y,radius,startAngle，endAngle，anticlockwise） 
		* x,y圆心坐标
		* radius 半径
		* angle 起始弧度 终点弧度
		* 布尔值 true 逆时针 flase为顺时针
	* arcTo（x1，y1，x2，y2，radius）
		* 根据给定的控制点和半径画一段圆弧
* 贝赛尔曲线
	* 二次贝塞尔
		* quadraticCurveTo（cp1x，cp1y，x，y） 
	* 三次贝赛尔
		* bezierCurveTo（cp1x，cp1y，cp2y，x，y） 