代码规范
---
[TOC]
## 0.规定的英文缩写：
| 原词        | 缩写 | 原词        | 缩写  |
| ----------- | ---- | ----------- | ----- |
| clock       | clk  | reset       | rst   |
| enable      | ena  | button      | btn   |
| switch      | sw   | address     | addr  |
| input       | in   | output      | out   |
| synchronic  | syn  | asynchronic | async |
| counter     | ctr  | divider     | div   |
| control     | ctrl | instruction | instc |
| accumulator | acc  | register    | rgs   |
| selector    | sel  | generate    | gen   |
| current     | curr | previous    | prev  |
| memory      | mem  |


## 1.设计文件 `xxx.v`
#### 1.文件与模块的命名
* 命名全部用英文小写，较长的单词使用英文缩写，用下划线 `_` 来分隔单词
* 同时一个文件中只有一个模块，模块的名字应该和文件名字相同。

#### 2.模块实例化
```verilog
    moy_mod u_my_mode (
        .port_a         ( clk           ),
        .port_b         ( rst_n         ),
        .port_c         ( port_c_in     ),

        .port_d         ( port_d_out    ),
        .port_e         ( port_e_out    )
    );
```


#### 2.端口的定义
* 统一在 `module()` 内部命名端口。
* 输入输出之间空一行并且分别添加注释。
* `wire` 和 `reg` 都要全部写上。
* 对于输入的变量：除了`clk` `rst` ，其他的加上_i后缀；对于输出的变量：加上_out后缀
* 注意对齐，使用Tab键快速对齐。
```verilog
    module my_mod(
        //input
        input   wire                clk                 ,
        input   wire                rst_n               ,
        input   wire    [ 3 : 0 ]   port_a_in           ,
        input   wire    [ 15 : 0 ]  port_b_in           ,
        input   wire    [ 3 : 0 ]   port_long_name_in   ,

        //output
        output  reg     [ `MY_PARA : 0 ]    port_with_param_out ,
        output  reg     [ 4 : 0 ]           port_c_out          ,
        output  reg     [ 3 : 0 ]           port_d_out
    );
```

#### 3.变量
##### 1.静态变量
* `parameter`  `define` 等静态变量，在设计文件之外新建一个 `parameter.v` 文件来进行声明，`localparam` 在设计文件内。
* 静态变量的命名全部用大写英文字母和下划线，例如 `MY_PARA`
```verilog
    `define     MY_PARA_A       1
    
    parameter   MY_PARA_B       2

    localparam  MY_PARA_C       3
```

##### 2.动态变量
* 命名使用英文小写字母以及下划线。英文缩写参照上面的表格。
* 对于时钟信号：应该注明其频率。例如 `clk_100MHz` `vga_clk_25kHz`
* 对于复位信号：
  | rst         | rst_n       | arst        | arst_n      |
  | ----------- | ----------- | ----------- | ----------- |
  | 同步，1有效 | 同步，0有效 | 异步，1有效 | 异步，0有效 |
* 变量的声明应该全部集中于端口定义结束之后。

##### 3.常量
* 显式定义位宽，尽量不要出现 0 ，1 等未定义位宽的数字。
* 在同一种情境下，不要混用进制。

#### 4.块的写法
##### 1.`begin` `end` 块
无论接下来的语句有多少行，都要写出`begin` `end`；`begin`接在语句第一行之后，`end` 另起一行.
##### 2.`case`
注意缩进。
```verilog
    case(num)
        10`d1   : variable <= 10'd1     ;
        10`d10  : variable <= 10'd10    ;
        default : variable <= 10'd0     ;
    endcase
```
##### 3.`always`
* 对于组合逻辑的always块：统一写成 `always @(*)` ；注意不要出现锁存器
* 对于时序逻辑的always块：一个块只驱动一个变量；全部都要用复位信号。
##### 4.`generate`块
```verilog
    genvar  index;
    generate
        for (index = 0; index < 10; index = index + 1) begin : block_name
            //code
        end
    endgenerate
```
#### 5.其他
```verilog
    assign  a = ~x + y ;
    assign  b = (~x | (state == `START)) ;
    assign  c = (state == `START) | ((state == `PLAY) & ~x)
                | (state == `FAIL) ;
```
##### 1.空格
一般一元运算符与操作数之间不用空格，二元运算符需要。
##### 2.括号
单目运算符一般不需要括号，双目运算符如果操作数是复杂的表达式则尽量加上括号。
##### 2.换行
一行过长则需要换行。注意换行时尽量不要出现在括号内部。

## 2.测试文件
#### 1.测试文件以及模块的命名
名称为对应的设计文件名称加上后缀 `_tb`。例如：`data_ctrl_tb.v`

#### 2.测试文件的写法
？

## 3.约束文件
```verilog
    set_property -dict {PACKAGE_PIN T2 IOSTANDARD LVCMOS33} [get_ports sw]
```
写好注释：对应的设计文件的端口是什么；在开发板上是什么，位置在哪里；用作什么功能；等等。


