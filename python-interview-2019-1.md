## Python开发工程师笔试题

> 答题要求：将该项目从[地址1](<https://github.com/jackfrued/python-interview-2019>)或[地址2](<https://gitee.com/jackfrued/python-interview-2019>)fork到自己的[github]()或[gitee]()仓库并填写答案，完成之后将自己的仓库（public）地址发给面试官即可，答题时间120分钟。

1. 下面的Python代码会输出什么。

   ```Python
   print([(x, y) for x, y in zip('abcd', (1, 2, 3, 4, 5))])
   print({x: f'item{x ** 2}' for x in range(5) if x % 2})
   print(len({x for x in 'hello world' if x not in 'abcdefg'}))
   ```

   答案：

   ```
   生成式： 
   列表 [('a', 1), ('b', 2), ('c', 3), ('d', 4)]
   字典 {1: item1, 3: item9}
   集合 6
   ```

2. 下面的Python代码会输出什么。

   ```Python
   from functools import reduce
   
   items = [11, 12, 13, 14] 
   print(reduce(int.__mul__, map(lambda x: x // 2, filter(lambda x: x ** 2 > 150, items))))
   ```

   答案：

   ```
   过滤 
   ```

3. 有一个通过网络获取数据的Python函数（可能会因为网络或其他原因出现异常），写一个装饰器让这个函数在出现异常时可以重新执行，但尝试重新执行的次数不得超过指定的最大次数。

   答案：

   ```Python
   def try_error(func):
    
    def retry(tires=1, errors=Exception):
    
    def outer(func):
        
        def inner(*args, **kwargs):
            for _ in range(tires):
                try:
            		return func(*args, **kwargs)
                except errors:
                    pass
        return inner
    return outer
   @retry(tires=3)
   def foo()
	   print('xy')
    
   
   ```

4. 下面的字典中保存了某些公司今日的股票代码及价格，用一句Python代码从中找出价格最高的股票对应的股票代码，用一句Python代码创建股票价格大于100的股票组成的新字典。

   > 说明：美股的股票代码是指英文字母代码，如：AAPL、GOOG。

   ```Python
   prices = {
       'AAPL': 191.88,
       'GOOG': 1186.96,
       'IBM': 149.24,
       'ORCL': 48.44,
       'ACN': 166.89,
       'FB': 208.09,
       'SYMC': 21.29
   }
   ```

   答案：

   ```Python
   max(zip(prices.values(), prices.keys()))[1]
   {k:v for k, v in prices.items() if v > 100}
   ```

5. 写一个函数，传入的参数是一个列表，如果列表中的三个元素`a`、`b`、`c`相加之和为`0`，就将这个三个元素组成一个三元组，最后该函数返回一个包含了所有这样的三元组的列表。例如：

   > 参数：`[-1, 0, 1, 2, -1, -4]`
   >
   > 返回：`[(-1, 0, 1), (-1, 2, -1)]`

   答案：
   
   
   ```Python
   from itertools import combinations, permutations(全排列), product(笛卡尔积)
   def foo(nums):
      result= []
      for a, b, c in combinations(num, 3):
         if a + b + c ==0:
            result.append(a, b, c)
      return result
   for x in permutations('abcd', 2)
      print(x)
   
   for x in combinations('abc', 3)
      print(x)
   for x in product('abc', 3)
      print(x)
   
   ```

6. 写一个函数，传入的参数是一个列表（列表中的元素可能也是一个列表），返回该列表最大的嵌套深度，例如：

   > 参数：`[1, 2, 3]`
   >
   > 返回：`1`
   >
   > 参数：`[[1], [2, [3]]]`
   >
   > 返回：`3`

   答案：
   
   ```Python
   递归
   def depth_of_list(items):
      if isinstance(items, list):
         max_depth = 1
         for item in items:
            curr_depth = depth_of_list(item)
            if curr_depth + 1 > max_depth
               max_depth = curr_depth +1
         return max_depth
      return  0
   ```

7. 写一个函数，实现将输入的长链接转换成短链接，每个长链接对应的短链接必须是独一无二的且每个长链接只应该对应到一个短链接，假设短链接统一以`http://t.cn/`开头。例如：给定一个长链接：，会返回形如：的短链接。

   > 参数：`http://jackfrued.xyz/api/users/10001`
   >
   > 返回：`http://t.cn/E6MUth1`

   答案：62进制

   ```Python
   seq_num = 1000000
   url_maps_1 = {}
   # url_maps_2 = {}
   def to)base62(num):
      chars = '0123456789qwertyuioplkjhgfdsazxcvbnmQAZWSXEDCRFVTGBYHNMJUIKLOP'
      result = []
      while num>0:
         result.append(chars[num % 62])
         num //= 62
     return ''.join(reversed(result))
   
   def to_short(url):
      if url in url_maps:
         return url_maps(url)
      global seq_num 
      seq_num += 1
      short_url = f'http://t.cn/to_{base62(seq_num)}'
      url_maps[url]=short_url
      return url_maps
      
   ```

8. 用5个线程，将1~100的整数累加到一个初始值为0的变量上，每次累加时将线程ID和本次累加后的结果打印出来。

    答案：
    ```Python
    枷锁
    from threading import Thread, get_ident, Lock
    from concurrent import ThreadPoolExecutor
    locker = Lock()
    result, i = 0, 1
    def calc():
      global result, i 
      while True:
         with Locker:
            if i> 100:
               break
            result , i = result+i, i +1
            print(get_ident(), result)
    for _ in range(5):
         Thread(tanget=calc).start()
    with ThreadPoolExcutor(max_workers=5) as pool:
         pool.submit(calc)
   ```
9. 请阐述Python是如何进行内存管理的。

    答案：16-20天

    ```
    
    ```

10. 在MySQL数据库中有名为`tb_result`的表如下所示，请写出能查询出如下所示结果的SQL。

    `tb_result`表：

    | rq         | shengfu |
    | ---------- | ------- |
    | 2017-04-09 | 胜      |
    | 2017-04-09 | 胜      |
    | 2017-04-09 | 负      |
    | 2017-04-09 | 负      |
    | 2017-04-10 | 胜      |
    | 2017-04-10 | 负      |
    | 2017-04-10 | 负      |

    查询结果：

    | rq         | 胜   | 负   |
    | ---------- | ---- | ---- |
    | 2017-04-09 | 2    | 2    |
    | 2017-04-10 | 1    | 2    |

    答案：

    ```SQL
    select rq, '胜', '负' from
    (select count(shengfu) from tb_result group by rq)
    group by shengfu;
    ```

11. 列举出你知道的HTTP请求头选项并说明其作用。

     答案：

     ```
   Head: 请求头，请求方法
   User-Agent: 浏览器
   Application: 应用
   Language: 语言
   Accept：接收
   Host: 主机
     ```

12. 阐述Web应用中的Cookie和Session到底有什么区别和联系。

    答案：

    ```
    cookie： cookie是在返回resp的时候把需要保持的东西写入浏览器直接保持起来
    session： session是服务器中
    ```

13. 请阐述访问一个用Django或Flask开发的Web应用，从用户在浏览器中输入网址回车到浏览器收到Web页面的整个过程中，到底发生了哪些事情，越详细越好。

    答案：

    ```
    
    解析网址，url请求服务器，uwsgi请求数据库，返回给服务器，服务器给浏览器响应
    ```

14. 请阐述HTTPS的工作原理，并说明该协议与HTTP之间的区别。

    答案：https阮一峰

    ```
    区别：防止脚本攻击，传输更稳定，有公钥和私钥
    ```

15. 简述你认为新浪微博是如何让订阅者在第一时间获得博主发布的消息。

    答案：场链接推送websocket

    ```
    运用celery做消息队列，轮询所有用户，一个一个发送
    ```

16. 简述如何检查数据库是不是系统的性能瓶颈以及你在工作中是如何优化数据库操作性能的。

    答案：258
    先主从复制，读写分离 dbrouters
    做分布式集群（一主带三从）  
    缓存
    原生sql
    98天nginx集群 
    keepalived双活服务
    ```
    首先查看sql语句是否有多重查询，再查看慢查询日志，再优化（加索引）
    ```

17. 在Linux系统中，假设Nginx的访问日志位于`/var/log/nginx/access.log`，该文件的每一行代表一条访问记录，每一行都由若干列（以制表键分隔）构成，其中第1列记录了访问者的IP地址。请用一条命令找出最近的100000次访问中，访问频率最高的IP地址及访问次数。

    答案：

    ```Shell
    
   tail -100000 /var/log/nginx/access.log | awk (sed) '{print $1}' | sort | uniq -c | sort -nr | head -1
    ```

18. 请阐述跨站脚本攻击（XSS）、跨站身份伪造（CSRF）和SQL注射攻击的原理及防范措施。

    答案：

    ```
    XSS: 
    CSRF: 携带已登录的用户的cookie在另一个网站登录
    SQL: 当以字符串结尾的时候，黑客就可以用字符串拼接的方式，来拼接字符串进行删库操作
    ```
    star法则
    背景
    需求评估
    核心业务的开发和版本迭代
    移动端数据接口的开发和文档编写
