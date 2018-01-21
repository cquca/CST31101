## 实验原理

![](/assets/p2.3-1.png)

实验完整原理图如上图所示，根据原理图可将5个模块连接并完成实验。下面分别介绍各模块原理。

---

### 取指阶段原理

![](/assets/p2.3-2.png)

如上图所示，PC为32bit\(1 word\)的寄存器，其存放指令地址，每条指令执行完毕后，增加4，即为下一条指令存放地址。指令地址传入指令存储器，即可取出相应地址存放的指令。

**需要注意的是，MIPS架构中，采用字节读写，1 32bit word = 4 byte，故需要地址+4来获取下一条指令。 **

---

### 指令译码原理

![](/assets/p2.3-3.png)

如上图所示，32位MIPS指令在不同类型指令中分别有不同结构。但\[31:16\]表示的opcode，以及\[5:0\]表示的funct，为译码阶段明确指令控制信号的主要字段。下表为Opcode及funct识别得到的部分信号，详细信号表参照课本及课堂Slides。

| opcode | aluop | operation | funct | alu function | alu control |
| :--- | :--- | :--- | :--- | :--- | :--- |
| lw | 00 | load word | XXXXXX | add | 010 |
| sw | 00 | store word | XXXXXX | add | 010 |
| beq | 01 | branch equal | XXXXXX | subtract | 110 |
| R-type | 10 | add | 100000 | add | 010 |
|  |  | subtract | 100010 | subtract | 110 |
|  |  | and | 100100 | and | 000 |
|  |  | or | 100101 | or | 001 |
|  |  | set-on-less-than | 101010 | slt | 111 |



