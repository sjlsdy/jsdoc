<template>
	<div class="hello">
		<div v-for="val in jsdata">
			<h2 v-html="val.name">
				</h2>
			<div v-for="item in val.children">
				<h3 v-html="item.name">
				</h3>
				<p v-html="item.des">
				</p>
				<div v-for="children in item.children">
					<h4>
				{{children.name}}<Button type="primary" shape="circle" icon="chevron-down" style="margin-left: 10px;" @click="columnsMath1view=!columnsMath1view">展开</Button>
				</h4>
					<div span="24" v-show="columnsMath1view">
						<Table border :stripe=true size=small :columns="children.columns" :data="children.data" style="font-size: 16px;"></Table>
					</div>
				</div>
			</div>
		</div>

		<h3>ES6（es2015）</h3>
		<h4>声明变量</h4>
		<div>
			<Poptip placement="right-end">
				<Button type="ghost">let</Button>
				<div slot="title">
					let
				</div>
				<div slot="content">
					let是块级作用域变量，用它所声明的变量，只在let命令所在的代码块内有效。
				</div>
			</Poptip>
			<Poptip placement="right-end">
				<Button type="ghost">const</Button>
				<div slot="title">
					const
				</div>
				<div slot="content">
					当我们尝试去改变用const声明的常量时，浏览器就会报错。<br /> const有一个很好的应用场景，就是当我们引用第三方库的时声明的变量，用const来声明可以避免未来不小心重命名而导致出现bug。
				</div>
			</Poptip>
			<!--
			<Tag checkable color="blue">const</Tag>
			<Tag checkable color="default">class</Tag>
			<Tag checkable color="default">extends</Tag>
			<Tag checkable color="default">super</Tag>
			<Tag checkable color="red">arrow functions</Tag>
			<Tag checkable color="default">template string</Tag>
			<Tag checkable color="default">destructuring</Tag>
			<Tag checkable color="default">default</Tag>
			<Tag checkable color="default">rest arguments</Tag>
			-->
		</div><br />
		<h4>类的概念</h4>
		<div>
			<Poptip placement="right-end">
				<Button type="ghost">class, extends, super</Button>
				<div slot="content">
					<pre>
class Animal {
    constructor(){
        this.type = 'animal'
    }
    says(say){
        console.log(this.type + ' says ' + say)
    }
}

let animal = new Animal()
animal.says('hello') //animal says hello

class Cat extends Animal {
    constructor(){
        super()
        this.type = 'cat'
    }
}

let cat = new Cat()
cat.says('hello') //cat says hello
					</pre>
					<div>
						上面代码首先用class定义了一个“类”，可以看到里面有一个constructor方法，这就是构造方法，而this关键字则代表实例对象。<br />
						简单地说，constructor内定义的方法和属性是实例对象自己的，而constructor外定义的方法和属性则是所有实例对象可以共享的。<br />
						Class之间可以通过extends关键字实现继承，这比ES5的通过修改原型链实现继承，要清晰和方便很多。<br />
						上面定义了一个Cat类，该类通过extends关键字，继承了Animal类的所有属性和方法。<br />
						super关键字，它指代父类的实例（即父类的this对象）。<br />
						子类必须在constructor方法中调用super方法，否则新建实例时会报错。这是因为子类没有自己的this对象，而是继承父类的this对象，然后对其进行加工。如果不调用super方法，子类就得不到this对象。<br />
						ES6的继承机制，实质是先创造父类的实例对象this（所以必须先调用super方法），然后再用子类的构造函数修改this。
					</div>
				</div>
			</Poptip>
		</div>
		<br />
		<h4>箭头函数</h4>
		<div>
			<Poptip placement="right-end">
				<Button type="ghost">arrow function</Button>
				<div slot="title">
					arrow function
				</div>
				<div slot="content">
					<pre>
function(x, y) { 
    x++;
    y--;
    return x + y;
}
(x, y) => {x++; y--; return x+y}
					</pre>
					除了看上去更简洁以外，arrow function还有一项超级无敌的功能！<br />
长期以来，JavaScript语言的this对象一直是一个令人头痛的问题，在对象方法中使用this，必须非常小心。例如：
					<pre>
class Animal {
    constructor(){
        this.type = 'animal'
    }
    says(say){
        setTimeout(function(){
            console.log(this.type + ' says ' + say)
        }, 1000)
    }
}

 var animal = new Animal()
 animal.says('hi')  //undefined says hi
					</pre>
					用箭头函数的写法：
					<pre>
class Animal {
    constructor(){
        this.type = 'animal'
    }
    says(say){
        setTimeout( () => {
            console.log(this.type + ' says ' + say)
        }, 1000)
    }
}
 var animal = new Animal()
 animal.says('hi')  //animal says hi
					</pre>
				</div>
			</Poptip>
		</div>
		<div style="height: 200px;"></div>
	</div>
</template>

<script>
	export default {
		name: 'hello',
		data() {
			return {
				msg: 'Welcome to Your Vue.js App',
				columnsMath1view: true,
				jsdata: [{
					name: "JavaScript 对象",
					des: "",
					children: [{
						name: "JavaScript Array",
						des: "Array 对象<br />Array 对象用于在单个的变量中存储多个值。<br />创建 Array 对象的语法：<br />new Array();<br />new Array(size);<br />new Array(element0, element1, ..., elementn);<br />参数<br />参数 size 是期望的数组元素个数。返回的数组，length 字段将被设为 size 的值。<br />参数 element ..., elementn 是参数列表。当使用这些参数来调用构造函数 Array() 时，新创建的数组的元素就会被初始化为这些值。它的 length 字段也会被设置为参数的个数。<br />返回值<br />返回新创建并被初始化了的数组。<br />如果调用构造函数 Array() 时没有使用参数，那么返回的数组为空，length 字段为 0。<br />当调用构造函数时只传递给它一个数字参数，该构造函数将返回具有指定个数、元素为 undefined 的数组。<br />当其他参数调用 Array() 时，该构造函数将用参数指定的值初始化数组。<br />当把构造函数作为函数调用，不使用 new 运算符时，它的行为与使用 new 运算符调用它时的行为完全一样。",
						children: [{
							name: "Date 对象属性",
							columns: [{
									title: '属性',
									key: 'name'
								},
								{
									title: '描述',
									key: 'des'
								},
								{
									title: '操作',
									key: 'action',
									width: 150,
									align: 'center',
									render: (h, params) => {
										return h('div', [
											h('Button', {
												props: {
													type: 'ghost',
													size: 'small'
												},
												style: {
													marginRight: '5px'
												},
												on: {
													click: () => {
														this.show(params.row.content)
													}
												}
											}, '查看')
										]);
									}
								}
							],
							data: [{
									name: 'constructor',
									des: '返回对创建此对象的数组函数的引用。'
								},
								{
									name: 'length',
									des: '设置或返回数组中元素的数目。'
								},
								{
									name: 'prototype',
									des: '使您有能力向对象添加属性和方法。'
								}
							]
						}, {
							name: "Math 对象方法",
							columns: [{
									title: '属性',
									key: 'name'
								},
								{
									title: '描述',
									key: 'des'
								},
								{
									title: '操作',
									key: 'action',
									width: 150,
									align: 'center',
									render: (h, params) => {
										return h('div', [
											h('Button', {
												props: {
													type: 'ghost',
													size: 'small'
												},
												style: {
													marginRight: '5px'
												},
												on: {
													click: () => {
														this.show(params.row.content)
													}
												}
											}, '查看')
										]);
									}
								}
							],
							data: [{
								name: 'concat()',
								des: '连接两个或更多的数组，并返回结果。'
							}, {
								name: 'join()',
								des: '把数组的所有元素放入一个字符串。元素通过指定的分隔符进行分隔。'
							}, {
								name: 'pop()',
								des: '删除并返回数组的最后一个元素'
							}, {
								name: 'push()',
								des: '向数组的末尾添加一个或更多元素，并返回新的长度。'
							}, {
								name: 'reverse()',
								des: '颠倒数组中元素的顺序。'
							}, {
								name: 'shift()',
								des: '删除并返回数组的第一个元素'
							}, {
								name: 'slice()',
								des: '从某个已有的数组返回选定的元素'
							}, {
								name: 'sort()',
								des: '对数组的元素进行排序'
							}, {
								name: 'splice()',
								des: '删除元素，并向数组添加新元素。'
							}, {
								name: 'toSource()',
								des: '返回该对象的源代码。'
							}, {
								name: 'toString()',
								des: '把数组转换为字符串，并返回结果。'
							}, {
								name: 'toLocaleString()',
								des: '把数组转换为本地数组，并返回结果。'
							}, {
								name: 'unshift()',
								des: '向数组的开头添加一个或更多元素，并返回新的长度。'
							}, {
								name: 'valueOf()',
								des: '返回数组对象的原始值'
							}, ]
						}]
					}, {
						name: "JavaScript Date",
						des: "Date 对象<br />Date 对象用于处理日期和时间。<br />创建 Date 对象的语法：<br />var myDate=new Date()<br />注释：Date 对象会自动把当前日期和时间保存为其初始值。",
						children: [{
							name: "Date 对象属性",
							columns: [{
									title: '属性',
									key: 'name'
								},
								{
									title: '描述',
									key: 'des'
								},
								{
									title: '操作',
									key: 'action',
									width: 150,
									align: 'center',
									render: (h, params) => {
										return h('div', [
											h('Button', {
												props: {
													type: 'ghost',
													size: 'small'
												},
												style: {
													marginRight: '5px'
												},
												on: {
													click: () => {
														this.show(params.row.content)
													}
												}
											}, '查看')
										]);
									}
								}
							],
							data: [{
									name: 'constructor',
									des: '返回对创建此对象的 Date 函数的引用。'
								},
								{
									name: 'prototype',
									des: '使您有能力向对象添加属性和方法。'
								}
							]
						}, {
							name: "Math 对象方法",
							columns: [{
									title: '属性',
									key: 'name'
								},
								{
									title: '描述',
									key: 'des'
								},
								{
									title: '操作',
									key: 'action',
									width: 150,
									align: 'center',
									render: (h, params) => {
										return h('div', [
											h('Button', {
												props: {
													type: 'ghost',
													size: 'small'
												},
												style: {
													marginRight: '5px'
												},
												on: {
													click: () => {
														this.show(params.row.content)
													}
												}
											}, '查看')
										]);
									}
								}
							],
							data: [{
								name: 'Date()',
								des: '返回当日的日期和时间。'
							}, {
								name: 'getDate()',
								des: '从 Date 对象返回一个月中的某一天 (1 ~ 31)。'
							}, {
								name: 'getDay()',
								des: '从 Date 对象返回一周中的某一天 (0 ~ 6)。'
							}, {
								name: 'getMonth()',
								des: '从 Date 对象返回月份 (0 ~ 11)。'
							}, {
								name: 'getFullYear()',
								des: '从 Date 对象以四位数字返回年份。'
							}, {
								name: 'getYear()',
								des: '请使用 getFullYear() 方法代替。'
							}, {
								name: 'getHours()',
								des: '返回 Date 对象的小时 (0 ~ 23)。'
							}, {
								name: 'getMinutes()',
								des: '返回 Date 对象的分钟 (0 ~ 59)。'
							}, {
								name: 'getSeconds()',
								des: '返回 Date 对象的秒数 (0 ~ 59)。'
							}, {
								name: 'getMilliseconds()',
								des: '返回 Date 对象的毫秒(0 ~ 999)。'
							}, {
								name: 'getTime()',
								des: '返回 1970 年 1 月 1 日至今的毫秒数。'
							}, {
								name: 'getTimezoneOffset()',
								des: '返回本地时间与格林威治标准时间 (GMT) 的分钟差。'
							}, {
								name: 'getUTCDate()',
								des: '根据世界时从 Date 对象返回月中的一天 (1 ~ 31)。'
							}, {
								name: 'getUTCDay()',
								des: '根据世界时从 Date 对象返回周中的一天 (0 ~ 6)。'
							}, {
								name: 'getUTCMonth()',
								des: '根据世界时从 Date 对象返回月份 (0 ~ 11)。'
							}, {
								name: 'getUTCFullYear()',
								des: '根据世界时从 Date 对象返回四位数的年份。'
							}, {
								name: 'getUTCHours()',
								des: '根据世界时返回 Date 对象的小时 (0 ~ 23)。'
							}, {
								name: 'getUTCMinutes()',
								des: '根据世界时返回 Date 对象的分钟 (0 ~ 59)。'
							}, {
								name: 'getUTCSeconds()',
								des: '根据世界时返回 Date 对象的秒钟 (0 ~ 59)。'
							}, {
								name: 'getUTCMilliseconds()',
								des: '根据世界时返回 Date 对象的毫秒(0 ~ 999)。'
							}, {
								name: 'parse()',
								des: '返回1970年1月1日午夜到指定日期（字符串）的毫秒数。'
							}, {
								name: 'setDate()',
								des: '设置 Date 对象中月的某一天 (1 ~ 31)。'
							}, {
								name: 'setMonth()',
								des: '设置 Date 对象中月份 (0 ~ 11)。'
							}, {
								name: 'setFullYear()',
								des: '设置 Date 对象中的年份（四位数字）。'
							}, {
								name: 'setYear()',
								des: '请使用 setFullYear() 方法代替。'
							}, {
								name: 'setHours()',
								des: '设置 Date 对象中的小时 (0 ~ 23)。'
							}, {
								name: 'setMinutes()',
								des: '设置 Date 对象中的分钟 (0 ~ 59)。'
							}, {
								name: 'setSeconds()',
								des: '设置 Date 对象中的秒钟 (0 ~ 59)。'
							}, {
								name: 'setMilliseconds()',
								des: '设置 Date 对象中的毫秒 (0 ~ 999)。'
							}, {
								name: 'setTime()',
								des: '以毫秒设置 Date 对象。'
							}, {
								name: 'setUTCDate()',
								des: '根据世界时设置 Date 对象中月份的一天 (1 ~ 31)。'
							}, {
								name: 'setUTCMonth()',
								des: '根据世界时设置 Date 对象中的月份 (0 ~ 11)。'
							}, {
								name: 'setUTCFullYear()',
								des: '根据世界时设置 Date 对象中的年份（四位数字）。'
							}, {
								name: 'setUTCHours()',
								des: '根据世界时设置 Date 对象中的小时 (0 ~ 23)。'
							}, {
								name: 'setUTCMinutes()',
								des: '根据世界时设置 Date 对象中的分钟 (0 ~ 59)。'
							}, {
								name: 'setUTCSeconds()',
								des: '根据世界时设置 Date 对象中的秒钟 (0 ~ 59)。'
							}, {
								name: 'setUTCMilliseconds()',
								des: '根据世界时设置 Date 对象中的毫秒 (0 ~ 999)。'
							}, {
								name: 'toSource()',
								des: '返回该对象的源代码。'
							}, {
								name: 'toString()',
								des: '把 Date 对象转换为字符串。'
							}, {
								name: 'toTimeString()',
								des: '把 Date 对象的时间部分转换为字符串。'
							}, {
								name: 'toDateString()',
								des: '把 Date 对象的日期部分转换为字符串。'
							}, {
								name: 'toGMTString()',
								des: '请使用 toUTCString() 方法代替。'
							}, {
								name: 'toUTCString()',
								des: '根据世界时，把 Date 对象转换为字符串。'
							}, {
								name: 'toLocaleString()',
								des: '根据本地时间格式，把 Date 对象转换为字符串。'
							}, {
								name: 'toLocaleTimeString()',
								des: '根据本地时间格式，把 Date 对象的时间部分转换为字符串。'
							}, {
								name: 'toLocaleDateString()',
								des: '根据本地时间格式，把 Date 对象的日期部分转换为字符串。'
							}, {
								name: 'UTC()',
								des: '根据世界时返回 1970 年 1 月 1 日 到指定日期的毫秒数。'
							}, {
								name: 'valueOf()',
								des: '返回 Date 对象的原始值。'
							}, ]
						}]
					}, {
						name: "JavaScript Math",
						des: "Math 对象用于执行数学任务。<br /><br /> 使用 Math 的属性和方法的语法：<br /> var pi_value=Math.PI;<br /> var sqrt_value=Math.sqrt(15);<br /><br /> 注释：Math 对象并不像 Date 和 String 那样是对象的类，因此没有构造函数 Math()，像 Math.sin() 这样的函数只是函数，不是某个对象的方法。您无需创建它，通过把 Math 作为对象使用就可以调用其所有属性和方法。",
						children: [{
							name: "Math 对象属性",
							columns: [{
									title: '属性',
									key: 'name'
								},
								{
									title: '描述',
									key: 'des'
								},
								{
									title: '操作',
									key: 'action',
									width: 150,
									align: 'center',
									render: (h, params) => {
										return h('div', [
											h('Button', {
												props: {
													type: 'ghost',
													size: 'small'
												},
												style: {
													marginRight: '5px'
												},
												on: {
													click: () => {
														this.show(params.row.content)
													}
												}
											}, '查看')
										]);
									}
								}
							],
							data: [{
									name: 'E',
									des: '返回算术常量 e，即自然对数的底数（约等于2.718）。'
								},
								{
									name: 'LN2',
									des: '返回 2 的自然对数（约等于0.693）。'
								},
								{
									name: 'LN10',
									des: '返回 10 的自然对数（约等于2.302）。'
								},
								{
									name: 'LOG2E',
									des: '返回以 2 为底的 e 的对数（约等于 1.414）。'
								}, {
									name: 'LOG10E',
									des: '返回以 10 为底的 e 的对数（约等于0.434）。'
								},
								{
									name: 'PI',
									des: '返回圆周率（约等于3.14159）。'
								},
								{
									name: 'SQRT1_2',
									des: '返回返回 2 的平方根的倒数（约等于 0.707）。'
								},
								{
									name: 'SQRT2',
									des: '返回 2 的平方根（约等于 1.414）。'
								}
							]
						}, {
							name: "Math 对象方法",
							columns: [{
									title: '属性',
									key: 'name'
								},
								{
									title: '描述',
									key: 'des'
								},
								{
									title: '操作',
									key: 'action',
									width: 150,
									align: 'center',
									render: (h, params) => {
										return h('div', [
											h('Button', {
												props: {
													type: 'ghost',
													size: 'small'
												},
												style: {
													marginRight: '5px'
												},
												on: {
													click: () => {
														this.show(params.row.content)
													}
												}
											}, '查看')
										]);
									}
								}
							],
							data: [{
									name: 'abs(x)',
									des: '返回数的绝对值。'
								},
								{
									name: 'acos(x)',
									des: '返回数的反余弦值。'
								},
								{
									name: 'asin(x)',
									des: '返回数的反正弦值。'
								},
								{
									name: 'atan(x)',
									des: '以介于 -PI/2 与 PI/2 弧度之间的数值来返回 x 的反正切值。'
								}, {
									name: 'atan2(y,x)',
									des: '返回从 x 轴到点 (x,y) 的角度（介于 -PI/2 与 PI/2 弧度之间）。'
								},
								{
									name: 'ceil(x)',
									des: '对数进行上舍入。'
								},
								{
									name: 'cos(x)',
									des: '返回数的余弦。'
								},
								{
									name: 'exp(x)',
									des: '返回 e 的指数。'
								}, {
									name: 'floor(x)	',
									des: '对数进行下舍入。'
								},
								{
									name: 'log(x)',
									des: '返回数的自然对数（底为e）。'
								},
								{
									name: 'max(x,y)',
									des: '返回 x 和 y 中的最高值。'
								},
								{
									name: 'min(x,y)',
									des: '返回 x 和 y 中的最低值。'
								}, {
									name: 'pow(x,y)',
									des: '返回 x 的 y 次幂。'
								},
								{
									name: 'random()',
									des: '返回 0 ~ 1 之间的随机数。',
									content: `定义和用法<br />
						random() 方法可返回介于 0 ~ 1 之间的一个随机数。<br />
						语法<br />
						Math.random()
						`
								},
								{
									name: 'round(x)',
									des: '把数四舍五入为最接近的整数。'
								},
								{
									name: 'sin(x)',
									des: '返回数的正弦。'
								}, {
									name: 'sqrt(x)',
									des: '返回数的平方根。'
								},
								{
									name: 'tan(x)',
									des: '返回角的正切。'
								},
								{
									name: 'toSource()',
									des: '返回该对象的源代码。'
								},
								{
									name: 'valueOf()	',
									des: '返回 Math 对象的原始值。'
								}
							]
						}]
					}]
				}],
			}
		},
		methods: {
			ab() {
				alert("===")
			},
			show(content = '未录入') {
				this.$Modal.info({
					title: '说明',
					width: '1000px',
					content: content
				})
			}
		}
	}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
</style>