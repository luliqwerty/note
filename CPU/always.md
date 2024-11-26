在 Verilog 中，`always` 块后面通常跟随一段逻辑，描述在触发条件下的操作。`always` 块的主要作用是实现**时序逻辑**或**组合逻辑**，具体取决于触发条件的不同。通常情况下，`always` 后面可以使用以下类型的语句：

### 1. `@(*)` —— 组合逻辑

- 使用 `@(*)` 作为触发条件，表示在任何输入信号发生变化时，`always` 块都会重新评估。这通常用于组合逻辑（无时钟控制），适用于`if-else`、`case`语句等。

```verilog
always @(*) begin
    if (sel) 
        out = in1;
    else 
        out = in2;
end
```

### 2. `@(posedge clock)` —— 正沿触发的时序逻辑

- `@(posedge clock)` 表示在时钟信号 `clock` 的上升沿（从0到1的瞬间）触发 `always` 块。用于设计同步时序逻辑，例如寄存器和状态机。

#### 时序逻辑 - 寄存器

```verilog
always @(posedge clock) begin
    if (reset)
        q <= 0;
    else
        q <= d;
end
```

### 3. `@(negedge clock)` —— 负沿触发的时序逻辑

- `@(negedge clock)` 表示在时钟信号 `clock` 的下降沿（从1到0的瞬间）触发 `always` 块。常用于边缘触发器的设计，但负沿触发时钟较少使用。

```verilog
always @(negedge clock) begin
    if (reset_n == 0)
        q <= 0;
    else
        q <= d;
end
```

### 4. `@(posedge clock or posedge reset)` —— 时钟与异步复位信号组合

- `@(posedge clock or posedge reset)` 表示当时钟信号上升沿或复位信号上升沿发生时，触发 `always` 块。复位信号一般用于在初始化时清零或设置寄存器。

```verilog
always @(posedge clock or posedge reset) begin
    if (reset)
        q <= 0;        // 异步复位
    else
        q <= d;
end
```

### 5. `@(negedge clock or negedge reset_n)` —— 下降沿时钟与下降沿复位信号组合

- `@(negedge clock or negedge reset_n)` 表示在时钟信号下降沿或复位信号下降沿触发 `always` 块。复位信号一般设置为低电平有效（`reset_n` 表示低有效复位）。

```verilog
always @(negedge clock or negedge reset_n) begin
    if (!reset_n)
        q <= 0;        // 异步复位
    else
        q <= d;
end
```

### 6. 触发信号的组合（事件列表）

- `always` 块可以在多个信号的特定边沿触发，用逗号分隔多个信号和边沿条件。

```verilog
always @(posedge clock, posedge enable, posedge reset) begin
    // 多信号触发逻辑
end
```

### 7. 无限循环 `always` 块

- 在某些测试中会使用 `always` 结合 `#` 延迟语句生成周期性信号，例如生成一个时钟信号。此时 `always` 块后不需要事件触发条件。

```verilog
reg clk;
initial clk = 0;

always begin
    #5 clk = ~clk;   // 每5个时间单位翻转一次，生成时钟信号
end
```

### 常用语句类型

`always` 块内部可以包含多种语句，如：

- **赋值语句**：`<=`（非阻塞赋值）、`=`（阻塞赋值）
- **条件语句**：`if-else`
- **多路分支**：`case`
- **循环语句**：`for`、`while`、`repeat`

### 示例总结

以下是一个典型的 `always` 块示例，包含时序逻辑和组合逻辑：

```verilog
module example (
    input wire clock,
    input wire reset,
    input wire [1:0] sel,
    input wire [7:0] in1, in2, in3, in4,
    output reg [7:0] out
);

    always @(posedge clock or posedge reset) begin
        if (reset)
            out <= 8'b0;
        else begin
            case (sel)
                2'b00: out <= in1;
                2'b01: out <= in2;
                2'b10: out <= in3;
                2'b11: out <= in4;
                default: out <= 8'b0;
            endcase
        end
    end
endmodule
```

这个模块在时钟的上升沿或复位信号触发时执行。