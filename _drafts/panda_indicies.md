# Panda Indicies

## Basic loc and iloc

use `loc` to look based on index and `iloc` for offsets.

```python

```

# Duplicates

Indices can contains duplicates.

```python
df = pd.DataFrame({
    "a": [1, 2, 3],
     "i": [1, 1, 2]
})
   a  i
0  1  1
1  2  1
2  3  2

df.set_index("i")
i   
1  1
1  2
2  3
```





## Composites

## Ranged indexes