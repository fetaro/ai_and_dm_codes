
## 演習 7-1の答え


```python
X = np.array([3,2,1,6,2,4,7])
print((X + 1) ** 2)
```

    [16  9  4 49  9 25 64]


## 演習 7-2の答え


```python
import numpy as np

X = np.array([2,1,3,8,6,7,4])
T = np.array([3,4,7,15,12,15,8])
Y = 2 * X + 1
print(np.mean((Y-T) ** 2))

```

    1.5714285714285714

