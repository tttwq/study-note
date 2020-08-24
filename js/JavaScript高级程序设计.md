# 在HTML中使用JavaScript

### &lt;script&gt;元素

6个属性：

> 1. `async`：可选。异步执行，仅适用于外部脚本（只有在使用src属性时使用）;
>
> > `async=‘async’`：脚本相对于页面其余部分异步执行，当页面继续进行解析时，脚本将被执行
>
> 2. `defer`：可选。仅适用于外部脚本（只有在使用src属性时使用）；
>
> > `defer=‘defer’`：脚本将在页面完成解析后执行
>
> 3. `charset`：可选。通过src属性指定的代码的字符集；
>
> 4. `language`：已废弃；
>
> 5. `src`：可选。包含要执行代码的外部文件；
>
> 6. `type`：必选。编写代码时使用的脚本语言的内容类型（MIME类型）-- text/javascript

 &lt;noscript&gt;元素

​      不支持脚本时显示替代内容；

# 基本概念

## 语法

1. 区分大小写 -- 变量、函数名、操作符；

2. 标识符规则：

   >  第一个字符必须是一个字母、下划线（_）、或美元符号（$）；
   >
   > 其他字符可以是字母、下划线、数字或美元符号；

3. 严格模式 --     ` "use strict"`（顶部或函数内部上方）；

4. 关键字

   | break    | do       | instanceof | typeof |
   | -------- | -------- | ---------- | ------ |
   | case     | else     | new        | var    |
   | catch    | finally  | return     | void   |
   | continue | for      | switch     | while  |
   | debugger | function | this       | with   |
   | default  | if       | throw      |        |
   | delete   | in       | try        |        |

5. 保留字

   | abstract | enum       | int       | short        |
   | -------- | ---------- | --------- | ------------ |
   | boolean  | export     | interface | static       |
   | byte     | extends    | long      | super        |
   | char     | final      | native    | synchronized |
   | class    | float      | package   | throws       |
   | const    | goto       | private   | transient    |
   | debugger | implements | protected | volatile     |
   | double   | import     | public    | let          |
   | yield    |            |           |              |

## 变量

1. 定义变量 ： `var`操作符；
2. `var`操作符定义的变量为该变量作用域中的局部变量。如果在函数中使用`var`定义变量，退出后会被销毁；省略`var`操作符则为全局变量（不推荐，在严格模式下抛出ReferenceError错误）；
3. 可以使用一条语句可以定义多个不同类型的变量（用逗号隔开）；

## 数据类型

1. 5种基本类型：Undefined, Null,     Boolean, Number, String；

2. 1种复杂类型：Object；

3. `typeof`操作符：

   >  检测数据类型，返回字符串；是一个操作符而非函数；
   >
   > “undefined”-- 未定义
   >
   > “boolean” -- 布尔值
   >
   > “string” -- 字符串
   >
   > “number” -- 数值
   >
   > “object” -- 对象或null
   >
   > “function” -- 函数

### Undefined

1. 在用`var`声明变量但未对其初始化，值为undefined；
2. 包含undefined值的变量（可以使用操作符）与未声明的变量（只能执行一项操作，使用`typeof`操作符）；
3. 对未初始化和未声明的变量执行`typeof`操作符，都返回undefined值；

### Null

1. 空指针对象，值为null，`typeof`返回object；
2. 如果定义的变量准备用于保存对象，最好初始化为null，便于后续采用检查其值是否为null来判断是否已保存对象；
3. undefined派生于null ( null == undefined //true)

### Boolean

1. 值为true和false（区分大小写）；

2. `Boolean()`：转型函数，将其他类型的值转换为布尔值；

3. 转换规则：

   | 数据类型  | 转换为true的值               | 转换为false的值 |
   | --------- | ---------------------------- | --------------- |
   | Boolean   | true                         | false           |
   | String    | 任何非空字符串               | ""（空字符串）  |
   | Number    | 任何非零数字值（包括无穷大） | 0和NaN          |
   | Object    | 任何对象                     | null            |
   | Undefined | 不适用                       | undefined       |

### Number

1. 十进制：直接输入；  八进制：第一位为0（严格模式下无效）； 十六进制：前两位为0x；

2. 进行算术计算时，最终转换为十进制；

3. 浮点数：

   > 小数点后没有数或值为整数会被自动转换为整数，小数点后带有6个零以上的浮点数将转换为e表示法；
   >
   > 浮点数最高精度是17位小数；
   >
   > 存在舍入误差，如 0.1+0.2结果不为0.3

4. 数值范围：`Number.MIN_VALUE=5e-324`     ；      `Number.MAX_VALUE=1.7976931348623157e+308`；

5. 正无穷：`Infinity `； 负无穷：`-Infinity `   ；  

6.  `isFinity()`：确定一个数是不是有穷的；

7. `NaN`：涉及`NaN`的任何操作都返回`NaN`，且与任何值都不相等，包括`NaN`本身  

8. `isNaN()`：确定一个变量值是否为`NAN`；

9. 数值转换：

   + `Number()`—— 任何类型：

     >  Boolean：true和false分别转换为1和0；
     >
     > 数字：简单传入和返回；
     >
     > null：0；
     >
     > undefined：`NaN`；
     >
     > 字符串：只包含数字 -- 十进制，十六进制格式 -- 转换为十进制，空字符串 -- 0，其他 -- `NaN`；
     >
     > Object：调用`valueOf()`转换，调用`toString()`转换；

   + `parseInt()`，`parseFloat()`——字符串:

     > 空字符串返回`NaN`；
     >
     > 识别八进制、十六进制；
     >
     > 可以传入第二个参数确定进制；

### String

1. 转义字符：

| \n     | 换行                                    |
| ------ | --------------------------------------- |
| \t     | 制表                                    |
| \b     | 退格                                    |
| \r     | 回车                                    |
| \f     | 进纸                                    |
| \\     | 斜杠                                    |
| \'     | 单引号                                  |
| \"     | 双引号                                  |
| \xnn   | 以十六进制代码nn表示的一个字符          |
| \unnnn | 以十六进制代码nnnn表示的一个Unicode字符 |

2. `length`属性获取字符串长度；

3. 字符串一旦创建值不可变。

   > 改变值：创建新字符串填入新值，销毁旧字符串;

4. 字符串转换：

1. + `toString()`：

     > null和undefined没有这个方法；
     >
     >  调用数值的`toString()`时可以传入基数确定进制，默认十进制；

   + `String()`：函数，可以转换undefined和null

### Object

1. 通过new操作符创建；

2. 每个Object实例都具有下列属性和方法：

3. - ` constructor`：保存创建当前对象的函数（构造函数）；
   -  `hasOwnProperty(propertyName)`：检查当前实例中是否存在某个属性；
   - `isPrototypeOf(object)`：检查传入对象是否为当前对象原形；
   - `propertyIsEnumerable(propertyName)`：检查给定属性能否用`for-in`枚举；
   - `toLocaleString()`：返回对象的字符串表示，与执行环境的地区相对应；
   - ` toString()`：返回对象的字符串表示；
   -  `valueOf()`：返回对象的字符串、数值、布尔值表示；

## 操作符

### 一元操作符

1.  只操作一个值；
2.  递增（++）和递减（--）：前置性（先于求值），后置型（后于求值）；与执行语句优先级相等；
3. 一元加（+）和减（-）：非数值应用，类似`Number()`；

### 位操作符

1.  `NaN`和`Infinity`被当成0处理；
2.  对于非数值，先执行`Number()`；
3.  按位非（~）、按位与（&）、按位或（|）、按位异或（^）；
4.  左移（<<）：右侧以0填充，不影响符号位；
5.  右移：有符号的右移（>>）、无符号的右移（>>>）-- 会把负数的二进制当成正数的二进制；

### 布尔操作符

1.  逻辑非（!）：两个逻辑非操作符 ==`Boolean()`;
2.  逻辑与（&&）：返回值不一定是布尔值，短路操作，若第一个值能决定结果，不再执行第二个操作数求值；
3.  逻辑或（||）：返回值不一定是布尔值，和逻辑与类似；

### 乘性操作符

1. 乘法（&times;）：`Infinity*0 == NaN`;
2. 除法（/）：`Infinity / Infinity == NaN` ， `0 / 0 == NaN`;
3. 求模（%）：`Infinity % Finity == NaN` ， `Infinity % Infinity == NaN` ， `Finity % 0 == NaN`；

### 加性操作符

1. 加法（+）：

   > `-Infinity+Infinity == NaN`；
   >
   > 存在一个字符串 -- 拼接，另一个操作数`toString`；

2. 减法（-）；

### 关系操作符

小于（<）、大于（>）、小于等于（<=）、大于等于（>=）

### 相等操作符

1. 相等（==）和不相等（!=）：

   > 先转换后比较；
   >
   > null和undefined相等，比较前null和undefined不转换为其它值，`null != 0`,`undefined != 0`；
   >
   > NaN和其它不相等（包括NaN）；
   >
   > 两个Object比较其是不是指向同一个对象；

2. 全等（===）和不全等（!==）：

   > 仅比较不转换；
   >
   > `null !== undefined`；

###  条件操作符：（？：）

###  赋值操作符

复合赋值（*=、/=、%=、+=、-=、<<=、>>=、>>>=）；

###  逗号操作符：

一条语句执行多个操作 -- 声明多个变量、赋值；

## 语句

1. if语句；
2. do-while语句；
3. while语句；
4. for语句；
5. for-in语句：使用前先确认对象是否为null或undefined；
6. label语句 ：`label：statement`；
7. break和continue语句；
8. with语句：`with(expression) statement`，严格模式下会视为语法错误；
9. switch语句：比较时使用全等操作符；

## 函数

1. return语句之后停止并立即退出，return之后不带返回值返回undefined；
2. 函数参数的个数和数据类型不限定；
3. 函数的参数在内部用一个数组表示，函数体内可以通过arguments对象来访问参数数组；
4. arguments对象与数组类似，但并不是Array的实例。可以用方括号语法访问元素，也可以用length确定长度；
5. 命名的参数只提供便利，不是必须；
6. arguments的值与对应命名参数的值同步，但内存空间独立，严格模式下，重写arguments的值会导致语法错误；
7. 没有传递值得命名参数将被赋予undefined值；
8. 函数没有重载；

# 变量、作用域和内存问题

## 基本类型和引用类型

1. 基本类型按值访问，操作变量中的值；引用类型值为保存在内存中的对象，操作对象的引用；
2. 引用类型的值可以添加、改变、删除其属性和方法；
3. 复制变量值：

| 基本类型                                                     | 引用类型                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 创建一个新变量并赋值到该变量；  两个变量任何操作不互相影响； | 创建一个新变量，并将变量对象的指针复制到新变量分配的空间中；  改变其中一个变量，影响另一个变量； |

4. 函数参数按值传递，把外部的值复制给函数内部参数，基本类型和引用类型区分；

5. 检测引用类型 --` instanceof`

   > `variable instanceof constructor`； 
   >
   > 检测基本类型会返回false；

## 执行环境及作用域

1. 每个执行环境都有一个与之关联的变量对象，用于保存定义的函数和变量；

2. 作用域链 -- 执行代码的一条索引路径 当前执行代码所在环境的变量对象 -->全局执行环境的变量对象；

3. 延长作用域链

   > + try-catch语句的catch块 -- 被抛出的错误对象的声明；
   >
   > + with语句；

4. 没有块级作用域；
5. var声明的变量会被添加到最接近的环境中，不声明直接初始化的变量会被添加到全局变量中；

## 垃圾收集

1. 标记清除 -- 给内存中所有变量加上标记，去掉环境中变量和被引用变量的标记，其余准备删除（常用策略）；
2. 引用计数 -- 循环引用(对象A包含指向对象B的指针，对象B包含对象A的指针） -->内存泄露；
3. 对全局变量解除引用优化内存占用 --设置值为null；

# 引用类型

### Object类型

1. 创建Object实例：
   + `new Object() `；
   + 对象字面量；
2. 访问对象属性：
   + 点表示法；
   + 方括号表示法 -- 属性以字符串形式，可以是变量；

### Array类型

1. 创建数组：

   + `new Array()` -- 可以传入length的值或包含项，可以省略new；
   + 数组字面量；

2. 数组的`length`值可读可写；

3. 检测数组：

   + `value instanceof Array`；
   + `Array.isArray(value)`;

4. 转换方法：

   + `toLocaleString()`、`toString()`、`valueOf()`方法 -- 以逗号分隔的字符串；
   + `join()`方法 -- 不同分隔符构建字符串，传入分隔符（字符串形式，默认逗号）；

5. 栈方法（先进后出） -- `push()` -->返回数组长度，`pop()` -->返回移除的值；

6. 队列方法（先进先出） -- `push()`，`shift()` --＞移除第一项并返回移除项；

   + `unshift()`，在数组前端添加任意项并返回数组长度；

7. 重排序方法

   + `reserve()` -- 反转数组项顺序；

   + `sort()` -- 转为字符串进行比较，默认升序，传入比较函数；

     > 比较函数接收两个参数，返回-1时两个参数不交换位置，返回1时两个参数交换；
     >
     > 升序：
     >
     > ```javascript
     > function compare(value1,value2){
     > 	if(value1 < value2){
     > 		return -1;
     > 	}else if(value1 > value2){
     > 		return 1;
     > 	}else{
     > 		return 0
     > 	}
     > }
     > ```
     >
     > ```javascript
     > function compare(value1,value2){
     > 	return value1 - value2
     > }
     > ```

8. 操作方法

   + `concat()`：创建当前数组副本，将传入参数添加至新数组末尾，返回新数组；

   + `slice()`：基于当前数组创建新数组，传入数组起止位置，返回新数组，新数组不包含结束位置；

     >  只传入一个数，则新数组为指定位置到数组末尾；
     >
     > 传入负数，则用数组长度加该数确定相应位置；

   + `splice()`：返回从原始数组删除的项；

     > 删除 -- 2个参数，起始位置+删除项数；
     >
     > 插入 -- 3个参数，起始位置、0、要插入的项；
     >
     > 替换 -- 3个参数，起始位置、删除项数、要插入的项；

9. 位置方法

   + `indexOf()`、`lastIndexOf()`：

     >  2个参数，要查找的项、查找起点（可选）；
     >
     > 返回查找的项在数组中的位置，找不到返回-1；
     >
     > 全等查找；

10. 迭代方法

    + `every()`：对数组中的每一项运行给定函数，如果该函数都返回true，则返回true；

      ```javascript
      arr.every(function(item,index,arrey){})；
      ```

    + `some()`：对数组中的每一项运行给定函数，如果该函数任一项返回true，则返回true；

      ```javascript
      arr.some(function(item,index,arrey){})；
      ```

    + `filter()`：对数组中的每一项运行给定函数，返回该函数返回true的项组成的数组；

      ```javascript
      arr.filter(function(item,index,arrey){})；
      ```

    + `forEach()`：对数组中的每一项运行给定函数，没有返回值；

      ```javascript
      arr.forEach(function(item,index,arrey){})；
      ```

    + `map()`：对数组中的每一项运行给定函数，返回每次函数调用的结果组成的数组；

      ```javascript
      arr.map(function(item,index,arrey){})；
      ```

11. 归并方法

    + `reduce()`、`reduceRight()`：

      > 2个参数，在每个项上调用的函数、作为归并基础的初始值（可选）；
      >
      > 传入函数：4个参数，前一个值、当前值、项的索引、数组对象；
      >
      > 函数返回值会自动作为下一项的第一个参数；
      >
      > ```javascript
      > arr.reduce(function(prev,cur,index,arrey){})          
      > ```

### Date类型

1. 1970年1月1日0时开始经过的毫秒数保存时间；

2. `new Date()`创建日期对象，可直接传入表示日期的字符串；

3. `Date.parse()`：返回相应日期的毫秒数；

4. `Date.UTC()`：返回相应日期毫秒数，月份基于0；

5. `Date.now()`：

6. - 返回调用这个方法的日期和时间毫秒数；
   - 在不支持的浏览器中，可以使用+new Date()获得同样效果；

7. 日期格式化：`toDateString()`、`toTimeString()`、`toLocaleDateString()`、`toLocaleTimeString()`、`toUTCString()`；

8. 日期时间方法：

| getTime()                              | 返回日期毫秒数                    |
| -------------------------------------- | --------------------------------- |
| setTime()                              | 以毫秒数设置日期                  |
| getFullYear()/getUTCFullYear()         | 返回4位数年份                     |
| setFullYear()/setUTCFullYear()         | 设置4位数年份                     |
| getMonth()/getUTCMonth()               | 返回日期中的月份                  |
| setMonth()/setUTCMonth()               | 设置日期中的月份                  |
| getDate()/getUTCDate()                 | 返回日期中的天数，1-31            |
| setDate()/setUTCDate()                 | 设置日期中的天数                  |
| getDay()/getUTCDay()                   | 返回星期，0-6                     |
| getHours()/getUTCHours()               | 返回小时数，0-23                  |
| setHours()/setUTCHours()               | 设置小时数                        |
| getMinutes()/getUTCMinutes()           | 返回分钟数，0-59                  |
| setMinutes()/setUTCMinutes()           | 设置分钟数                        |
| getSeconds()/getUTCSeconds()           | 返回秒数，0-59                    |
| setSeconds()/setUTCSeconds()           | 设置秒数                          |
| getMilliSeconds()/getUTCMilliSeconds() | 返回毫秒数                        |
| setMilliSeconds()/setUTCMilliSeconds() | 设置毫秒数                        |
| getTimezoneOffset()                    | 返回本地时间与UTC时间之间的分钟数 |

### RegExp类型

1. 创建正则表达式：

   + 字面量方法：`var expression = /pattern / flags`;

   + 构造函数方法：`var expression = new RegExp("pattern" , "flags")`

     > `pattern`：字符类、限定符、分组、向前查找、反向引用；
     >
     > `flags`：g--全局 ，i--不区分大小写 ， m--多行；

   + 在ECMAScript 3 中，字面量方法共享一个RegExp实例，而构造函数方法每次新建一个实例；

2. 元字符： (   [       {   \   ^       $   |   )       ?   *   +       .   ]   }；

   | \d    | 匹配0-9的数字，相当于[0-9]                     | \D     | 匹配除了0-9的数字                |
   | ----- | ---------------------------------------------- | ------ | -------------------------------- |
   | \w    | 匹配字母、数字、下划线的字符串                 | \W     | 匹配不是字母、数字、下划线的字符 |
   | \s    | 匹配任意不可见字符，包括空格、制表符、换行符等 | \S     | 匹配任意可见字符                 |
   | \b    | 匹配单词的边界                                 |        |                                  |
   | \t    | 匹配制表符                                     |        |                                  |
   | \n    | 匹配换行                                       | .      | 匹配除换行符以外的所有字符       |
   | ^     | 匹配字符串的开始位置                           |        |                                  |
   | $     | 匹配字符串的结束位置                           |        |                                  |
   | \     | 转义字符                                       |        |                                  |
   | +     | 重复1次或多次，相当于{1,}                      |        |                                  |
   | ?     | 重复0次或1次，相当于{0,1}                      |        |                                  |
   | *     | 重复任意次，相当于{0,}                         |        |                                  |
   | {n}   | 重复n次                                        | {n,m}  | 重复n到m次                       |
   | x\|y  | x或者y                                         |        |                                  |
   | [xyz] | xyz中任意一个                                  | [^xyz] | 除了xyz中任意一个                |
   | [a-z] | a-z中任意一个                                  |        |                                  |
   | ()    | 将括号里的字符作为整体                         |        |                                  |

3. RegExp实例属性：

   + `global`：返回布尔值，是否设置g标志；
   + `ignoreCase`：返回布尔值，是否设置i标志；
   + `lastIndex`：返回整数，开始搜索下一个匹配项的字符位置；
   + `multiline`：返回布尔值，是否设置了m标志；
   + `source`：返回正则表达式的字符串表示（字面量形式）；

4. RegExp实例方法：

   + `exec()`：

     >  返回包含第一个匹配项信息的数组，在没有匹配项的情况下返回null，每次返回一个匹配项；
     >
     > pattern不设置全局模式，则始终返回第一个匹配项信息
     >
     > 返回数组第一项为与整个模式匹配的字符串，其他项是与模式的捕获组匹配的字符串
     >
     > 返回数组额外包含`index`属性和`input`属性；
     >
     > >  `index`：匹配项在字符串中的位置；
     >
     > > ` input`：应用正则表达式的字符串；

   + `test()`：返回布尔值，判断参数与模式是否匹配；

   + `toString() `, `toLocaleString()`：返回正则表达式的字面量；

5. RegExp构造函数属性

6. 局限性

   + 不支持向后查找；
   + 不支持并集和交集类；
   + 不支持原子组；
   + 不支持条件匹配；
   + 不支持正则表达式注释；
   + ……

### Function类型

1. 没有函数重载；
2. 解析器加载数据时，率先读取函数声明；而对于函数表达式，必须等到执行到它所在的代码行才会解释执行；
3. 内部对象：
   + `arguments`：类数组对象，保存函数参数；
   + `this`：引用函数执行的环境对象；
   + `callee`属性：指向拥有这个arguments对象的函数（严格模式下会导致错误）；
   + `caller`属性：指向调用当前函数的函数（严格模式下导致错误）；

4. 函数的属性和方法
   + `length`：函数希望接收的命名参数的个数；
   + `prototype`：不可枚举，不能用for-in实现（具体可见第6章）；
   + `apply()`：设置函数体内this对象的值，扩充函数作用域，传入this值，参数数组；
   + `call()`：设置函数体内this对象的值，扩充函数作用域，传入this值，其余参数；
   + `bind()`：创建一个函数实例，且该实例的this绑定传入bind()的值；
   + `toString()`、`toLocaleString()`、`valueOf()`；

### 基本包装对象

1. Boolean、Number、String，后台创建基本包装类型的对象：创建实例->调用方法->销毁实例；
2. 基本包装类型的实例调用typeof时返回Object，基本包装类型的对象转换为布尔值时为true；
3. Boolean
   + `var booleanObject = new Boolean(true)`;

4. Number
   + `var numberObject = new Number(1)`;
   + `toFixed()`：按照指定的小数位返回数值的字符串表示；
   + `toExponential()`：按照指定的小数位返回数值指数形式的字符串表示；
   + `toPrecision()`：按照指定位数返回数值的字符串表示；

5. String
   + `length`：返回字符串中的字符数；
   + `charAt()`、`charCodeAt()`：传入字符位置，返回字符串中特定字符，`charCodeAt()`以字符编码形式返回；
   + `stringValue[]`：返回字符串中特定字符；
   + `concat()`：拼接字符串，返回拼接后的新字符串；
   + `slice()`：传入开始-结束（不包含）位置，返回截取字符串，遇到负数时参数加字符串长度；
   + `substr()`：传入开始位置，截取长度，返回截取字符串，第一个参数负数加字符串长度，第二个参数转换为0；
   + `substring()`：传入开始-结束（不包含）位置，返回截取字符串，遇到负数时转换为0；
   + `indexOf()`、`lastIndexOf()`：传入字符串、开始搜索位置（可选），查找给定字符串并返回位置，若没找到，返回-1；
   + `trim()`：创建字符串副本，删除字符串前后空格；
   + `toUpperCase()`、`toLocaleUpperCase()`、`toLowerCase()`、`toLocaleLowerCase()`：大小写转换；
   + `match()`：`string.match(pattern)`，字符串匹配模式，返回数组，与`exec()`相似；
   + `search()`：`string.search(pattern)`，返回字符串第一个匹配项的索引；
   + `replace()`：传入RegExp对象，字符串或函数，返回被替换的字符串；
   + `split()`：分割字符串并放入数组中；
   + `localeCompare()`：比较两个字符串（在字母表中的位置）；
   + `formCharCode()`：接收字符编码，返回字符串；

### 单体内置类型

1. Global对象

2. Window对象

3. Math对象

   + `min()`和`max()`方法；

   + 舍入方法：`Math.ceil()` , `Math.floor()` ,` Math.round()`；

   + `Math.random()`：返回0~1的随机数；

   + 其他方法：

     | Math.abs(num)         | 返回num的绝对值     | Math.asin(x)    | 返回x的反正弦值   |
     | --------------------- | ------------------- | --------------- | ----------------- |
     | Math.exp(num)         | 返回Math.E的num次幂 | Math.atan(x)    | 返回x的反正切值   |
     | Math.log(num)         | 返回num的自然对数   | Math.atan2(y,x) | 返回y/x的反正切值 |
     | Math.power(num,power) | 返回num的power次幂  | Math.sin(x)     | 返回x的正弦值     |
     | Math.sqrt(num)        | 返回num的平方根     | Math.cos(x)     | 返回x的余弦值     |
     | Math.acos(x)          | 返回x的反余弦值     | Math.tan(x)     | 返回x的正切值     |

# 面向对象的程序设计

## 理解对象

1. 数据属性：

   + 4个特性：

     >  [[Configurable]]：能否通过delete删除属性从而重新定义属性；
     >
     > [[Enumerable]]：能否通过for-in循环返回属性；
     >
     > [[Writable]]：能否修改属性的值；
     >
     > [[Value]]：这个属性的数据值；

2. 访问器属性

   + 4个特性

     >  [[Configurable]]：能否通过delete删除属性从而重新定义属性；
     >
     > [[Enumerable]]：能否通过for-in循环返回属性；
     >
     > [[Get]]：在读取属性时调用的函数；
     >
     > [[Set]]：在写入属性时调用的函数；

3. `Object.defineProperty()`：修改属性特性，传入属性所在的对象、属性的名字、一个描述符对象；
4. 可以多次调用`Object.defineProperty()`设置同一属性，但把`Configurable`设置为false之后就会有限制了；
5. `Object.defineProperties()`：定义多个属性，传入属性所在的对象、与第一个对象要添加或修改的属性一一对应的对象；
6. `Object.getOwnPropertyDescriptor()`：获取给定属性的描述符，传入属性所在的对象、描述符的属性名称；

## 创建对象

1. 工厂模式

   ```javascript
   function createPerson(name, age, job){
   	var o = new Object();
   	o.name = name;
   	o.age = age;
   	o.job = job;
   	return o;
   }
   var person1 = createPerson("Greg", 27, "doctor");
   ```

2. 构造函数模式

   ```javascript
   function Person(name, age, job){
   	this.name = name;
   	this.age = age;
   
   	this.job = job;
   }
   var person1 = new Person("Greg", 27, "doctor");
   ```

   + 步骤：
     1. 创建一个新对象；
     2. 构造函数的作用域赋给新对象（this指向新对象）；
     3. 执行构造函数的代码；
     4. 返回新对象；
   + 构造函数中的方法要在每个实例上重新创建一遍，即不同实例上的同名函数是不相等的；

3. 原型模式

- ```javascript
  function Person(){
  }
  Person.prototype.name = "Greg";
  Person.prototype.age = 27;
  Person.prototype.job = "doctor";
  Person.prototype.sayName = function(){
  	alert(this.name)
  }
  var person1 = new Person();
  ```

- - 原型对象

    > 每个函数都有一个`prototype`属性，该属性是一个指针，指向一个原型对象；
    >
    > 所有原型对象都会自动获得一个`constructor`属性，指向`prototype`属性所在函数；
    >
    > 调用构造函数创建实例，实例内部有一个[[prototype]]属性（`__proto__`），指向构造函数的原型对象；
    >
    > [[prototype]]为隐式属性；
    >
    > `isPrototypeOf() `--`Person.prototype.isPrototypeOf(person1)`    //true；
    >
    > `Object.getPrototypeOf()` --`Object.getPrototypeOf(person1) == Person.prototype`    //true；
    >
    > `hasOwnProperty()`：确定属性是否存在于实例中；
    >
    > `hasPrototypeProperty()`：确定属性是否存在于原型中；

  - 原型与in操作符

    > `in`操作符：通过对象能够访问到属性时返回true；
    >
    > `Object.keys()`：返回包含所有可枚举属性的字符串数组；
    >
    > `Object.getOwnPropertyNames()`：返回对象中所有实例属性；

## 继承

1. 原型链
   + `instance.__proto__   `  --> `Function.prototype`，当原型对象等于另一个类型的实例时，原型对象包含指向另一个类型原型对象的指针；

2. 借用构造函数 -- 通过使用`call()`和`apply()`方法；

3. 组合继承 --原型链实现对原型属性和方法的继承，构造函数实现对实例属性的继承；

4. 原型式继承；
5. 寄生式继承；
6. 寄生组合式继承；

# 函数表达式

## 递归

一个函数通过名字调用自身；

```javascript
function factorial (num){
	if (num <=1){
		return 1
	}else{
		return num * factorial(num-1)
	}
}
```

使用`auguments.callee`代替函数名；

## 闭包

## 模仿块级作用域

## 私有变量



