- 作业题2:股票买卖，给定一个数组，第i个元素代表第i天的股价。假设最多允许进行1次买卖，求可能的最大利润是多少?

- ```
  # coding=utf-8
  import numpy as np
  
  def get_max_profit(price):
      if price is None or len(price) == 0:
          return 0
  
      max_profit = 0
      min_price = price[0]
      length = len(price)
      for i in range(1, length):
          min_price = np.minimum(min_price, price[i])
          max_profit = np.maximum(max_profit, price[i] - min_price)
  
      return max_profit
  
  
  def main():
      price = [68, 72, 59, 73, 66, 63, 59, 72, 65, 70, 64, 75, 71, 70, 67, 70, 72, 66, 63, 59, 68, 73, 74]
      result = get_max_profit(price)
      print(result)
  
  
  if __name__ == '__main__':
      main()
  ```

  



- 作业题3: 

- ```
  假如我们有一个问题: 给出一段文本，使用一些关键词对它进行描述!
  为了方便统一正确答案，这道题可能预先已经给大家写出了一些关键词作为提示.其中这些给出的提示就可以看作是key， 
  而整个的文本信息就相当于是query，value的含义则更抽象，可以比作是你看到这段文本信息后，脑子里浮现的答案信息，
  这里我们又假设大家最开始都不是很聪明，第一次看到这段文本后脑子里基本上浮现的信息就只有提示这些信息，
  因此key与value基本是相同的，但是随着我们对这个问题的深入理解，通过我们的思考脑子里想起来的东西原来越多，
  并且能够开始对我们query也就是这段文本，提取关键信息进行表示.  这就是注意力作用的过程， 通过这个过程，
  我们最终脑子里的value发生了变化，
  根据提示key生成了query的关键词表示方法，也就是另外一种特征表示方法.
  
  ```

- 将注意力计算的公式列举上并解释一下即可。





- 作业题4: 

- ```
  def _some_operations(tx, man_name, woman_name):
      tx.run("MERGE (a:Man{name: $man_name})"
             "MERGE (b:Woman{name: $woman_name})"
             "MERGE (a)-[r:And]-(b)",
             man_name=man_name, woman_name=woman_name)
  
  
  with driver.session() as session:
      session.write_transaction(_some_operations, "Jack", "Lucy")
  ```

- 