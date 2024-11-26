# PC

### PC 模块的输入和输出

|   port name   | direction | type   | description        |
| :-----------: | --------- | ------ | ------------------ |
|      clk      | input     | wire   | 时钟信号           |
|     reset     | input     | wire   | 复位信号           |
| branch_taken  | input     | wire   | 跳转信号           |
| branch_target | input     | [31:0] | 跳转目标地址       |
|      pc       | output    | [31:0] | 表示当前指令的地址 |



### 核心逻辑：

#### 顺序执行

在大多数情况下，程序按照指令序列从前往后执行，PC 的值会按照指令长度自动增加：

**PC~next~ = PC~next~ + 4;**

这里的 4 是因为 32 位 MIPS 架构中，每条指令长度为 4 字节。

#### 条件跳转

当遇到条件跳转 （如 `beq` ,  `bne`）或者无条件跳转指令 （如`j`），根据分支条件信号 `branch_taken` ，决定 PC 是更新为目标地址还是继续顺序执行。

1. 如果分支成立

    **PC~next~ = branch_target;**

2. 如果分支不成立

    **PC~next~ = PC~next~ + 4;**

### 代码

```verilog
module pc (
	input wire clk,
    input wire reset,
    input wire branch_taken,
    input [31:0] branch_target,
    output wire [31:0] pc
);
    always @(posedge clk or posedge reset) begin
        if (reset) begin
            pc <= 32'b0;	// 复位时 pc 初始化为 0
        end else begin
            pc <= branch_taken ? branch_target : pc + 4;
        end
    end
endmodule
```

### testbench

```verilog
`timescale 1ns / 1ps

module testbench;

    reg clk;
    reg reset;
    reg branch_taken;
    reg [31:0] branch_target;
    reg [31:0] pc;

    testbench dut (
        .clk(clk),
        .reset(reset),
        .branch_taken(branch_taken),
        .branch_target(branch_target),
        .pc(pc)
    );

    initial begin
        clk = 0;
        forever begin
            #5 clk = ~clk;
        end
    end

    initial begin
        reset = 1;
        branch_taken = 0;
        branch_target = 32'h00000000;

        #10 reset = 0;

        #10 branch_taken = 0;

        #20

        branch_target = 32'h00000040;
        #10 branch_taken = 1;
        #10 branch_taken = 0;

        #30 $stop;
    end
    
endmodule
```

# NPC

NPC - next pc

### 输入和输出

|     port name     | direction | type   | description                |
| :---------------: | --------- | ------ | -------------------------- |
|        pc         | input     | [31:0] | 当前PC值                   |
|   branch_target   | input     | [31:0] | 跳转目标地址               |
| exception_handler | input     | [31:0] | 异常处理地址               |
|    npc_select     | input     | [1:0]  | 控制信号：选择下一地址来源 |
|        npc        | output    | [31:0] | 写一条指令地址             |

### 代码

```verilog
module npc (
    input [31:0] pc,
    input [31:0] branch_target,
    input [31:0] exception_handler,
    input [1:0] npc_select,
    output [31:0] npc
);
    always @(*) begin
        case (npc_select)
            2'b00: npc = pc + 4;
            2'b01: npc = branch_target;
            2'b10: npc = exception_handler;
            default: npc = pc + 4;
        endcase
    end
endmodule
```

