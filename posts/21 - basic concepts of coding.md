- [编码的基本概念](#编码的基本概念)
  - [信源编码](#信源编码)
  - [分类](#分类)
  - [前缀条件](#前缀条件)


## 编码的基本概念

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20220923112742360.png)

码符号C表示的是**编码的字符集**。如二进制编码，c:{0，1} (无特殊说明，本章所有编码都是二进制编码);

信源编码就是**将信源符号序列按照一定的数学规律映射成由码符号组成的码序列的过程。**

+ 信源编码器输入的消息序列:
  $$
  \boldsymbol{X}=(X_{1} X_{2} \ldots X_{l} \quad \ldots X_{L}) ,
  X_{l} \in\{a_{1}, \ldots a_{n}\}
  $$
  输入的消息总共有  $n^{L}$  种可能的组合

- 输出的码字 (码序列) 为:

  $$
  \begin{array}{l}
  Y=(Y_{1} Y_{2} \ldots Y_{k} \ldots Y_{K}),
  Y_{k} \in\{b_{1}, \ldots b_{m}\}
  \end{array}
  $$
  输出的码字总共有  $m^{K}$种可能的组合。

### 信源编码

将信源输出符号X, 经信源编码器后变换成另外的压缩符号Y,  然后将压缩后信息经信道传送给信宿。

信源符号之间存在**分布不均匀**和**相关性**,使得信源存在冗余度,**信源编码**的主要任务就是**减少冗余,提高编码效率**。

针对信源输出符号序列的**统计特性**, 寻找一定的方法把信源输出符号序列变换为**最短**的码字序列。

### 分类

分组码和非分组码

1.分组码: 信源序列在进入编码器之前先**分成若干信源符号组**（也称信源字），将信源编码器根据一定的规则用码符号序列（也称码字）表示信源字作为编码器的输出。

2.非分组码: 信源序列连续不断地从编码器的输入端进入，同时在编码器的输出端连续不断的产生码序列。

![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20220923113517071.png)

> 例 信源符号$X=\{a_{1}, a_{2}, a_{3}, a_{4}\}$对应不同码字如表
>
> ![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20220923113809815.png)
>
> 该信源的信息熵为:1.75 bit/symbol
>
> + 等长码:码中所有码字的长度都相同，如:码0
>
> + 变长码;码中的码字长短不一，如:码1、2、3、4
>
> + 非奇异码:信源符号与码字是一一对应的，如:码0、2、3、4
>
> + 奇异码:信源符号与码字不是一一对应的，如:码1
>
> + 唯一可译码: 任意有限长的码元序列,只能被唯一地分割成一个个的码字。如码0、3、4。
>
>   例:{0,10,11}是一种唯一可译码。
>
>   任意一串有限长码序列,如100111000,只能被分割成 10,0,11,10,0,0。**任何其他分割法都会产生一些非定义的码字**。
>
> + 奇异码不是唯一可译码
> + 非奇异码
>   + 唯一可译码，如: 码3;
>   + 非唯一可译码，如:码2;

+ 非即时码（延长码）
  如果接收端收到一个完整的码字后不能立即译码，还需等下一个码字开始接收后才能判断是否可以译码，如：码 3；在延长码中有的码是唯一可译的取决于码的总体结构。

+ 即时码 （非延长码 ) （异前缀码 )
  在译码时无需参考后续的码符号就能**立即** 作出判断 译成对应的信源符号。如：码 0 、 4
  **任意一个码字都不是其它码字的 前缀 部分——前缀条件**。
  **可以证明，一种可唯一译码并且具有即时性的编码方法必定满足前缀条件。**

### 前缀条件

任意一个码字都不是其它码字的前缀部分----前缀条件。
如:**码0**:  00、01、10、11。**码4**: 1、01、001、0001
**可以证明，一种可唯一译码并且具有即时性的编码方法必定满足前缀条件。**

> 判断码:000、001、01、10是否唯一可译?是否是即时码?
>
> ![](https://raw.githubusercontent.com/timerring/picgo/master/picbed/image-20230204173736436.png)
>
> 由上图可知，都是。

```C
#include<stdio.h>
#include<string.h >
char c[100][50];
char f[300][50];
int N, sum = 0; // N为输入码字的个数, sum为尼随后缀集合中码字的个数
int flag; //判断是否唯一可译标查位
void patterson(char c[],char d[]) //检测尾随后缀
{
	int i, j, k;
	for (i = 0;; i++)
	{
		if (c[i] == '\0' && d[i] == '\0')   //字符一样跳出
			break;
		if (c[i] == '\0')   //d比c长，将d的尾随后缀放入f中
		{
			for (j = i; d[j] != '\0'; j++)f[sum][j - i] = d[j];
			f[sum][j - i] = '\0';
			for (k = 0; k < sum; k++)
			{
				if (strcmp(f[sum], f[k]) == 0)   //查看当前生成的尾随后缀在f集合中是否存在
				{
					sum--; sum--; break;
				}
			}
			sum++;
			break;
		}
		if (d[i] == '\0')  //c比d长，将c的wei'sui后缀放入f中
		{
			for (j = i; c[j] != '\0'; j++)f[sum][j - i] = c[j];
			f[sum][j - i] = '\0';
			for (k = 0; k < sum; k++)
			{
				if (strcmp(f[sum], f[k]) == 0)   //查看当前生成的尾随后缀在f集合中是否存在
				{
					sum--; break;
				}
			}
			sum++;
			break;
		}
		if (c[i] != d[i])
			break;
	}
}
int main()
{
	int i, j;
	printf("请输入码字的个数（小于100）：");   //输入码得个数
	scanf_s("%d", &N,10);
	while (N > 100)
	{
		printf("输入码字得个数过大，请输入小于100的数\n");
		printf("请输入码字的个数（小于100）：");
		scanf_s("%d", &N,10);
	}
	flag = 0;
	printf("请分别输入码字（每个码字长度小于50个字符）:\n");
	for (i = 0; i < N; i++)
	{
		scanf_s("%s", &c[i],51);
	}
	for(i=0;i<N-1;i++)    //判断如果码本身是否重复
		for (j = i + 1; j < N; j++)
		{
			if (strcmp(c[i], c[j]) == 0)
			{
				flag = 1; break;
			}
		}
	if (flag == 1)
		printf("这不是唯一可译码。\n");
	else
	{
		for (i = 0; i < N ; i++)  //根据原始编码生成的尾随后缀集合s[1]放入f中
		{
			for (j = i + 1; j < N; j++)
				patterson(c[i], c[j]);
		}
		for (i = 0;; i++)
		{
			int s = 0;
			for (j = 0; j < N; j++)
			{
				if (i == sum)
				{
					s = 1; break;
				}
				else patterson(f[i], c[j]);
			}
			if (s == 1)break;
		}
		for (i = 0; i < sum; i++)   //判断p里面的字符串是否与s中的重复，重复则不是唯一的
		{
			for (j = 0; j < N; j++)
			{
				if (strcmp(f[i], c[j]) == 0)
				{
					flag = 1;
					break;
				}
			}
		}
		if (flag == 1)
			printf("这不是唯一可译码的。\n");
		else
			printf("这是唯一可译码。\n");
	}
	printf("尾随后缀集合为：");
	for (i = 0; i <= sum; i++)
		printf("\n%s", f[i]);
}

```



参考文献：

1. Proakis, John G., et al. *Communication systems engineering*. Vol. 2. New Jersey: Prentice Hall, 1994.
2. Proakis, John G., et al. *SOLUTIONS MANUAL Communication Systems Engineering*. Vol. 2. New Jersey: Prentice Hall, 1994.
3. 周炯槃. 通信原理（第3版）[M\]. 北京：北京邮电大学出版社, 2008.
4. 樊昌信, 曹丽娜. 通信原理（第7版） [M\]. 北京：国防工业出版社, 2012.



[返回首页](https://github.com/timerring/information-theory)