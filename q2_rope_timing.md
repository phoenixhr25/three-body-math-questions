# Q2: An Uneven Rope and Nonlinear Time
Q2：不均匀的绳子，非线性的时间

“A rope with uneven thickness takes exactly 1 hour to burn from one end to the other.
Can you use it to measure 15 minutes?”
“一根粗细不均匀的绳子，从一头点燃烧完用一小时。你能否只用它计时15分钟？”

🔍 Algorithmic Insight
This is a recursive time decomposition method:

Use a known time unit (30 min) to define a smaller one (15 min)

Leverages non-uniformity but predictable total duration

Combines parallelism (burning both ends) with sequencing

🧠 Computational Analogy
Think of it like solving problems where:

Time isn’t linearly divisible

You must design operations that leverage total invariants (e.g. fixed total time)

A real-world application might be task pipelining or non-linear decay modeling

Here's how the pattern looks in Python:

```python
import numpy as np
import matplotlib.pyplot as plt

np.random.seed(42)
n = 1000  # 每根绳子分成1000小段
rope1 = np.random.uniform(0.5, 1.5, n)  # 第一根绳子的粗细
rope2 = np.random.uniform(0.5, 1.5, n)  # 第二根绳子的粗细

# 第一根绳子两头点燃
l, r = 0, n - 1
time = 0
while l < r:
    # 每次燃烧两头最细的部分
    min_piece = min(rope1[l], rope1[r])
    time += min_piece / 2  # 两头一起烧
    rope1[l] -= min_piece
    rope1[r] -= min_piece
    if rope1[l] == 0:
        l += 1
    if rope1[r] == 0:
        r -= 1
# 如果剩下中间一段
if l == r:
    time += rope1[l] / 2

first_rope_time = time  # 应为0.5小时，即30分钟

# 第二根绳子一头点燃，同时计时
progress = 0
segment = 0
elapsed = 0
while progress < sum(rope2):
    elapsed += rope2[segment]
    if elapsed >= sum(rope2) / 2:
        # 燃烧到一半（30分钟），开始两头点燃剩余一半
        break
    segment += 1

# 剩余部分的总长
remaining_rope = rope2[segment:]
remaining_length = sum(remaining_rope)
# 这部分用两头点燃，时间再除以2
second_half_time = remaining_length / 2

# 画图
labels = ["0 min", "15 min", "30 min", "45 min", "60 min"]
x = [0, 0.25, 0.5, 0.75, 1]
plt.figure(figsize=(8, 2))
plt.hlines(1, 0, 0.5, colors="red", lw=8, label="First Rope (30 min, both ends)")
plt.hlines(0.8, 0, 0.5, colors="orange", lw=8, label="Second Rope (first half, one end)")
plt.hlines(0.8, 0.5, 0.75, colors="green", lw=8, label="Second Rope (remaining, both ends)")
plt.xticks(x, labels)
plt.ylim(0.7, 1.05)
plt.xlabel("Elapsed Time")
plt.title("How to Measure 15 Minutes with Two Uneven Ropes")
plt.legend()
plt.show()
```
