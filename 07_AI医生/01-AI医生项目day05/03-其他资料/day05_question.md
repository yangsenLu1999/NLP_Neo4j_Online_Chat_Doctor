- 作业题1: 
  - 给定一个整形数组, 找出最大下标距离 j - i , 当且仅当 A[i] < A[j] 和 i < j 。
  
  - 示例: 输入数组为[5, 3, 4, 0, 1, 4, 1], 则最大下标距离产生于A[i]=3, i=1和A[j]=4, j=5的时候, 此时j - i = 4, 这个4就是满足条件的最大下标距离。
  
  - ```
    # 函数调用格式如下
    def main():
        array = [5, 3, 4, 0 ,1, 4, 1]
        dis = maxDistance(array)
        print("dis=%d," % dis)
    
    
    if __name__ == '__main__':
        main()
    ```
    





- 作业题2: 给定一个一维整形数组，里面只有一个数字出现了一次，其他数字都出现了2次，请将这个唯一出现了一次的数字找出来。

  - 示例: 给定数组 A = [2, 35, 8, 16, 8, 2, 7, 35], 返回唯一只出现了一次的7
  
  - ```
    # 函数调用格式如下
    def main():
        array = [2, 35, 8, 16, 8, 2, 7, 35]
        num = onlyOneTimeNumber(array)
        print("num=%d," % num)
    
    
    if __name__ == '__main__':
        main()
    ```
  
  - 
  
  



- 作业题3: RNN相关
  - 1: 为什么RNN会比CNN更容易出现梯度消失或爆炸, 有哪些改进方案?
  - 2: RNN可以采用Relu激活函数吗?为什么?
  - 3: 画出LSTM的单元结构图, 以及其中涉及到的计算公式?
  - 4: 相比于RNN处理序列数据, 我们可以用CNN处理同样的文本吗?如何实施? 有哪些需要特殊处理的地方?请尽可能详细的给出说明或图示.(不必要写代码)





- 作业题4: 完成当天的知识总结, 按照自己的理解和进度(代码部分自己安排), 总结文件提交。