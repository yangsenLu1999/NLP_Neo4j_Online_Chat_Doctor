- 作业题1: 
  - 给定一个只含数字的字符串，返回所有合法的IP地址。

```
# coding=utf-8
import numpy as np

def get_all_ip(s, start, part, ip, result):
    length_s = len(s)
    if length_s - start > (4 - part) * 3:
        return

    if length_s - start < (4 - part):
        return

    if start == length_s and part == 4:
        result.append(ip[:-1])
        return

    num = 0
    max_i = np.minimum(start+3, length_s)
    for i in range(start, max_i):
        num = num * 10 + int(s[i])
        if num < 256:
            ip += s[i]
            get_all_ip(s, i+1, part+1, ip+'.', result)
        if num == 0:
            break


def get_ip(s):
    result = []
    ip = ''
    get_all_ip(s, 0, 0, ip, result)
    return result


def main():
    s = '10112'
    res = get_ip(s)
    for i in res:
        print(i)


if __name__ == '__main__':
    main()
```



- 作业题2: 在之前作业的基础上实现股票买卖2.0，给定一个数组，第i个元素代表第i天的股价。假设最多允许进行2次买卖，求可能的最大利润是多少?

  - ```
    # coding=utf-8
    import numpy as np
    
    def get_max_profit(price):
        length = len(price)
        current_profit = [0] * length
        future_profit = [0] * length
        low = price[0]
        for i in range(1, length):
            low = np.minimum(low, price[i])
            current_profit[i] = np.maximum(current_profit[i - 1], price[i] - low)
    
        high = price[length - 1]
        for i in range(length - 2, -1, -1):
            high = np.maximum(high, price[i])
            future_profit[i] = np.maximum(future_profit[i + 1], high - price[i])
    
        max_profit = 0
        for i in range(0, length):
            max_profit = np.maximum(max_profit, current_profit[i] + future_profit[i])
    
        return max_profit
        
    def main():
        price = [68, 72, 59, 73, 66, 63, 59, 72, 65, 70, 64, 75, 71, 70, 67, 70, 72, 66, 63, 59, 68, 73, 74]
        result = get_max_profit(price)
        print(result)
    
    
    if __name__ == '__main__':
        main()
    ```





- 作业题3: 在之前作业的基础上实现蛙跳2.0，给出一维非负元素的数组，每个元素代表该元素位置能够跳的最远距离。假设初始位置在第一个元素，并假设输入数组能满足到达数组末尾，求最少的跳数是多少?

  - ```
    def frog_jump(a):
        result = 0
        last = current = 0
        length = len(a)
        for i in range(length):
            if i > last:
                last = current
                result += 1
            current = max(current, i + a[i])
        
        return result
    
    
    def main():
        a = [2, 1, 3, 1, 1]
        res = frog_jump(a)
        print(res)
    
    if __name__ == '__main__':
        main()
    ```





- 作业题4, 5, 6, 7答案都参考http://52/83/69/131:8989





- 作业题7: 项目代码 + 总结