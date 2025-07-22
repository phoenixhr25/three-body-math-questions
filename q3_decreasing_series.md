# Q3：“82, 50, 26 — what’s the next number?”
递减的数列，隐藏的规律

“82, 50, 26 — what’s the next number?”
“82，50，26，下一个数是多少？”

```
sequence = [82, 50, 26, 10]
first_diff = [sequence[i+1] - sequence[i] for i in range(len(sequence)-1)]
print("First differences:", first_diff)
```
