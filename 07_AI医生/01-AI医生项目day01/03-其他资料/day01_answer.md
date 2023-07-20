- 面试题1: 
  - 给定一个整形数组，是否能找出其中的两个数使得其和为某个指定的值?

```
# coding=utf-8
import numpy as np

def hasSum(array, target):
    sorted_array = sorted(array)
    length = len(sorted_array)
    i, j = (0, length - 1)
    while i < j:
        if sorted_array[i] + sorted_array[j] > target:
            j -= 1
        elif sorted_array[i] + sorted_array[j] < target:
            i += 1
        else:
            break

    if i < j:
        return 1, sorted_array[i], sorted_array[j]
    else:
        return 0, 0, 0


def main():
    array = [11, 7, 45, 67, 134, 5, 83, 55, 106, 33, 57, 82, 6, 24, 87, 61, 3, 39, 6, 26]
    target_number = 46
    result, a, b = hasSum(array, target_number)
    if result == 1:
        print('YES, %d + %d = %d' % (a, b, target_number))
    else:
        print('NO')


if __name__ == '__main__':
    main()
```



- 面试题2: 结构图参照讲义。self-attention用注意力机制可以全局的收集特征, 不必要通过seq2seq的方式顺序收集特征, 这样可以更好的利用远距离信息, 学生的其他理解也可以采纳, 没有固定的正确答案。