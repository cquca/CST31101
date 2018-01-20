## Verilog中组合逻辑的不同实现方式

验证实验给出两种不同的组合逻辑实现方式：

* assign方式

```verilog
module calculate(
    input wire [7:0] num1,
    input wire [2:0] op,
    output [31:0] result
    );
    wire [31:0] num2;
    wire [31:0] Sign_extend;

    assign num2 = 32'h00000001;
    assign Sign_extend={{24{1'b0}},num1[7:0]};
    assign result = (op == 3'b000)? Sign_extend + num2:
                    (op == 3'b001)? Sign_extend - num2:
                    (op == 3'b010)? Sign_extend & num2:
                    (op == 3'b011)? Sign_extend | num2:
                    (op == 3'b100)? ~Sign_extend: 32'h00000000;
endmodule
```

* always方式

```verilog
module calculate(
    input wire [7:0] num1,
    input wire [2:0] op,
    output reg [31:0] result
    );
    reg [31:0] num2;
    reg[31:0] Sign_extend;
    always @(op) begin
       num2 = 32'h00000001;
       Sign_extend={24'h000000,num1[7:0]};
            case(op)
                3'b000:result = Sign_extend + num2;
                3'b001:result = Sign_extend - num2; 
                3'b010:result = Sign_extend &  num2;
                3'b011:result = Sign_extend |  num2;
                3'b100:result = ~Sign_extend  ;          
                default:result = 32'h00000000;
            endcase
        end
endmodule
```

---

二者区别对比如下:

|  | assign方式 | always方式 |
| :--- | :--- | :--- |
| result | wire | reg |
| num2 | wire | reg |
| sign\_extend | wire | reg |

always方式既可以实现组合逻辑，也可实现时序逻辑：

1. always @（a or b or c）或always@（\*）形式的，即不带时钟边沿的，综合出来还是组合逻辑；
2. always @（posedge clk）形式的，即带有边沿的，综合出来一般是时序逻辑，会包含触发器（Flip-Flop）

---

观察always方式的触发信号op，可以得知其为组合逻辑。在这里，给出两种方式在FPGA资源及编程难度上的对比。

|  | assign方式 | always方式 |
| :--- | :--- | :--- |
| 资源占用 | 使用wire变量，综合得到的组合逻辑全部由导线构成，不占用FPGA资源 | 由于内部赋值与输出都需要使用reg变量，同为组合逻辑，需占用一定资源 |
| 编程难度 | 面向信号进行状态描述，一般需要考虑单个信号在所有状态下的可能性，需要完全理解后进行编程。 | 面向实验需求描述，always模块内书写方式与高级语言相仿，可以按照实验要求逐一列举。 |
| 理解难度 | 阅读者理解难度大。 | 阅读者理解较容易。 |

**注意:Imagination及龙芯高校开源计划代码均采取assign方式，实验推荐使用assign方式实现组合逻辑。设计实验中新增内容使用assign方式增加输出信号更为简单。**

