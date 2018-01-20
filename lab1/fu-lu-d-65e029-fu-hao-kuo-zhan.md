## 附录 D 有符号扩展与无符号扩展

* 无符号扩展：扩展位全部置0：

```verilog
assign sign_extend = {{24{1'b0}},num1[7:0};
```

* 有符号扩展：扩展位全部置最高位的值：

```verilog
assign sign_extend = {{24{num1[7]}},num1[7:0};
```



