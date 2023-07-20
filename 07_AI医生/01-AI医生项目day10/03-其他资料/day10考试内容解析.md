- 考试题1: 
  
  - 给定一个整形数组, 找出最大下标距离 j - i , 当且仅当 A[i] < A[j] 和 i < j 
  
  - ```
    算法思路: 记录从数组第一个元素开始的下降序列descent_seq, 然后使用指针从尾部开始逆向扫描, 求出满足要求的下标的最大距离。
    
    反证法: 假设存在最大下标距离的两个下标i和j, 满足i<j, A[i]<A[j], 并且A[i]不在descent_seq中。
           如果上述假设情况发生, 那么我们一定还能找到一个k, 满足k<i, A[k]<A[i], 那么此时最大下标距离应该是j-k, 而不是j-i, 矛盾! 因此假设不成立!
           得出结论: 满足要求的A[i]一定在descent_seq中, 也就是一定在从数组第一个元素开始的下降序列中。
    ```

```
# coding=utf-8

def maxDistance(array):
    descent_array = []
    max_number = array[0]
    for i in range(len(array)):
        if i == 0:
            descent_array.append('O')
        else:
            if array[i] < max_number:
                descent_array.append('O')
                max_number = array[i]
            else:
                descent_array.append('X')

    print(descent_array)

    i = j = len(descent_array) - 1
    max_distance = 0
    max_i = -1
    max_j = -1
    while i >= 0:
        if descent_array[i] == 'X':
            i -= 1
            continue

        while array[j] <= array[i] and i < j:
            j -= 1

        if i < j and j - i > max_distance:
            max_distance = j - i
            max_i = i
            max_j = j

        i -= 1

    return max_distance, max_i, max_j


def main():
    array = [5, 3, 4, 0 ,1, 4, 1]
    dis, a, b = maxDistance(array)
    print("dis=%d, start=%d, end=%d" % (dis, a, b))


if __name__ == '__main__':
    main()
```





- 考试题2: 在一维数组中，找出一个点，使得其所有左边的数字均小于等于它，所有右边的数字都大于等于它。返回这个点所在的下标，要求你的算法时间复杂度为O(n)。

  - ```
    # 从左向右扫描一遍, 记录任意位置i的数字a[i]是否满足左边的所有数字都小于等于它, 满足的话用flag标记。再从右向左扫描一遍, 记录任意位置i的数字a[i]是否满足右边的所有数字都大于等于它, 满足的话最后判断一下刚才的flag标记是都等于1, 这样的i就是解。
    
    def get_point_number(a):
        length = len(a)
        result = []
        flag = [0] * length
        first_max = a[0]
        for i in range(0, length):
            if a[i] >= first_max:
                first_max = a[i]
                flag[i] = 1
        second_min = a[-1]
        for i in range(length - 1, -1, -1):
            if a[i] <= second_min:
                second_min = a[i]
                if flag[i] == 1:
                    result.append(i)
    
        return result
    
    
    def main():
        a = [1, 0, 1, 0, 1, 2, 3]
        res = get_point_number(a)
        print(res)
    
    if __name__ == '__main__':
        main()
    ```







- 考试题3: Softmax反向传播的推导.

  - ![WechatIMG1](/Users/zhudejun/Desktop/2020-05-09 -- 直播课/WechatIMG1.jpeg)
  
  







- 考试题4.1 : fasttext模型在大量类别上能够快速训练的原因?(从模型结构上深入分析)
- 参考答案:
  - 1:fasttext模型是结构简单，仅由Embedding层，GAP层和输出层组成，适用于大规模文本分类的高效选择之一。使用n-gram特征，层次softmax是fasttext模型的两大显著特征。
  - 2: 模型结构简单，参数量相比大型模型(如BERT)较少，即提高训练效率又提高推断效率。
  - 3: 当业务场景中存在大量目标类别时，fasttext的输出层使用层次softmax提升训练效率。
  - 4: 关于层次softmax
    - 4.1: 层次softmax是一种使用最优二叉树结构替代网络原有输出层(全连接层)的方式。
    - 4.2: 提升训练效率的内在原理: 在训练阶段，由于二叉树是根据预先统计的每个标签数量的占比构造的哈夫曼树（最优二叉树），根据哈夫曼树的性质，使得占比最大的标签节点路径最短，又因为路径中的节点代表参数量，也就意味着这种方式需要更新的参数最少，因此提升训练速度。
    - 4.3: 该方式对模型推断(预测)是否有影响: 在预测阶段，相比全连接层速度略有提升，因为运算参数减少了1/N，N是标签总数。
    - 4.4: 是否存在一定弊端: 因为最优二叉树的节点中存储参数，而样本数量最多的标签对应的参数又最少，可能出现在某些类别上欠拟合，影响模型准确率。因此，若非存在大量目标类别产生的训练低效，首选具有全连接层的输出层。





- 考试题4.2 : 为了提升fasttext模型的评估指标都做了哪些优化?
- 参考答案:
  - 1: 迁移词向量，使模型初始化的参数为迁移参数。
  - 2: 对数据进行增强，对于中文文本数据，一般是选择回译增强法，扩充正负样本的数量。
  - 3: 根据文本分类目标和业务要求修改损失函数（这种方法实现难度较大，一般不采用) 。
- 备选答案(建议学生背下来的说法): 
  - 在项目中，我们首先使模型初始化参数为迁移参数，这样我们的模型训练时，起始的验证准确率由原来的50%提升至63%，最终准确率也提升了大概7%。而且我们还对正负样本数据分别进行回译增强，在原有的数据集基础上，我们分别上采样了正负样本各1000条，有效扩展了数据特征维度，将验证准确率由之前的87%提升至90%。







- 考试题5 : 
  - 1: 关于Bert的模型架构.
  - ![BERT](/Users/zhudejun/Desktop/2020-05-09 -- 直播课/BERT.png)
  - ![BERT2](/Users/zhudejun/Desktop/2020-05-09 -- 直播课/BERT2.png)
  - 2: 关于Bert训练过程中的关键点.
    - 2.1: 四大关键词: Pre-trained, Deep, Bidirectional Transformer, Language Understanding
      - a: Pre-trained: 首先明确这是一个预训练的语言模型, 未来所有的开发者可以直接继承!
        - 整个Bert模型最大的两个亮点都集中在Pre-trained的任务部分。
      - b: Deep: 
        - Bert_BASE: Layer = 12, Hidden = 768, Head = 12, Total Parameters = 110M
        - Bert_LARGE: Layer = 24, Hidden = 1024, Head = 16, Total Parameters = 340M
        - 对比于Transformer: Layer = 6, Hidden = 2048, Head = 8, 是一个浅而宽, 说明Bert这样深而窄的模型效果更好 (和CV领域的总体结论基本一致)。
      - c: Bidirectional Transformer: Bert的一个创新点, 它是一个双向的Transformer网络。
        - 原始的Transformer其实是一个单向的网络, 和GPT一致, 见上图。
      - d: Language Understanding: 更加侧重语言的理解, 而不仅仅是生成 (Language Generation)
    - 2.2: Bert的语言输入表示包含了3个组成部分: (见上图)
      - 词嵌入张量: word embeddings
      - 语句分块张量: segmentation embeddings
      - 位置编码张量: position embeddings
    - 2.3: Bert的预训练中引入两大核心任务 (这两个任务也是Bert原始论文的两个最大的创新点)
      - a: 引入 Masked LM (带mask的语言模型训练)
        - a.1: 在原始训练文本中, 随机的抽取15%的token作为即将参与mask的对象。
        - a.2: 在这些被选中的token中, 数据生成器并不是把他们全部变成[MASK], 而是有下列3个选择:
          - a.2.1: 在80%的概率下, 用[MASK]标记替换该token, 比如my dog is hairy -> my dog is [MASK]
          - a.2.2: 在10%的概率下, 用一个随机的单词替换该token, 比如my dog is hairy -> my dog is apple
          - a.2.3: 在10%的概率下, 保持该token 不变, 比如my dog is hairy -> my dog is hairy
        - a.3: Transformer Encoder在训练的过程中, 并不知道它将要预测哪些单词? 哪些单词是原始的样子? 哪些单词被遮掩成了[MASK]? 哪些单词被替换成了其他单词? 正是在这样一种高度不确定的情况下, 反倒逼着模型快速学习该token的分布式上下文的语义, 尽最大努力学习原始语言说话的样子!!! 同时因为原始文本中只有15%的token参与了MASK操作, 并不会破坏原语言的表达能力和语言规则!!!
      - b: 引入Next Sentence Prediction (下一句话的预测任务)
        - b.1: 目的是为了服务问答, 推理, 句子主题关系等NLP任务。
        - b.2: 所有的参与任务训练的语句都被选中参加。
          - 50%的B是原始文本中实际跟随A的下一句话。(标记为IsNext, 代表正样本)
          - 50%的B是原始文本中随机抽取的一句话。(标记为NotNext, 代表负样本)
        - b.3: 在该任务中, Bert模型可以在测试集上取得97-98%的准确率。
    - 2.4: 关于基于Bert的模型微调(fine-tuning)
      - 只需要将特定任务的输入, 输出插入到Bert中, 利用Transformer强大的注意力机制就可以模拟很多下游任务。(句子对关系判断, 单文本主题分类, 问答任务(QA), 单句贴标签(命名实体识别))
      - 微调的若干经验:
        - batch size: 16, 32
        - epochs: 3, 4
        - learning rate: 2e-5, 5e-5
        - 全连接层添加: layers: 1-3, hidden_size: 64, 128
      - ![BERT3](/Users/zhudejun/Desktop/2020-05-09 -- 直播课/BERT3.png)
  - 3: Bert模型本身的优点和缺点。(没有标准答案)
    - 优点: Bert的基础建立在transformer之上, 拥有强大的语言表征能力和特征提取能力。在11项NLP基准测试任务中达到了state of the art。同时再一次证明了双向语言模型的能力更加强大。
    - 缺点: 
      - 1: 可复现性差, 基本没法做, 只能拿来主义直接用!
      - 2: 训练过程中因为每个batch_size中的数据只有15%参与预测, 模型收敛较慢, 需要强大的算力支撑!
    - 引申:
      - 1：深度学习就是表征学习 (Deep learning is representation learning)
        - 整个Bert在11项语言模型大赛中, 基本思路就是双向Transformer负责提取特征, 然后整个网络加一个全连接线性层作为fine-tuning微调。但即便如此傻瓜式的组装, 在NLP中著名的难任务-NER(命名实体识别)中, 甚至直接去除掉了CRF层, 照样大大超越BiLSTM + CRF的组合效果, 这去哪儿说理去???
      - 2: 规模的极端重要性 (Scale matters)
        - 不管是Masked LM, 还是下一句预测Next Sentence Prediction, 都不是首创的概念, 之前在其他的模型中也提出过, 但是因为数据规模 + 算力局限没能让世人看到这个模型的潜力, 那些Paper也就不值钱了。但是到了谷歌手里, 不差钱的结果就是Paper值钱了!!!!!!
      - 3: 关于进一步的研究展示了Bert在不同的层学习到了什么。
        - 低的网络层捕捉到了短语结构方面的信息。
        - 单词和字的特征表现在3-4层, 句法信息的特征表现在6-9层, 句子语义信息的特征表现在10-12层。
        - 主谓一致的特征表现在8-9层 (属于句法信息的一种)。







- 考试题6: 按照讲义上的课程内容理解就好, 主要是为了在BiLSTM上面增加一层约束机制(这个约束就是CRF)。
  - 关于forward()函数: 这个涉及到Pytorch的代码机制, 不是必须要用到forward(), 可以完全不用。









- 考试题7: 这个模型存在的意义就是判断用户和医生的连续对话是不是围绕同一个主题的。利用Bert省时省力, 当然也可以自定义一个训练模型来得到结果。









- 考试题8: 传统的seq2seq架构有独立的Encoder和Decoder, 编码器端的结果是一个唯一的语义张量, 不利于解码器端应用注意力机制。采用transformer进行改进后, 会有巨大的提升。







- 附加题1: 关于文本摘要, 首先要明确这也是一个"生成式任务"!
  - 训练数据: x: 一段文本, label: 该段文本的摘要
  - seq2seq, transformer都可以!!!
  - 需要同学们未来补充的1个知识: PGN(Pointer Generator Networks)
    - 本质上是为了防止对原文本大量的抽取extraction, 而不是生成generation!!!





- 附加题2: 同学给出模型架构的解释3分, 给出代码再加3分, 如果能给出可运行的transformer代码, 给满10分。