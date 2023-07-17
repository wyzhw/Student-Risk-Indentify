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
------

## Plan

- [x] **d =10** for Position Embedding

- [x] Compare model performance

  - [x] **score / rank** which one is more informative. (below 80)

  - [x] Add LSTM, GRU and Binary LSTM

    |RNN model|Performance| Score | Duration+ | Ratio++ | Rank (d=10) | All |
    | :---------- | :--: | :--: | :--: | :--: | :--: | :--: |
    |ASSIGNMENT 1||  |  |  |  |  |
    |  | *Accuracy* | 0.69 | 0.74 | 0.72 | 0.73 |  |
    |  | *F1_macro* | 0.60 | 0.66 | 0.67 | 0.70 |  |
    | ASSIGNMENT 1, 2, 3 |  | | | | | |
    |  | *Accuracy*  | 0.7942 | 0.8004 | 0.8169 | 0.8128 | **0.8375** |
    |                    | *F1_macro*  | 0.7716 | 0.7748 | 0.7983 | 0.7966 | **0.8221** |

    | LSTM model         | Performance | Score  | Duration+ | Ratio++ | Rank (d=10) |    All     |
    | :----------------- | :---------: | :----: | :-------: | :-----: | :---------: | :--------: |
    | ASSIGNMENT 1, 2, 3 |             |        |           |         |             |            |
    |                    | *Accuracy*  | 0.7963 |  0.7984   | 0.8106  |   0.8169    | **0.8355** |
    |                    | *F1_macro*  | 0.7754 |  0.7758   | 0.7829  |   0.8010    | **0.8218** |

    | GRU model          | Performance | Score  | Duration+ | Ratio++ | Rank (d=10) |    All     |
    | :----------------- | :---------: | :----: | :-------: | :-----: | :---------: | :--------: |
    | ASSIGNMENT 1, 2, 3 |             |        |           |         |             |            |
    |                    | *Accuracy*  | 0.7757 |  0.8005   | 0.8169  |   0.8210    | **0.8313** |
    |                    | *F1_macro*  | 0.7548 |  0.7741   | 0.8017  |   0.8053    | **0.8168** |

    | Bi-LSTM model      | Performance | Score  | Duration+ | Ratio++ | Rank (d=10) |    All     |
    | :----------------- | :---------: | :----: | :-------: | :-----: | :---------: | :--------: |
    | ASSIGNMENT 1, 2, 3 |             |        |           |         |             |            |
    |                    | *Accuracy*  | 0.7963 |  0.8149   | 0.8231  |   0.8272    | **0.8519** |
    |                    | *F1_macro*  | 0.7740 |  0.7966   | 0.8046  |   0.8078    | **0.8417** |


  1. *学生的Assignment 分数。*
  2. *学生提交Assignment的所需要的时间。*
  3. *Assignment分数和提交时间两者的比率。*
  4. *通过使用Score变换得到的Rank得到 Position Embedding*

  > Score: 1
  >
  > Duration: 1+2 
  >
  > Ration: 1+2+3
  >
  > Rank: 4
  >
  > All: 1+2+3+4

  从结果来看，只是用了一个 `Position Embedding 将比Score转化成RANK` 得到的结果就跟`分数`，`时间`、以及`分数和时间的比例`打平，甚至略好，可以认为 RANK 比单纯的 SCORE 更有意义和参考性。我认为其中的原因可能是由于：

  > 排名反映了学生的相对水平和竞争力，而成绩可能受到不同作业难度、评分标准等因素的影响。
  > 排名更好地消除了数据的量纲和尺度差异，使数据更加规范化和标准化，便于 RNN 模型的训练和收敛。
  > 排名能够捕捉数据的变化趋势和动态特征，而成绩可能存在一些噪声和异常值，影响 RNN 模型的泛化能力。

- [ ] 关于使用 assignment embeddings：

  All assignment embeddings are the same, while we have different outputs to predict. 由于我们只使用了三个作业的情况来预测学生的最终成绩是否危险。故对于每个作业，我们的token是一样的。相当于每一位学生，他们concatenate 之后就会有部分数据的列相同，而他们最终的成绩是否危险确是不得而知的。因此，对于模型来说，只要输入的token相同，得到的Assignment Embedding 也是相同的，反而为训练提供了噪音。




​	关于不同的模型与代码的参数如下，地址为：https://github.com/wyzhw/Student-Risk-Indentify
