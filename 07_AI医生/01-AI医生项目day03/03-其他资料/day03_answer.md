- 考试题1: 给定一个整形数组，是否能找出其中的两个数使得其和为某个指定的值? 在第一天代码的基础上分析你的时间复杂度, 然后进行改进达到O(n)

  - ```
    # coding=utf-8
    import numpy as np
    
    def hasSum(array, target):
        dict_array = {}
        for i in xrange(0, len(array)):
            dict_array[array[i]] = i
    
        for i in xrange(0, len(array)):
            temp = target - array[i]
            if dict_array.get(temp, None) == None:
                continue
            else:
                return i, dict_array[temp]
    
        return -1, -1
        
    def main():
        array = [11, 7, 45, 67, 134, 5, 83, 55, 106, 33, 57, 82, 6, 24, 87, 61, 3, 39, 6, 26]
        target_number = 13
        a, b = hasSum(array, target_number)
        if a != -1:
            print('YES, %d, %d' % (a, b))
        else:
            print('NO')
    
    
    if __name__ == '__main__':
        main()
    ```





- 考试题2: 
  - 给定一个单链表, 如果有环, 返回环的长度, 否则返回0.

```
from __future__ import print_function
import numpy as np
from ListModel import ListNode


def lengthOfCircle(list1):
    first = ListNode(0)
    second = ListNode(0)
    first.next_node = list1
    second.next_node = list1
    while first is not None and second is not None:
        if first == second:
            return 1, first
        first = first.next_node
        second = second.next_node
        second = second.next_node

    if first is None or second is None:
        return 0, first
        
def main():
    a1 = ListNode(3)
    a2 = ListNode(8)
    a3 = ListNode(7)
    a4 = ListNode(1)
    a5 = ListNode(2)
    a6 = ListNode(3)
    a7 = ListNode(4)
    a8 = ListNode(5)
    a1.next_node = a2
    a2.next_node = a3
    a3.next_node = a4
    a4.next_node = a5
    a5.next_node = a6
    a6.next_node = a7
    a7.next_node = a8
    a8.next_node = a4
    res, keynode = lengthOfCircle(a1)
    if res == 1:
        print('YES!')
        count_node = keynode.next_node
        num = 1
        while keynode is not count_node:
            count_node = count_node.next_node
            num += 1
        print('The length of circle is %d' % num)
    else:
        print('NO!')
        
if __name__ == '__main__':
    main()
```





- 考试题3: 给定一个数组，找出最少元素，使得将其删除后，剩下的元素是递增有序的。(提示: 本质上就是寻找最长递增子序列)

- ```
  def get_max_ascent_sequence(a):
      hash_index = {}
      max_count = 0
      end = 0
      length = len(a)
      dp = [0] * length
      for i in range(0, length):
          dp[i] = 1
          for j in range(0, i):
              if a[i] >= a[j]:
                  if dp[j] + 1 > dp[i]:
                      dp[i] = dp[j] + 1
                      hash_index[i] = j
                  if dp[i] > max_count:
                      max_count = dp[i]
                      end = i
  
      result = []
      while end >= 0:
          result.append(a[end])
          if end in hash_index.keys():
              end = hash_index[end]
          else:
              end = -1
      result.reverse()
      return result, max_count
      
  
  def main():
      a = [4, 2, 3, 7, 5, 1, 8, 11, 7, 3, 9, 10, 12]
      res, max_num = get_max_ascent_sequence(a)
      print(res)
      print(max_num)
  
  
  if __name__ == '__main__':
      main()
  ```





- 考试题4: 
  - 1.1: 首先fasttext模型结构简单，仅由Embedding层，GAP层和输出层组成，适用于大规模文本分类任务，同时可以预训练词向量。
  - 1.2: fasttext模型的两个显著特征:
    - 使用n-gram特征
    - 使用层次softmax
  - 1.3: 关于层次softmax的原理:
    - softmax是一种使用最优二叉树结构替代网络原有输出层(全连接层)的方式。
    - 提升训练效率的内在原理: 在训练阶段，由于二叉树是根据预先统计的每个标签数量的占比构造的哈夫曼树 (最优二叉树)，根据哈夫曼树的性质，使得占比最大的标签节点路径最短，又因为路径中的节点代表参数量，也就意味着这种方式需要更新的参数最少，因此提升训练速度。
    - 该方式对模型推断(预测)是否有影响: 在预测阶段，相比全连接层速度略有提升，因为运算参数减少了1/N，N是标签总数。
    - 是否存在一定弊端: 因为最优二叉树的节点中存储参数，而样本数量最多的标签对应的参数又最少，可能出现在某些类别上欠拟合，影响模型准确率。因此，若非存在大量目标类别产生的训练低效，首选具有全连接层的输出层。
  - 2: 参考答案:
    - 首先fasttext工具主要的两大功能就是用来训练词向量和用来文本分类,。
    - 训练的速度提升是主要的原因, 在预测阶段也有速度提升。
    - 迁移词向量, 使模型初始化参数为预训练的参数。
    - 对数据进行增强, 比如原始文本是中文, 一般采用回译数据法, 扩充正负样本的数量。
    - 根据文本分类目标, 还有业务需求等, 可以修改损失函数。(但是这种方法实现难度较高, 一般不采用)





- 考试题5:
  - 参考答案:
  - 1: one-hot, embedding稠密词向量, word2vector等。
  - 2: 学生描述一种或多种skipgram, CBOW等都可以, 还包括fasttext, glove等流行的词向量工具都可以。
  - 3: 不需要人工打标签, 是在一个无监督的场景下构造了一个有监督的任务, 本质上就是有监督的训练。(因为标签label蕴含在文本当中)
  - 4: 包括找近义词, 人工审核, 一词多义等等。或者将词向量用在具体的任务场景下, 比如英译法, 比如文本分类, 查看不同词向量的最终表现的差别来评估。
  - 5: 传统的embedding不能, skipgram和CBOW, fasttext都不能解决一词多义。后续的Elmo, GPT, Bert动态词向量模型才可以。





- 考试题6: 看看学生具体的改进, 优化的点, 准确率等指标的分析。
  - 重在看学生的实践, 分析过程是否详细, 不用过多关注准确率等指标。