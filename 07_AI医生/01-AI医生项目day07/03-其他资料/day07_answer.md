- 作业题1: 输入一个递增有序数组的一个旋转，输出旋转数组的最小值。
  
  - ```
    def get_min_value(a):
        left = 0
        right = len(a) - 1
        min_value = a[left]
        while left < right:
            mid = int(left + (right - left) / 2)
            min_value = min(a[left], min_value)
            if (a[mid] == a[left]) and (a[mid] == a[right]):
                left += 1
            elif a[mid] >= a[left]:
                left = mid + 1
                min_value = min(a[left], min_value)
            else:
                min_value = min(a[mid], min_value)
                right = mid - 1
    
        return min_value
    
    
    def main():
        a = [3, 4, 5, 6, 1, 2]
        res = get_min_value(a)
        print('res=%d' % res)
    
    
    if __name__ == '__main__':
        main()
    ```





- 作业题2: 
  - 参考答案: http://52.83.69.131:8989有详细解答





- 作业题3: 相关的总结, 开放性。