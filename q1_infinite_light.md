# Q1：无限之灯，有限之时

“有一盏灯关着，一分钟后闪亮一下，再过半分钟再闪一下，接着每隔上一次一半的时间再次闪亮……请问，两分钟时，灯共闪了多少次？”

她皱着眉认真算着，然后疑惑地问：“难道不会一直闪下去吗？”

其实，这就是“无限趋近”的奇妙。在有限的时间里，可以发生无限多次事件。答案是：**无数次**。

数学上的极限思想，就像孩子的成长，有时是在加速和逼近中悄悄发生的。

让我们用代码画一画这些闪烁发生的时间点：

```python
import matplotlib.pyplot as plt

times = []
t = 1.0
total_time = 2.0
interval = 1.0
while t <= total_time:
    times.append(t)
    interval /= 2
    t += interval

plt.figure(figsize=(8,2))
plt.eventplot(times, orientation='horizontal', colors='blue')
plt.title("灯闪烁的时间点分布")
plt.xlabel("时间（分钟）")
plt.yticks([])
plt.show()
```

> 你能在图里看出“无限逼近”的奥秘吗？