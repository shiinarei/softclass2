#Java实现论文查重
软件工程|https://edu.cnblogs.com/campus/gdgy/CSGrade21-12?page=4
作业要求|https://edu.cnblogs.com/campus/gdgy/CSGrade21-12/homework/13014
作业目标|计一个论文查重算法，给出一个原文文件和一个在这份原文上经过了增删改的抄袭版论文的文件，在答案文件中输出其重复率。
作业目标|学习代码实现论文查重，并学会PSP模式
Github链接|https://github.com/13ugYellow/13ugYellow
#PSP2.1
| PSP2.1                                |   Personal Software Process Stages    | 预估耗时（分钟） | 实际耗时（分钟） |
| ------------------------------------- | :-----------------------------------: | :--------------: | :--------------: |
| Planning                              |                 计划                  |        25        |        25        |
| Estimate                              |       估计这个任务需要多少时间        |        310        |        330       |
| Development                           |                 开发                  |        30        |        25        |
| Analysis                              |      需求分析（包括学习新技术）       |        10        |        10        |
| Design Spec                           |             生成设计文档              |        10         |        15        |
| Design Review                         |               设计复审                |        10        |        15        |
| Coding Standard                       | 代码规范 (为目前的开发制定合适的规范) |        5        |        5        |
| Design                                |               具体设计                |        20        |        30        |
| Coding                                |               具体编码                |        60        |        75        |
| Coding Review                         |               代码复审                |        30        |        30        |
| Test                                  | 测试（自我测试，修改代码，提交修改）  |        20        |        15        |
| Reporting                             |                 报告                  |        50        |        45       |
| Test Repor                            |               测试报告                |        30        |        25        |
| Size Measurement                      |              计算工作量               |        20        |        30        |
| Postmortem & Process Improvement Plan |     事后总结, 并提出过程改进计划      |        15        |        10        |
| 
                                      |                 合计                  |       335        |     355          |
#模块接口的设计与实现过程
## 创建get_file_contents函数获取指定路径的文件内容
![](https://img2023.cnblogs.com/blog/3273975/202309/3273975-20230916231238446-1793755264.png)


## 创建filter函数将读取到的文件内容先进行jieba分词，然后再把标点符号、转义符号等特殊符号过滤掉
![](https://img2023.cnblogs.com/blog/3273975/202309/3273975-20230916231407132-1817145243.png)


## 创建calc_similarity函数传入过滤之后的数据，通过调用gensim.similarities.Similarity计算余弦相似度
![](https://img2023.cnblogs.com/blog/3273975/202309/3273975-20230916231510577-2089323915.png)


## 测试代码
![](https://img2023.cnblogs.com/blog/3273975/202309/3273975-20230916231553670-2106921765.png)


# 性能测试
##内存占用
##get_file_contents函数
![](https://img2023.cnblogs.com/blog/3273975/202309/3273975-20230916234258855-2085862474.png)


##filter函数
![](https://img2023.cnblogs.com/blog/3273975/202309/3273975-20230916234548676-259778850.png)


##calc_similarity函数
![](https://img2023.cnblogs.com/blog/3273975/202309/3273975-20230916234733803-1252893475.png)

##耗时
![](https://img2023.cnblogs.com/blog/3273975/202309/3273975-20230917000558079-362452446.png)

##分析
由结果可知，整个程序耗时约1.33s，其中用来文件查重的余弦算法耗时最长，占用内存最多，花了1.1362s，占用内存159.4MB。可以通过将余弦算法换为simhash算法，提高性能。

# 模块异常分析
本模块只会在读文件时发生异常，不过由于查重材料是给定的，直接将其绝对路径作为测试素材，故不会出现异常。

#导包
![](https://img2023.cnblogs.com/blog/3273975/202309/3273975-20230917003404069-217439796.png)

#最终结果
![](https://img2023.cnblogs.com/blog/3273975/202309/3273975-20230917003038914-692733662.png)
