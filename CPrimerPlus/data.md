# 数据

常量和变量

基本数据类型：
* 整型
* 浮点型


数据类型关键字

|最初|c90标准新增|C99标准新增|
|---------|---------|---------|
|int|signed|_Bool|
|long|void|_Complex|
|short||_Imaginary|
|unsigned|||
|char|||
|float|||
|double|||

位bit    字节byte=8bit(存储大小的B)    字word

整数的存储 二进制

浮点数的存储 转成二进制小数，分开存储小数和指数部分

>IEEE浮点数标准  
>二进制浮点数 V = (-1)^s * 2M * 3^E  
>s表示符号位，0正，1负  
>M尾数二进制小数，大于等于1小于2  
>E阶码对浮点数加权，权重是2的E次幂  

声明一个变量只是将变量名标识符的有关信息告诉编译器，使编译器“认识”该标识符，但声明不一定引起内存的分配  
定义变量意味着给变量分配内存空间，用于存放对应类型的数据，变量名就是对相应的内存单元的命名

声明并初始化为变量创建和标记存储空间，并为其指定初始值

## 整型
### int类型 有符号整型

表示正整数，负整数和零，存储占用一个字长  
取值范围根据系统的字长决定，一般是32位,4个字节 
-2,147,483,648~2,147,483,647  
八进制字面量使用0前缀，十六进制字面量使用0x或0X  
格式化转换符十进制%d,八进制%o,十六进制%x，显示前缀需要%#o,%#x,%#X
>printf要保证转换符数量与待打印变量数量一致,类型匹配，编译器不检查

### 其他整型

* short 格式化字符%h
* long 字面量加L后缀 格式化字符%l
* long long 字面量加LL后缀 格式化字符%ll
* unsigned 无符号数 u或者U后缀 格式化字符%u
  
整型的溢出，一般是反转，有符号从0开始，无符号已负的最大值开始

### char类型 字符类型

字符：字母和符号  
char类型也是整数类型，实际存储的是整数，实际是使用数字编码处理字符  
字符常量使用单引号，双引号是字符串。
>字符常量是使用int存储，所以存在'FATE',赋值给char类型只有最后八位有效'E'

非打印字符，转义字符
|Sequence|Meaning|
|---------|---------|
|\a |Alert (ANSI C).警报|
|\b |Backspace.退格|
|\f |Form feed.换页|
|\n |Newline.换行|
|\r |Carriage return.回车|
|\t |Horizontal tab.水平制表符|
|\v |Vertical tab.垂直制表符|
|\\ |Backslash ( \ ).反斜杠\|
|\' |Single quote ( ' ).单引号|
|\" |Double quote ( " ).双引号|
|\? |Question mark ( ? ).问好|
|\0oo| Octal value. ( o represents an octal digit.)八进制值|
|\xhh |Hexadecimal value. ( h represents a hexadecimal digit.)十六进制值|

\0oo和\xhh的写法更好的表达使用字符编码的意图

格式化转换字符%c， %d表示的是字符编码的整数值

### _Bool类型 布尔值

C语言值0表示false，非0表示true

_Bool原则上仅占一位存储空间，非零表达式值自动转换为1

### 可移植类型 stdint.h和inttypes.h

* 精准宽度整型 int32_t
* 最小宽度整型 int_last8_t
* 最块最小宽度整型 int_fast8_t

stdint.h定义类可移植类型名
inttypes.h定义可移植类型对应的格式化转换说明字符串宏

## 浮点数

* float 至少表示6位有效数字
* double 至少表示13位有效数字
* long double

字面量:有符号的数字（包含小数点）后面跟e或E，最后是一个有符号数表示10的指数。类似2.87e-3,-1.56E+12。后面还可加%f(用float覆盖默认的double)，%L(long double)

格式化转换字符：%f，%e(指数计数法)

浮点数的溢出：inf NaN 下溢损失精度

复数和虚数 float _Complex； double _Complex； long double _Complex；

## 类型大小 

sizeof运算符，以字节为单位  格式化输出使用%zd或者%u，%lu