- 作业题1: 
  - 给定两个数组表示的整数, 返回最接近第二个整数, 并且大于第二个整数的值。

```
# coding=utf-8
import numpy as np

def getclosenumber(x, y):
    sorted_x = sorted(x)
    length = len(x)
    result = []
    used = [False] * length
    for i in range(length):
        j = 0
        while j < length and (used[j] or sorted_x[j] < y[i]):
            j += 1

        used[j] = True
        result.append(sorted_x[j])

        if j == length:
            break

        if sorted_x[j] > y[i]:
            for k in range(length):
                if not used[k]:
                    result.append(sorted_x[k])
            break

    return result
    
def main():
    x = [4, 6, 2, 0, 3, 5]
    y = [5, 3, 2, 4, 1, 0]
    res = getclosenumber(x, y)
    print("res=%s" % res)


if __name__ == '__main__':
    main()
```





- 作业题2: 蛙跳，给出一维非负元素的数组，每个元素代表该元素位置能够跳的最远距离。假设初始位置在第一个元素，请根据输入数组判断是否能跳到数组的末尾。

- ```
  def frog_jump(a):
      i = 0
      length = len(a)
      current_max = 0
      while i < length - 1:
          if a[i] == 0 and current_max < i + 1:
              return False
          if a[i] + i > current_max and a[i] > 0:
              current_max = a[i] + i
              if current_max >= length - 1:
                  return True
          i += 1
  
      return False
  
  
  def main():
      a = [2, 1, 3, 1, 1]
      b = [3, 2, 1, 0, 1]
      res = frog_jump(b)
      print(res)
      res = frog_jump(a)
      print(res)
  
  
  if __name__ == '__main__':
      main()
  ```

  



- 作业题3: 神经网络的训练中如何判断过拟合?如果防止过拟合, 都有哪些办法?请详细说明。
  - 参考答案: 训练集上的指标在提升, 同时验证集上的指标在下降是过拟合最直观的表现。使用Relu, dropout, batchnormalization, 降低网络参数量, 层数, 复杂度等等都可以。





- 作业题4: CRF和HMM的对比
  - 参考答案: 讲义上的两点区别和联系。CRF在预测中使用了维特比算法，叙述一下维特比算法。