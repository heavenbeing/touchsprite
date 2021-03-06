# Lua 基础简明教程

标签（空格分隔）： 脚本开发

---
##目录
[TOC]

##注释
写一个程序，总是少不了注释的。
在Lua中，你可以使用单行注释和多行注释。
单行注释中，连续两个减号"--"表示注释的开始，一直延续到行末为止。相当于C++语言中的"//"。
多行注释中，由"--[["表示注释开始，并且一直延续到"]]"为止。这种注释相当于C语言中的"/**/"。在注释当中，"[["和"]]"是可以嵌套的。

##Lua 编程	
经典的"Hello world"的程序总是被用来开始介绍一种语言。在Lua中，写一个这样的程序很简单：
```lua
print("Hello world")
```
在Lua中，语句之间可以用分号"`；`"隔开，也可以用空白隔开。一般来说，如果多个语句写在同一行的话，建议总是用分号隔开。
Lua 有好几种程序控制语句，如：
**条件控制：** if 条件 then … elseif 条件 then … else … end
**While循环：** while 条件 do … end
**Repeat循环：** repeat … until 条件
**For循环：** for 变量 = 初值，终点值，步进 do … end
**For循环：** for 变量1，变量2，… ，变量N in表或枚举函数 do … end

> 注意一下，for的循环变量总是只作用于for的局部变量，你也可以省略步进值，这时候，for循环会使用1作为步进值。
你可以用break来中止一个循环。

如果你有程序设计的基础，比如你学过Basic，C之类的，你会觉得Lua也不难。但Lua有几个地方是明显不同于这些程序设计语言的，所以请特别注意。

###语句块

语句块在C++中是用"{"和"}"括起来的，在Lua中，它是用do 和 end 括起来的。比如：
```lua
do print("Hello") end
```
你可以在 函数 中和 语句块 中定局部变量。

###赋值语句

赋值语句在Lua被强化了。它可以同时给多个变量赋值。
例如：
```lua
a,b,c,d=1,2,3,4
```
甚至是：
```lua
a,b=b,a -- 多么方便的交换变量功能啊。
```
在默认情况下，变量总是认为是全局的。假如你要定义局部变量，则在第一次赋值的时候，需要用local说明。比如：
```lua
local a,b,c = 1,2,3 -- a,b,c都是局部变量
```

###循环语句

> 1. while 循环：while 条件 do … end
2. repeat 循环：repeat … until 条件
3. for 循环：for 变量 = 初值，终点值，步进 do … end
4. for 循环：for 变量1，变量2，… ，变量N in表或枚举函数 do … end


while 练习
```lua
my_table = {1,2,3}
local index = 1  -- 注意: table 中的索引从1开始

while my_table[index] do   -- 只要条件返回True,就一直执行循环 
print(my_table[index]) 
index = index +1   -- Lua中没有i++ 的写法,所以只能用这种写法
end

-- 输出 1
--      2
--      3
```

repeat 练习(相当于其他语言中的do...while) 
```lua
local snum = 1 --起始值

repeat
print("snum is "..snum)
snum = snum + 1
until snum == 4   --当snum 等于 4 时 跳出循环

--输出:
--snum is 1
--snum is 2
--snum is 3
```

for 循环练习1
```lua
for i = 1, #my_table do --#my_table 表示取表的长度,上边定义了长度为3
print(my_table[i])
end
```

--for 循环练习2
```lua
for i=1,10,2 do -- 这里i=1表示起始值, 10 表示最大值, 2表示步进值(可以没有,默认值为1,也就是其他语言里的i++)
print(i)
end
```

注意一下，for的循环变量总是只作用于for的局部变量，你也可以省略步进值，这时候，for循环会使用 1 作为步进值。
可以用break来中止一个循环。

###数值运算

和C语言一样，支持` +, -, *, /`。但Lua还多了一个"`^`"。这表示指数乘方运算。比如2^3 结果为8, 2^4结果为16。
连接两个字符串，可以用"`..`"运处符。如：
```lua
"This a " .. "string." -- 等于 "this a string"
```
###比较运算
< > <= >= == ~=
分别表示 小于，大于，不大于，不小于，相等，不相等
所有这些操作符总是返回 `true` 或 `false`。
对于Table，Function和Userdata类型的数据，只有 == 和 ~=可以用。相等表示两个变量引用的是同一个数据。比如：
```lua
a={1,2}
b=a
print(a==b, a~=b) -- true, false
a={1,2}
b={1,2}
print(a==b, a~=b) -- false, true
```
###逻辑运算

and, or, not

其中，and 和 or 与C语言区别特别大。
在这里，请先记住，在Lua中，只有 `false` 和 `nil` 才计算为 `false`，其它任何数据都计算为 `true`，`0` 也是 `true`！
`and` 和 `or` 的运算结果不是 true和false，而是和它的两个操作数相关。
**a and b：** 如果a为false，则返回a；否则返回b
**a or b：** 如果 a 为true，则返回a；否则返回b
举几个例子：
```lua
print(4 and 5) --> 5
print(nil and 13) --> nil
print(false and 13) --> false
print(4 or 5) --> 4
print(false or 5) --> 5
```
在Lua中这是很有用的特性，也是比较令人混洧的特性。
我们可以模拟C语言中的语句：
```lua 
x = a? b : c
```
在Lua中，可以写成：
```lua 
x = a and b or c
```
最有用的语句是：
```lua
x = x or v
```
它相当于：
```lua
if not x then x = v end 
```
###运算符优先级
从高到低顺序如下：
```lua
^

not - （一元运算）

* /

+ -

..（字符串连接）

< > <= >= ~= ==

and

or
```
##关键字
关键字是不能做为变量的。Lua的关键字不多，就以下几个：
```lua
and break do else elseif

end false for function if

in local nil not or

repeat return then true until　while
```
##变量类型
怎么确定一个变量是什么类型的呢？大家可以用type()函数来检查。Lua支持的类型有以下几种：
###Nil 空值
所有没有使用过的变量，都是nil。nil既是值，又是类型。

###Boolean 布尔值
true 或 false
###Number 数值
在Lua里，数值相当于C语言的double

###String 字符串
如果你愿意的话，字符串是可以包含'\0'字符的

###Table 关系表类型
这个类型功能比较强大，我们在后面慢慢说。

###Function 函数类型
不要怀疑，函数也是一种类型，也就是说，所有的函数，它本身就是一个变量。

###Userdata
嗯，这个类型专门用来和Lua的宿主打交道的。宿主通常是用C和C++来编写的，在这种情况下，Userdata可以是宿主的任意数据类型，常用的有Struct和指针。

###Thread 线程类型
在Lua中没有真正的线程。Lua中可以将一个函数分成几部份运行。如果感兴趣的话，可以去看看Lua的文档。

##变量的定义
所有的语言，都要用到变量。在Lua中，不管你在什么地方使用变量，都不需要声明，并且所有的这些变量总是全局变量，除非，你在前面加上"`local`"。
这一点要特别注意，因为你可能想在函数里使用局部变量，却忘了用local来说明。
至于变量名字，它是`大小写相关`的。也就是说，A和a是两个不同的变量。
定义一个变量的方法就是赋值。"`＝`"操作就是用来赋值的
我们一起来定义几种常用类型的变量吧。

###Nil
正如前面所说的，没有使用过的变量的值，都是Nil。有时候我们也需要将一个变量清除，这时候，我们可以直接给变量赋以nil值。如：
```lua
var1=nil -- 请注意 nil 一定要小写
```
###Boolean

布尔值通常是用在进行条件判断的时候。
布尔值有两种：true 和 false。在Lua中，只有false和nil才被计算为false，而所有任何其它类型的值，都是true。比如0，空串等等，都是true。不要被C语言的习惯所误导，0在Lua中的的确确是true。你也可以直接给一个变量赋以Boolean类型的值，如：
```lua
　　　　varboolean = true
```
###Number

在Lua中，是没有整数类型的，也不需要。一般情况下，只要数值不是很大（比如不超过100,000,000,000,000），是不会产生舍入误差的。在很多CPU上，实数的运算并不比整数慢。
实数的表示方法，同C语言类似，如：
4 0.4 4.57e-3 0.3e12 5e+20

###String

字符串，总是一种非常常用的高级类型。在Lua中，你可以非常方便的定义很长很长的字符串。
字符串在Lua中有几种方法来表示，最通用的方法，是用双引号或单引号来括起一个字符串的，如：
```lua
"This is a string."
```
和C语言相同的，它支持一些转义字符，列表如下：
```
\a bell

\b back space

\f form feed

\n newline

\r carriage return

\t horizontal tab

\v vertical tab

\\ backslash

\" double quote

\' single quote

\[ left square bracket

\] right square bracket
```
由于这种字符串只能写在一行中，因此，不可避免的要用到转义字符。加入了转义字符的串，看起来实在是不敢恭维，比如：
```lua
　　　　"one line\nnext line\n\"in quotes\", 'in quotes'"
```
一大堆的"\"符号让人看起来很倒胃口。如果你与我有同感，那么，我们在Lua中，可以用另一种表示方法：用"[["和"]]"将多行的字符串括起来，如：
```lua
page = [[
<HTML>
　　　<HEAD>
　　　　　<TITLE>An HTML Page</TITLE>
　　　</HEAD>
　　　<BODY>
　　　　　<A HREF="http://www.lua.org">Lua</A>
　　　　　[[a text between double brackets]]
　　　</BODY>
　</HTML>
  　]]
```
 
值得注意的是，在这种字符串中，如果含有单独使用的"`[[`"或"`]]`"就仍然得用"`\[`"或"`\]`"来避免歧义。当然，这种情况是极少会发生的。

###Table
关系表类型，这是一个很强大的类型。我们可以把这个类型看作是一个数组。只是C语言的数组，只能用正整数来作索引；在Lua中，你可以用任意类型来作数组的索引，除了nil。同样，在C语言中，数组的内容只允许一种类型；在Lua中，你也可以用任意类型的值来作数组的内容，除了nil。

Table的定义很简单，它的主要特征是用"`{`"和"`}`"来括起一系列数据元素的。比如：
```lua
T1 = {} -- 定义一个空表
T1[1]=10 -- 然后我们就可以象C语言一样来使用它了。
T1["John"]={Age=27, Gender="Male"}
```
这一句相当于：
```lua
T1["John"]={} -- 必须先定义成一个表，还记得未定义的变量是nil类型吗
T1["John"]["Age"]=27
T1["John"]["Gender"]="Male"
```
当表的索引是字符串的时候，我们可以简写成：
```lua
T1.John={}
T1.John.Age=27
T1.John.Gender="Male"
```
或
```lua
T1.John{Age=27, Gender="Male"}
```
这是一个很强的特性。
在定义表的时候，我们可以把所有的数据内容一起写在"`{`"和"`}`"之间，这样子是非常方便，而且很好看。比如，前面的T1的定义，我们可以这么写：
```lua
T1=
　　{
	　　　　10, -- 相当于 [1] = 10
	　　　[100] = 40,
	　　　　　　John= -- 如果你原意，你还可以写成：["John"] =
	　　　　　　{
		　　　　　　　　Age=27,   -- 如果你原意，你还可以写成：["Age"] =27
		　　　　　　　　Gender=Male   -- 如果你原意，你还可以写成：["Gender"] =Male
		　　　　　　},
	　　　　　　20 -- 相当于 [2] = 20
	}
```

看起来很漂亮，不是吗？我们在写的时候，需要注意三点：
第一，所有元素之间，总是用逗号"`，`"隔开；
第二，所有索引值都需要用"`[`"和"`]`"括起来；如果是字符串，还可以去掉引号和中括号；
第三，如果不写索引，则索引就会被认为是数字，并按顺序自动从1往后编；
表类型的构造是如此的方便，以致于常常被人用来代替配置文件。是的，不用怀疑，它比ini文件要漂亮，并且强大的多。

###Function
函数，在Lua中，函数的定义也很简单。典型的定义如下：
```lua
function add(a,b) -- add 是函数名字，a和b是参数名字
return a+b -- return 用来返回函数的运行结果
end
```
请注意，return语言一定要写在end之前。假如你非要在中间放上一句return，那么请写成：do return end。
还记得前面说过，函数也是变量类型吗？上面的函数定义，其实相当于：
```lua
add = function (a,b) return a+b end
```
当你重新给add赋值时，它就不再表示这个函数了。你甚至可以赋给add任意数据，包括nil （这样，你就清除了add变量）。Function是不是很象C语言的函数指针呢？
和C语言一样，Lua的函数可以接受可变参数个数，它同样是用"…"来定义的，比如：
```lua
function sum (a,b,…)
```
如果想取得…所代表的参数，可以在函数中访问arg局部变量（表类型）得到。如 
```lua
sum(1,2,3,4)
```
则，在函数中，
```lua
a = 1, b = 2, arg = {3, 4}
```
更可贵的是，它可以同时返回多个结果，比如：
```lua
function s()
　　return 1,2,3,4
end
a,b,c,d = s() -- 此时，a = 1, b = 2, c = 3, d = 4
```
前面说过，表类型可以拥有任意类型的值，包括函数！因此，有一个很强大的特性是，拥有函数的表，哦，我想更恰当的应该说是对象吧。Lua可以使用面向对象编程了。不信？那我举例如下：
```lua
　　　　t =
　　　　{
　　　　 Age = 27
　　　　 add = function(self, n) self.Age = self.Age+n end
　　　　}
　　　　print(t.Age) -- 27
　　　　t.add(t, 10)
　　　　print(t.Age) -- 37
```
不过，t.add(t,10) 这一句实在是有点土对吧？没关系，在Lua中，你可以简写成：
```lua
t:add(10)   -- 相当于 t.add(t,10)
```
**注意事项**
用触动精灵开发脚本时，一定要记得把封装函数写在调用前面，因为脚本是按照从上往下的顺序执行的，如果先调用而没有封装，就会报错。

