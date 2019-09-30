---
layout: post
title: MS Homework 2
subtitle: Homework
#image: /img/2019-08-04_23.18.15.jpg
tags: [Homework]
bigimg: /img/path.jpg
gh-repo: CreatorZZY
gh-badge: [follow]
comments: true
---

第二次作业 - 计算机作图部分
===
熊老师好：
我Python接触没多久，以前用的C系语言，Python用得不好老师你不要见笑。
# 第一道作图题
```python
'''
@Author: George Zhao
@Date: 2019-09-29 21:21:18
@LastEditors: George Zhao
@LastEditTime: 2019-09-29 21:33:53
@Description: Homework2 - 2.
@Email: 2018221138@email.szu.edu.cn
@Company: SZU
@Version: 1.0
'''
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd

def main():
    data_ = [133, 193, 190, 111, 83, 34, 43, 16, 9, 9, 9, 9]
    # 我实在顶不顺了,复杂度高就高吧
    data = list()
    for i in range(12):
        val = data_[i]
        for _ in range(val):
            data.append(i/5+0.1)
    
    print("Tol: 839")
    plt.title('Title')
    plt.xlabel('Content')
    plt.ylabel('Times')
    plt.hist(x= data,bins = np.arange(0,2.3,0.2),rwidth=0.8)
    plt.savefig("2.png",format='png')

if __name__ == "__main__":
    main()

```
![2](/img/2019-09-29-MS-Homework-2/2.png)

# 第二道作图题
```python
'''
@Author: George Zhao
@Date: 2019-09-29 23:21:18
@LastEditors: George Zhao
@LastEditTime: 2019-09-29 23:33:10
@Description: Homework2 - 3.
@Email: 2018221138@email.szu.edu.cn
@Company: SZU
@Version: 1.0
'''
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd

def main():
    age = [x for x in range(40, 81, 5)]
    Male = [4.4, 7.2, 7.3, 6.9, 19.3, 50.2, 68.5, 86.2, 97.0]
    Female = [2.1, 3.3, 4.5, 5.5, 6.7, 16.4, 12.5, 19.9, 15.2]
    plt.plot(age, Male, "r--")
    plt.plot(age, Female, "b--")
    plt.title('Title')
    plt.xlabel('Age')
    plt.ylabel('Per')
    plt.savefig("3.png", format='png')
    plt.clf()
    Male_log = [np.log(x) for x in Male]
    Female_log = [np.log(x) for x in Female]
    plt.plot(age, Male_log, "r--")
    plt.plot(age, Female_log, "b--")
    plt.title('Title')
    plt.xlabel('Age')
    plt.ylabel('Per_log')
    plt.savefig("4.png", format='png')

if __name__ == "__main__":
    main()
```
![3](/img/2019-09-29-MS-Homework-2/3.png)

![4](/img/2019-09-29-MS-Homework-2/4.png)
说明了，率是随着年龄的增长是呈现出一种指数增长，而并非单纯的线性增长。

另外，男性的发病率显著比 女性要高，而且被指数效应放大。
这个可以用拿线性回归回归完之后有个y=ax+b+ε的数学模型中的ε只要两者ε是满足同一个分布律来尝试证明。当然前提是（a男>=a女 | b男>=b女）。