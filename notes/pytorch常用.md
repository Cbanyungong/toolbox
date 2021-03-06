[TOC]

---



#### 一、基本函数和功能

---

##### torch.where索引矩阵特定条件元素

矩阵筛选符合条件的值（不用mask了）,可以索引或者作为三元操作符，具体用例：

> torch.where(x > 0, x, y)

---

##### 比较索引获得（大于、等于、非零等）

参见[pytorch索引获得](https://blog.csdn.net/luolinll1212/article/details/82224491)。

其中注意一下nonzero等的返回indice方式是个什么意思：[索引解读](https://blog.csdn.net/monchin/article/details/79750216)，矩阵有几个维度返回的索引就有几个向量，每个向量对应dim n的编号。

---

##### 最值索引

```
x.max(0)    # 按列比较，找出每列的最大值和索引
x.max(1)    # 按行比较，找出每行的最大值和索引
```

---

##### 矩阵填充
```
v=torch.ones(3,3)  
v[1].fill_(1)  
v[2].fill_(2)  
```


#### 二、其他功能

---

##### 随机数种子

```
def setup_seed(seed):
	torch.manual_seed(seed)					 # CPU
	torch.cuda.manual_seed_all(seed)	   # GPU	
	np.random.seed(seed)						 # numpy
	random.seed(seed)							  # random
	torch.backends.cudnn.deterministic = True	# cudnn

setup_seed(20)
```

---

##### 学习率设置

不同层设置不同学习率/冻结层/学习率衰减，参考[链接](https://mp.weixin.qq.com/s?__biz=MzU3NjE4NjQ4MA==&mid=2247485953&idx=2&sn=3ae788b7d643541254ba311f7a7faced&chksm=fd16fb1eca61720870bc58c1a465a346cf2c6a7e8bea39e4b3d582474b595021f3a5b635086d&mpshare=1&scene=1&srcid=0829lJpVJIPQYhNhBEfJ29MZ&sharer_sharetime=1567053900915&sharer_shareid=3cd6dd8f62fdaf4fb8c6de4adbc2f2cd&key=d7c08afaa78fc97e93c23f5f63f9f26051024a83eb55c77f75945dc77fe4c810a94114011509d35616f231381746f42ba7ba594c944ba04dba7551ae1ad01aa83514470e5f933bddf4a332691b04f510&ascene=1&uin=MjQyNDcwMDIwNQ%3D%3D&devicetype=Windows+10&version=62060833&lang=zh_CN&pass_ticket=D0cRCwsVGQnm6JbMF7YpEVwfJFqP1rF8o7L%2BiLBh1TW%2FDh%2BJLNUcwfggb7it%2Bu0P)。

---

##### 数据类型转换

方法一：现有的封装函数

```
# 假定一个tensor为： ts = torch.Tensor([1,2,3])
ts.long() 		#  将tensor投射为long类型
ts.half() 		#  将tensor投射为half类型
ts.int() 		#  将tensor投射为int类型
ts.float() 		#  将tensor投射为float类型
ts.byte() 		#  将tensor投射为byte类型
```

方法二：torch.type()

```
ts = ts.type(torch.IntTensor) # 将ts转换为Int类型的张量
```

方法三：type_as()

```
a1.type_as(a2)  # 将a1转换为a2同类型
```

pytorch包含的张量类型有：

| Data tyoe                | CPU tensor           | GPU tensor                |
| ------------------------ | -------------------- | ------------------------- |
| 32-bit floating point    | `torch.FloatTensor`  | `torch.cuda.FloatTensor`  |
| 64-bit floating point    | `torch.DoubleTensor` | `torch.cuda.DoubleTensor` |
| 16-bit floating point    | N/A                  | `torch.cuda.HalfTensor`   |
| 8-bit integer (unsigned) | `torch.ByteTensor`   | `torch.cuda.ByteTensor`   |
| 8-bit integer (signed)   | `torch.CharTensor`   | `torch.cuda.CharTensor`   |
| 16-bit integer (signed)  | `torch.ShortTensor`  | `torch.cuda.ShortTensor`  |
| 32-bit integer (signed)  | `torch.IntTensor`    | `torch.cuda.IntTensor`    |
| 64-bit integer (signed)  | `torch.LongTensor`   | `torch.cuda.LongTensor`   |



