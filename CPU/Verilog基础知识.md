###  **Verilog **中的数据类型

`wire`：线网型，用于连续赋值，只能作为连接信号，不能存储值，表示电路的物理连接。

​	程序中 `input` 和 `output` 默认都是 `wire` 线网型的。

`reg`：寄存器类型，用于在过程块中赋值，reg 类型数据的缺省是未知的。reg 数据可以是正值或者是负值，但当一个 reg 类型数据是一个表达式中的操作数时，它的值首先被当为无符号值。如果一个4位的 reg 类型数据被写入 -1 (1111)，在表达式运算中，它的值就是 +15。**所有在 always，initial 语句块中赋值的信号必须定义为 `reg` 类型**

`parameter`：参数



input 端口不能声明为 reg 类型，输入端口只能是 wire 类型，这是因为输入端口用于接收信号，而不能存储值。reg 类型通常在时序逻辑中存储数据，因此只能在模块内部定义或用于 output



###  timescale systax

```verilog
`timescale <time_unit> / <time_precision>
```

The *time_unit* is the measurement of delays and simulation time while the *time_precision* specifies how delay values are rounded before being used in simulation.



### initial 块

每个 initial 块在程序中只能执行一次，它会按照顺序执行块中的所有代码

多个 initial 块中的代码是并行执行、同时执行的

```verilog
    initial begin
        in = 4'b0001;
        #10;
        in = 4'b0010;
        #10;
        in = 4'b0100;
        #10;
        in = 4'b1000;
        #10;
    end

	initial begin
        reset = 1;
    end
```



### case 语句块

case 语句块中不能使用 assign

```verilog
reg [3:0] option;
case (option)
    4'b0000: begin
        ...
    end
    4'b0001: begin
        ...
    end
    default: begin
        ...
    end
endcase
```

### enum

```verilog
typedef enum {
    ADD,
    SUB,
    SLT,
    SLTU,
    SLL,
    SRL,
    SLA,
    SRA,
    AND,
    OR,
    XOR,
    NOR
} OPERATION;

OPERATION OP;

case (op)
    ADD:
    SUB:
    default:
endcase
```

### paremeter

```verilog
parameter   ADD = 4'B0000, // 0
            SUB = 4'B0001,
            MUL = 4'B0010,
            DIV = 4'B0011,
            AND = 4'B0100,
            OR  = 4'B0101,
            XOR = 4'B0110,
            NOR = 4'B0111,
            SLT = 4'B1000,
            SLTU= 4'B1001,
            SLL = 4'B1010,
            SRL = 4'B1011,
            SLA = 4'B1100,
            SRA = 4'B1101; // 13
```

### always

在 Verilog 中，`always` 块后面通常跟随一段逻辑，描述在触发条件下的操作。`always` 块的主要作用是实现**时序逻辑**或**组合逻辑**，具体取决于触发条件的不同。通常情况下，`always` 后面可以使用以下类型的语句：

1. `@(*)` —— 组合逻辑

- 使用 `@(*)` 作为触发条件，表示在任何输入信号发生变化时，`always` 块都会重新评估。这通常用于组合逻辑（无时钟控制），适用于`if-else`、`case`语句等。

```verilog
always @(*) begin
    if (sel) 
        out = in1;
    else 
        out = in2;
end
```

2. `@(posedge clock)` —— 正沿触发的时序逻辑

- `@(posedge clock)` 表示在时钟信号 `clock` 的上升沿（从0到1的瞬间）触发 `always` 块。用于设计同步时序逻辑，例如寄存器和状态机。

时序逻辑 - 寄存器

```verilog
always @(posedge clock) begin
    if (reset)
        q <= 0;
    else
        q <= d;
end
```

3. `@(negedge clock)` —— 负沿触发的时序逻辑

- `@(negedge clock)` 表示在时钟信号 `clock` 的下降沿（从1到0的瞬间）触发 `always` 块。常用于边缘触发器的设计，但负沿触发时钟较少使用。

```verilog
always @(negedge clock) begin
    if (reset_n == 0)
        q <= 0;
    else
        q <= d;
end
```

4. `@(posedge clock or posedge reset)` —— 时钟与异步复位信号组合

- `@(posedge clock or posedge reset)` 表示当时钟信号上升沿或复位信号上升沿发生时，触发 `always` 块。复位信号一般用于在初始化时清零或设置寄存器。

```verilog
always @(posedge clock or posedge reset) begin
    if (reset)
        q <= 0;        // 异步复位
    else
        q <= d;
end
```

5. `@(negedge clock or negedge reset_n)` —— 下降沿时钟与下降沿复位信号组合

- `@(negedge clock or negedge reset_n)` 表示在时钟信号下降沿或复位信号下降沿触发 `always` 块。复位信号一般设置为低电平有效（`reset_n` 表示低有效复位）。

```verilog
always @(negedge clock or negedge reset_n) begin
    if (!reset_n)
        q <= 0;        // 异步复位
    else
        q <= d;
end
```

6. 触发信号的组合（事件列表）

- `always` 块可以在多个信号的特定边沿触发，用逗号分隔多个信号和边沿条件。

```verilog
always @(posedge clock, posedge enable, posedge reset) begin
    // 多信号触发逻辑
end
```

7. 无限循环 `always` 块

- 在某些测试中会使用 `always` 结合 `#` 延迟语句生成周期性信号，例如生成一个时钟信号。此时 `always` 块后不需要事件触发条件。

```verilog
reg clk;
initial clk = 0;

always begin
    #5 clk = ~clk;   // 每5个时间单位翻转一次，生成时钟信号
end
```

### 在实践中遇到的问题

在 Verilog 中，不能在 always 块中实例化模块。模块实例化必须在设计的顶层结构中完成，而不是在always 块中。verilog的设计结构是模块实例化成为静态过程，这意味着所有模块实例在仿真或综合之前就已经确定。always 是行为描述的区域，不支持动态的模块化实例。

如果需要在 always 块中选择不同的操作，可以用如下方法：

多路复用器：使用always 快通过条件选择不同的输入源，将模块实例化放在always块外面。

组合逻辑和控制信号：实例化所有需要的模块，然后用控制信号来选择不同模块的输出。

**不可用 `reg` 连接模块输出**