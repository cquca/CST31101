## Verilog中组合逻辑的不同实现方式

验证实验给出两种不同的组合逻辑实现方式：

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



