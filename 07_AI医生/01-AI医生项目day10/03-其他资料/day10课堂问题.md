- 问题1: array = [5, 3, 4, 0 ,1, 4, 1]原始数组, 找从第一个元素开始的下降序列。

  - 找到下降序列: descent_seq = [5, 3, 0]
  - 目标是寻找i, j, 现在需要确认这个i的下标一定出现在descent_seq中。
  - 问题是怎么确认这件事? (反证法)
  - 第一个结论: 那么我们一定还能找到一个k, 满足k<i, A[k]<A[i], 
    - 比如A[i] = 4, 这就是最后找到的那个i。
  - 参考代码中 descent_array = ['O', 'O', 'X', 'O', 'X', 'X', 'X']
  - 引申问题: 平时训练模型的代码中用到的那些已经封装好的算法！
    - 1: 大家平时只注意到这个算法能训练, 本质是可收敛。
    - 2: 容易忽略的是这个算法当初在发表论文的时候, 已经证明过它的收敛性了。

- 问题2: 采用将整个数组元素依次执行异或操作，最终的结果值C就是那个唯一出现了一次的数字。

  - 异或: x^y, 相同等于0, 不同等于1, 二进制的层面, 位运算

    - x = 0011010 = 2 + 8 + 16 = 26
    - y = 0111110 = 32 + 16 + 8 + 4 + 2 = 62
    - x^y = 0100100 =  32 + 4 = 36
    - x1 = 0011001
    - y1 = 0011001
    - x1^y1 = 0000000 = 0

  - ```
    def one_number(array):
    		x = array[0]
    		for i in range(1, len(array)):
    				x = array[i] ^ x
    		
    		return x
    ```

  - x = 3, y = 5, x + y = 8 复杂度等效于 x ^ y

  - 异或操作不要求两个相同的值在一起, 因为异或操作满足"交换律"！！！

    - a^b^c = a^c^b

- 问题3: 看网上有用gradient clipping解决梯度消失 这个没理解？

  - 梯度剪裁, clip(gradients, -5, 5), 相当于所有在[-5, 5]区间外的梯度都被剪成-5, 5了, 相当于缩小了梯度范围, 就不会爆炸。
  - 这个技术解决不了梯度消失！！！

- 问题4: CNN处理文本的核心操作.

  - 1: 卷积窗口, [conv_length, embedding_dim], 第一个维度理解为单词的个数, 可以选择2, 3, 4, 5, .....
  - 2: 不同的卷积窗口, 卷积的结果张量映射到对应不同长度的张量结果上。最后进行max_pooling + concat + 求均值。

