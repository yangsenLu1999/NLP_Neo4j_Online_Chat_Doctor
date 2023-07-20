- 作业题1: 
  - 给定一个整形数组，是否能找出其中的两个数使得其和为某个指定的值?
  
  - 示例: 输入数组为{1, 5, 7, 3}, 指定值为10, 则我们可以从中找出两个数3和7, 和等于10。
  
  - ```
    # 函数调用格式如下
    def main():
        array = [1, 5, 7, 3]
        target_number = 10
        result, a, b = hasSum(array, target_number)
        if result == 1:
            print('YES, %d + %d = %d' % (a, b, target_number))
        else:
            print('NO')
    
    
    if __name__ == '__main__':
        main()
    ```
  
    
  
- 作业题2: 画出Transformer的结构图, 

  - 1: 按照你的理解讲一下原理
  - 2: 为什么self-attention可以替代seq2seq?





- 作业题3: 成功调用起Unit对话API, 并在命令行端启动代码进行3-5轮对话, 将输出效果截图保存提交。





- 作业题4: 

  - 1: 成功启动Flask服务, 并在浏览器端显示出'Hello, World.'并截图保存提交。
  - 2: 成功启动Redis数据库服务, 并用Python代码完成一次(key, value)的对话数据写入+ 读取, 对输出截图保存提交。
  - 3: 成功启动gunicorn服务, 并在后台可以查到对应的pid号, 启动命令和pid号截图保存提交。
  - 4: 成功启动supervisor监控服务, 可以通过命令行端进行start启动进程, stop停止进程的操作, 相关操作截图保存提交。





- 作业题5: 完成当天的知识总结, 按照自己的理解和进度(代码部分自己安排), 总结文件提交。