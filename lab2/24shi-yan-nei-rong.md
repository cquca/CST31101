## 实验内容

阅读实验原理实现以下模块：

1. _**PC**_，要求输出指令存储器_**Inst\_Rom**_读使能信号ce，地址addr\(长度自定，与ROM地址匹配\)。若选择按字节使能\(Byte Write Enable\)，PC+4得到地址；否则使用PC+1。

2. _**Controller**_，其中包含两部分，分别为_**main\_decoder**_，_**alu\_decoder**_。参考MIPSfpga中控制器的实现代码，使用组合逻辑产生下列信号：

| memtoreg | memwrite | pcsrc | alusrc | regdst | regwrite | jump | alucontrol |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| \[0:0\] | \[0:0\] | \[0:0\] | \[0:0\] | \[0:0\] | \[0:0\] | \[0:0\] | \[2:0\] |
| led\[0\] | led\[1\] | led\[2\] | led\[3\] | led\[4\] | led\[5\] | led\[6\] | led\[7:9\] |



