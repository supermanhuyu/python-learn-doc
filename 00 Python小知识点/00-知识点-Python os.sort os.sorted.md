### sort or sorted ?

```
sort 与 sorted 区别：

sort 是应用在 list 上的方法，sorted 可以对所有可迭代的对象进行排序操作。

list 的 sort 方法返回的是对已经存在的列表进行操作，而内建函数 sorted 方法返回的是一个新的 list，而不是在原来的基础上进行的操作。
```



### list.sorted的用法

```python



sorted(iterable)
----------------------------------------------------------------------------------
>>>a = [5,7,6,3,4,1,2]
>>> b = sorted(a)       # 保留原列表
>>> a 
[5, 7, 6, 3, 4, 1, 2]
>>> b
[1, 2, 3, 4, 5, 6, 7]
----------------------------------------------------------------------------------

sorted(iterable, cmp)
sorted(iterable, key)
sorted(iterable, cmp, key)
sorted(iterable, cmp, key, reverse=False)

----------------------------------------------------------------------------------
>>> L=[('b',2),('a',1),('c',3),('d',4)]
>>> sorted(L, cmp=lambda x,y:cmp(x[1],y[1]))   # 利用cmp函数
[('a', 1), ('b', 2), ('c', 3), ('d', 4)]
>>> sorted(L, key=lambda x:x[1])               # 利用key
[('a', 1), ('b', 2), ('c', 3), ('d', 4)]

>>> students = [('john', 'A', 15), ('jane', 'B', 12), ('dave', 'B', 10)]
>>> sorted(students, key=lambda s: s[2])            # 按年龄排序
[('dave', 'B', 10), ('jane', 'B', 12), ('john', 'A', 15)]
 
>>> sorted(students, key=lambda s: s[2], reverse=True)       # 按降序
[('john', 'A', 15), ('jane', 'B', 12), ('dave', 'B', 10)]
----------------------------------------------------------------------------------


```

### 与list.sort 的使用

```
sort(self, key=None, reverse=False)

if __name__ == '__main__':

    a = [5, 7, 6, 3, 4, 1, 2]
    b = [('dave', 'B', 10), ('jane', 'B', 12), ('john', 'A', 15)]
    a.sort(reverse=True)
    print(a)
    b.sort(key=lambda x:x[0])
    print(b)
```

