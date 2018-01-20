## 附录 E  Block Memory Generator设置

IP核查找路径：Flow Navigator-&gt;IP Catalog-&gt;Vivado Repository -&gt;Basic Elements-&gt;Memory Elements-&gt;Block Memory Generator

![](/assets/apendix_e-1.png)

或者Flow Navigator-&gt;IP Catalog，在搜索栏直接搜索Block Memory Generator

![](/assets/apendix_e-2.png)

---

Block Memory Generator共有四类设置，分别为Basic、端口设置、其他设置、Summary：

![](/assets/apendix_e-3.png)

其中Basic需要设置存储器类型，Interface Type需选择Native，选中Generate address interface with 32bits，将地址长度设置为32位，Memory Type根据实验要求选择，其他选项无需设置。

---

![](/assets/apendix_e-4.png)

端口设置需要设置**数据字宽度**及**阵列深度**，根据实验要求，字宽均为32位，阵列深度需根据需求自定义，但不可超过155520字。

写数据端口默认开启写使能，读数据端口默认不开启，可根据自己需求选择Enable Port Type。

---

![](/assets/apendix_e-5.png)

其他设置主要用于加载coe文件，这里只需要注意一个问题，Fill Remaining Memory Locations需要选中，以防读数据操作时，地址超过coe文件已有数据范围，导致异常。

