# JavaScript

声明变量的三种:

1. var   声明出的是全局变量//一般不用
2. let    声明普通的可变变量//最常用
3. const  同c声明不可变变量//好习惯

注意JavaScript里的数据类型是由数据本身决定的,

比如let name="sss"   这里生成了一个String  而我没有主动输入String,都是由语言决定的.

### 所有类型

**值类型**:String    number    boolean     Null     Undefined     Symbol

**引用类型(对象类型)**:Object    Array   Function     两个特殊对象:正则 RegExp  日期Date 

其中

number包括了浮点数和整数

当声明了一个变量却没有赋值,类型就是Undefine



### 字典

类似python:

let  John{

​	age:19,

​	address:{   //可以嵌套

​			street:67,

​			city:Guangdong

​		}

}

JavaScript里甚至可以这样直接添加属性:

John.weight='160';

### 解构

将一个字典里的值按解构赋值,例如上面的John,想全部提取出来,可以:

const { age,address:{street , city}} =John

现在左边所有声明的变量全部可以单独使用了

### 解构后重命名

dict 是一个字典{ number : 10 }

const {number} = dict  //number为10

const {number : a}=dict  //a为10  这里将number重命名为10

### 数组

const  a =new Array(3,4,7,5,3);    //const对Array而言并无影响,仍然可以对值进行修改,因为const类型的数据也能修改其属性,但  a=[3,5,2];这样就不行了

如果只传递一个数字:

const a=new Array(2);

代表数组a的大小为2



JSON

没有单引号,必须使用双引号,其他的和JS一致

JSON.stringify (John)  这个就是转换成json格式的一个方法

### 循环

与c,java一致

特别的方法:

let a =[2,4,5,7];

for(let numbers of a){

​	numbers......

}

### 回调函数

一个函数作为其他函数的参数



Array 的foreach方法:

Array.foreach( ( element,index,array )=>{  xxx  })    箭头函数

//这里传入的三个参数是数组的元素,下标,数组本身,这是foreach给它分配的,不是没有意义的名字



也可以改成Array.foreach( function( element,index,array) { } )和箭头函数差不多



### lambda函数JavaScript版(箭头函数)

在python中是用来简化简单代码的

1. lambda x: (x+3)*6    常用,一个加减乘除函数

2. lambda x: x+=5 if x==2 else 3   加上条件判断,这里else 3代表如果x不是2那就返回3

   与一些参数就是函数的函数配合比较好,这里有两个:

3. map( function , list ) :以前面function为规则,从原来的list映射一个新的list( python3返回的是一个迭代器,所以用list()函数重新整理)

   list(map( lambda x:x**2, [ 4,6,8,3,2 ] ) )生成 [ 16,36,64,9,4 ]

4. filter( function , list ): function是判断函数,应当返回True或False,对每个list中的数判断一遍,True就留下,False就走,返回list(不是迭代器)

   filter( lambda x: True if x % 2==0 else False, [ 3,4,5,7,9 ])    返回[4]

在JavaScript中是这样的:(更不简洁,更通用)

const addNums = (x=3 ,y=5) =>x+y   (等于代表初始值,,和python一样)

即:

const function =( 参数 ) => 要return的东西

当然也可以真的像函数一样(用大括号了就相当于函数了):

const function = ( x, y ) =>{

​			if( x>3 && y>4){

​				return x+y;

​		}

​	}

###  类

function People( name ,address){

​		this.name=name;

​		this.address=address;

​		this. func= function( ){  };

}

p1=new People( John, Paris);

几乎就是Java里把class换成function

People.prototype.func2=function( ){   }  //prototype可以在类外面给类添加函数



新版本添加了class,可以用class了,唯一的区别是构造函数:

constructor( name , address){

​	this.name=name;.....

}建议用这个

### es6数组拼接

[ ...  数组   ,  ...  另一个数组 ]  





undefined: 空缺,更严重

null: 自己加的,或可预测的,合理的空



大括号是定义对象:

var apple = {

​	color: green

}

访问时可以apple.color   

甚至可以 apple["color"] ( 或者其他代表字符串的变量 )

可以用变量动态地访问属性
