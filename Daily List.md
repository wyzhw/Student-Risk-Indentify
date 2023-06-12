# Overview

## Word embedding

![image-20230606185627380](C:\Users\wyzhw\AppData\Roaming\Typora\typora-user-images\image-20230606185627380.png)



## Embedding in Keras

`model.add(Embedding(input_dim, output_dim, input_length))`

> 例如，下面我们定义了一个包含 200 个词汇表的嵌入层（例如从 0 到 199 的整数编码词，包括 0 和 199），一个 32 维的向量空间，其中将嵌入单词，每个输入文档有 50 个单词。
>
> `e = Embedding(200, 32, input_length=50)`

https://machinelearningmastery.com/use-word-embedding-layers-deep-learning-keras/

主要完成的工作：

- 调整了获取 Position Embedding 的函数

  ![image-20230612113443273](C:\Users\wyzhw\AppData\Roaming\Typora\typora-user-images\image-20230612113443273.png)

- 添加了RNN 模型用作分类

  ![image-20230612113509160](C:\Users\wyzhw\AppData\Roaming\Typora\typora-user-images\image-20230612113509160.png)

- 测试了 单个 PE embedding 在RNN 里的model performance (f1-socre)

  ​	assignment-1： 0.66 -> 0.68 (below 80)

  ​	assignment-1,2,3： 0.74 -> 0.72 (below 80)

  

还需要完成的工作：

- 准备一个词汇表和相应的词向量矩阵?作为输入

- Assignment Embedding

  [1,0,0]

  [0,1,0]

  [0,0,1]

​	
