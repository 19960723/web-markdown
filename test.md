## 常规知识点
this
	代表函数调用相关联的对象，通常也称之为执行上下文
1. js基础知识
	- 基本类型
		Number、String、Boolean、undefined、null、Symbol(es6)
		基本数据类型是按值访问 由高向低分配,栈内存最大是 8MB,（超出报栈溢出）
		Number: 8 字节
		String: 每个长度 2 字节
		Boolean: 4 字节
	- 引用数据
		Object、Array、Function、Date
	- 数据结构分类
		逻辑结构: 反映数据之间的逻辑关系
		储存结构: 数据结构在计算机中的表示
	
2. 从输入url到获得页面经历的所有事情(越细越好)
	- 1. 对网址进行DNS解析, 得到对应的IP
	- 2. 根据这个IP, 找到对应的服务器, 发起TCP三次握手
	- 3. 建立TCP链接后发起HTTP请求 (tcp是比http更底层的一个连接协议) (ip是tcp下面一层)
	- 4. 服务器响应HTTP请求, 浏览器得到html代码
	- 5. 浏览器解析 html 代码, 并请求 html 代码中的资源(js、css、img) (先得到html代码, 才能去找这些资源)
	- 6. 浏览器对页面进行渲染呈现给用户
	- 7. 服务器关闭TCP连接
	
2. 闭包
	闭包就是能够访问外部函数变量的一个函数
	闭包是将函数内部和函数外部连接起来的桥梁
	作用
		- 可以读取函数内部的变量
		- 让这些变量的值始终保持在内存中，不会在f1调用后被自动清除
	使用场景
		封装功能时(需要使用私有的属性和方法)，函数防抖、函数节流、函数柯里化、给元素伪数组添加事件需要使用元素的索引值
	如何避免闭包引起的内存泄漏
		- 1. 在退出函数之前，将不使用的局部变量全部删除，可以使变量赋值为null
		- 2. 避免变量的循环赋值和引用(代码如上)
	
2.1 内存泄漏
	原因
		- 意外的全局变量(在函数内部没有使用var进行声明的变量)
		- console.log
		- 闭包
		- 对象的循环引用
		- 未清除的计时器
		- DOM泄露(获取到DOM节点之后，将DOM节点删除，但是没有手动释放变量，拿对应的DOM节点在变量中还可以访问到，就会造成泄露)


3. 原型链
	- 每个对象都会在其内部初始化一个属性, 原型也是一个对象, 所以原型上也有原型
	- 当我们访问一个对象的属性时, 如果这个对象内部不存在这个属性, 那么他就会去 prototype 里找这个属性, 
	这个prototype又会有自己的prototype, 于是就这样一直找下去,也就是我们平时所说的原型链概念
	- 就是利用原型让一个引用类型继承另一个引用类型的属性和方法
	- 举例说明： Student → Person → Object ，学生继承人类，人类继承对象类
4. 继承
	ES5
		1. 原型链继承
		2. 构造函数继承
		3. 组合继承
		4. 寄生组合式继承
	ES6
		5. es6 类继承
5. es6新特性
	- let、 const
	- 解构赋值
	- 箭头函数
	- class 类
	- 模块 
	- Promise
	- Generator
	- async / await
6. DOM事件和事件流
	addEventlistener
		- 绑定事件对象.addEventListener(事件类型，回调函数，布尔值) 
			- 如果不传布尔值或为falsy值 -- fn就会走冒泡阶段
			- 如果布尔值为true -- fn 就会走捕获阶段
	事件流
		- 事件捕获阶段
			从window对象传导到目标节点（上层传到底层）称为“捕获阶段”（capture phase），捕获阶段不会响应任何事件
		- 目标阶段
			在目标节点上触发，称为“目标阶段”
		- 事件冒泡阶段
			从目标节点传导回window对象（从底层传回上层），称为“冒泡阶段”（bubbling phase）。
			事件代理即是利用事件冒泡的机制把里层所需要响应的事件绑定到外层
		事件委托
			优点: 
				- 可以大量节省内存占用, 减少事件注册, 比如在ul上代理所有li的click事件就非常棒
				- 可以实现当新增子对象时无需再次对其绑定（动态绑定事件）
			注意:
				- 使用“事件委托”时，并不是说把事件委托给的元素越靠近顶层就越好。事件冒泡的过程也需要耗时，越靠近顶层，事件的”事件传播链”越长，也就越耗时。如果DOM嵌套结构很深，事件冒泡通过大量祖先元素会导致性能损失
7. 盒子模型
	- content
	- padding
	- border
	- margin
	
8. 事件循环
	js 是单线程执行的, 先执行同步 -> 异步 (微任务 [存入微任务队列] -> 宏任务 [存入宏任务队列])   
	反复执行以上步骤就是 事件循环了
	
9. BFC
	形成一个完全独立的空间，让空间中的子元素不会影响到外面的布局
	触发BFC的方式
		- 根元素或其它包含它的元素
		- 浮动元素 (元素的 float 不是 none)
		- 绝对定位元素 (元素具有 position 为 absolute 或 fixed)
		- 内联块 (元素具有 display: inline-block)
		- 表格单元格 (元素具有 display: table-cell，HTML表格单元格默认属性)
		- 表格标题 (元素具有 display: table-caption, HTML表格标题默认属性)
		- 具有overflow 且值不是 visible 的块元素，
		- display: flow-root:  除了兼容性问题，用display: flow-root来触发BFC最佳,不会产生任何副作用
		- column-span: all 应当总是会创建一个新的格式化上下文，即便具有 column-span: all 的元素并不被包裹在一个多列容器中

	解决的问题
		1. 浮动元素
			- 解决浮动元素令父元素高度塌陷的问题
				浮动元素会脱离文档流，如果父元素的高度是由原本的浮动元素撑起的话，元素一旦浮动，就会造成父元素的高度坍塌，因为浮动元素脱离文档流，不参加高度计算
				解决:
					- 元素father设置 display：flow-root;触发BFC,因为计算BFC高度时，浮动元素也参加计算
				```
					.father{
					  border: 5px solid;
					  width: 400px;
					}
					.son {
					  background: pink;
					  width: 400px;
					  height: 50px;
					}
					<div class="father">
						<div class="son"></div>
					</div>
				```
			- 兄弟间，浮动元素与不浮动元素界限不清，重叠
				- 浮动元素left与未浮动元素right重叠在一起，界限不清
				- 如果不想他们重叠在一起，则可以借助BFC来使其不重叠，利用这个特性，我们可以创造自适应两栏布局
				解决
					- 给元素right添加display:flow-root;属性
				```
					.left {
						float: left;
						border: 1px solid ;
						width: 300px;
						height: 100px;
					}
					.right {
						border: 1px solid red;
						height: 200px;
						// display: flow-root; 开启 BFC
					}
					<div class="left">left</div>
					<div class="right">right</div>
				```
		2. 解决自适应布局的问题 (两栏自适应布局)
			类似于上面 浮动元素 的问题     (兄弟间，浮动元素与不浮动元素界限不清，重叠)
		3. 解决外边距垂直方向重合问题 (外边距垂直方向重合)
			- 父子元素margin 重叠
				解决:
					- 使父元素形成一个BFC:在father元素中添加 overflow: hidden/auto; 或 display：flow-root
					- 在father元素中添加border：1px solid；或是padding：1px；
				```
				.father{
				  background: pink;
				  height: 100px;
				  width: 400px;
				  // padding-top: 1px;
				}
				.son {
				  margin-top: 50px;
				  background: #000;
				  height: 50px;
				}
				
				<div class="father">
					<div class="son"></div>
				</div>	
			```
			- 相邻元素垂直外边距折叠问题
				原因： 相邻垂直边距margin产生合并，并以最大的那个作为边距
				解决
					给元素didi外面包一个元素(div)wrap，并触发wrap的BFC
				```
					.gege {
					  background: red;
					  width: 100px;
					  height: 100px;
					  margin: 40px;
					}
					.didi {
					  background: green;
					  width: 100px;
					  height: 100px;
					  margin: 40px;
					}
					<!-- <div class="didi">didi</div> -->
					<div style="display: flow-root"><div class="didi">didi</div></div>  父元素开启 BFC
				```
				
10. Flex   
	父元素设置 display: flex; 开启弹性布局
		container
			- flex-direction 修改主轴
			- flex-wrap 是否换行
			- justify-content 主轴的对齐方式
			- align-items 交叉轴的对齐方式
			- align-content 多根轴线的对齐方式
		items
			- order 排序 数值越小，排列越靠前
			- flex  默认值为0 1 auto
			- self-align 可覆盖align-items
11. Promise原理以及手写代码
	- Promise 是异步编程的一种解决方式
	- 可以很好地解决回调地域的问题 (避免层层嵌套的回调函数)
12. Vue响应式原理
	Object.defindProperty() 这个是响应式原理的基础
		- 在访问和设置对应的属性的时候可以劫持这个属性的访问，这也是vue响应式原理的基础
13. Vue虚拟dom & diff 算法
14. 前端性能优化
15. 防抖节流
	- 函数防抖
		概念
			就是指触发事件后在 n 秒内函数只能执行一次，如果在 n 秒内又触发了事件，则会重新计算函数执行时间
			在一段固定的时间内，只能触发一次函数，在多次触发事件时，只执行最后一次
		使用时机
			搜索功能，在用户输入结束以后才开始发送搜索请求，可以使用函数防抖来实现
	- 函数节流
		概念
			就是限制一个函数在一定时间内只能执行一次
		使用时机
			改变浏览器窗口尺寸，可以使用函数节流，避免函数不断执行
			滚动条scroll事件，通过函数节流，避免函数不断执行
	区别
		节流是为了限制函数的执行次数，而防抖是为了限制函数的执行时机
16. HTTP缓存
17. 常见算法(排序洗牌等)

























