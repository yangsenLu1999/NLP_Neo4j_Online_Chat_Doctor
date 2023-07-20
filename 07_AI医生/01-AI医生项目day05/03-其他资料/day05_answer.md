- 作业题1: 
  - 给定一个整形数组, 找出最大下标距离 j - i , 当且仅当 A[i] < A[j] 和 i < j 。

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



- 作业题2:  给定一个一维数组，里面只有一个数字出现了一次，其他数字都出现了2次，请将这个唯一出现了一次的数字找出来。

- ```
  采用将整个数组元素依次执行异或操作，最终的结果值C就是那个唯一出现了一次的数字。 异或操作满足交换律  a^b^c=a^c^b
  ```

  





- 作业题3: RNN相关问题
  - 4: 关于采用CNN来处理文本, 需要考虑的是卷积核的大小设置, 只能设为[conv_length, sequence_length], 第一个维度为卷积尺寸, 可以是2, 3, 4这样的值, 但是第二个维度必须和数字化张量的第二个维度匹配, 即等于sequence_length。其他的处理步骤和RNN基本一致。





- 作业题4: 项目代码+总结