
# NumPy的ndarray: 一种多维数组对象

## 创建ndarray

### array 函数创建


```python
import numpy as np
```


```python
data1 = [6,7.5,8,0,1]
arr1 = np.array(data1)
arr1
```




    array([6. , 7.5, 8. , 0. , 1. ])



### 嵌套序列


```python
data2 = [[1,2,3,4],[5,6,7,8]]
arr2 = np.array(data2)
arr2
```




    array([[1, 2, 3, 4],
           [5, 6, 7, 8]])




```python
arr2.ndim
```




    2




```python
arr2.shape
```




    (2, 4)




```python
print(arr1.dtype,arr2.dtype)
```

    float64 int32
    

### 其它函数


```python
np.zeros(10)
```




    array([0., 0., 0., 0., 0., 0., 0., 0., 0., 0.])




```python
np.ones((3,6))
```




    array([[1., 1., 1., 1., 1., 1.],
           [1., 1., 1., 1., 1., 1.],
           [1., 1., 1., 1., 1., 1.]])




```python
np.empty((2,3,2))
```




    array([[[1.46268009e-311, 3.16202013e-322],
            [0.00000000e+000, 0.00000000e+000],
            [1.33511969e-306, 2.31746027e-052]],
    
           [[9.28204515e-072, 1.86454635e+160],
            [1.60399042e-051, 1.85586081e-051],
            [6.52077860e-038, 4.27632616e-033]]])




```python
np.arange(15)
```




    array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14])



## ndarray的数据类型

### dtype


```python
arr1 = np.array([1,2,3],dtype=np.float64)
arr2 = np.array([1,2,3],dtype=np.int32)
print(arr1.dtype,arr2.dtype)
```

    float64 int32
    

### astype


```python
arr = np.array([1,2,3,4,5])
print(arr.dtype)

float_arr = arr.astype(np.float32)
print(float_arr.dtype)
```

    int32
    float32
    

## 数组和标量之间的运算


```python
arr = np.array([[1,2,3],[4,5,6]])
arr
```




    array([[1, 2, 3],
           [4, 5, 6]])




```python
arr*arr
```




    array([[ 1,  4,  9],
           [16, 25, 36]])




```python
1/arr
```




    array([[1.        , 0.5       , 0.33333333],
           [0.25      , 0.2       , 0.16666667]])



## 基本的索引和切片


```python
arr = np.arange(10)
arr
```




    array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])




```python
arr[5]
```




    5




```python
arr[5:8]
```




    array([5, 6, 7])




```python
arr[5:8]=12
arr
```




    array([ 0,  1,  2,  3,  4, 12, 12, 12,  8,  9])




```python
arr_slice = arr[5:8]
arr_slice[1] = 12345
arr
```




    array([    0,     1,     2,     3,     4,    12, 12345,    12,     8,
               9])




```python
arr_slice[:]=64
arr
```




    array([ 0,  1,  2,  3,  4, 64, 64, 64,  8,  9])




```python
arr2d = np.array([[1,2,3],[4,5,6],[7,8,9]])
arr2d
```




    array([[1, 2, 3],
           [4, 5, 6],
           [7, 8, 9]])




```python
arr2d[2]
```




    array([7, 8, 9])




```python
arr2d[2][1]
```




    8




```python
arr2d[2,1]
```




    8



## 切片索引


```python
arr[1:6]
```




    array([ 1,  2,  3,  4, 64])




```python
arr2d
```




    array([[1, 2, 3],
           [4, 5, 6],
           [7, 8, 9]])




```python
arr2d[:2]
```




    array([[1, 2, 3],
           [4, 5, 6]])




```python
arr2d[:2,1:]
```




    array([[2, 3],
           [5, 6]])



## 布尔型索引


```python
names = np.array(['Bob','Joe','Will','Bob','Will','Joe','Joe'])
names
```




    array(['Bob', 'Joe', 'Will', 'Bob', 'Will', 'Joe', 'Joe'], dtype='<U4')




```python
data = np.random.randn(7,4)
data
```




    array([[-0.45087179,  0.95959909, -1.1507511 ,  0.57504121],
           [-0.63651958,  0.4646842 ,  1.19323906,  2.17561511],
           [-0.90224968, -1.33174767,  0.35437275,  0.46909408],
           [ 0.05625285,  0.82508478, -0.61066097,  0.21289136],
           [ 1.05920379, -0.6029447 , -0.69286011,  0.79485695],
           [ 0.78852535, -1.13555996,  0.58967264, -0.29439058],
           [ 1.16155404,  1.47606197, -0.98348904,  0.30604953]])




```python
names == 'Bob'
```




    array([ True, False, False,  True, False, False, False])




```python
data[names=='Bob']
```




    array([[-0.45087179,  0.95959909, -1.1507511 ,  0.57504121],
           [ 0.05625285,  0.82508478, -0.61066097,  0.21289136]])




```python
data[names=='Bob',:2]
```




    array([[-0.45087179,  0.95959909],
           [ 0.05625285,  0.82508478]])




```python
mask = (names=='Bob')|(names=='Will')
mask
```




    array([ True, False,  True,  True,  True, False, False])




```python
data[data<0]=0
data
```




    array([[0.        , 0.95959909, 0.        , 0.57504121],
           [0.        , 0.4646842 , 1.19323906, 2.17561511],
           [0.        , 0.        , 0.35437275, 0.46909408],
           [0.05625285, 0.82508478, 0.        , 0.21289136],
           [1.05920379, 0.        , 0.        , 0.79485695],
           [0.78852535, 0.        , 0.58967264, 0.        ],
           [1.16155404, 1.47606197, 0.        , 0.30604953]])




```python
data[names!='Joe']=7
data
```




    array([[7.        , 7.        , 7.        , 7.        ],
           [0.        , 0.4646842 , 1.19323906, 2.17561511],
           [7.        , 7.        , 7.        , 7.        ],
           [7.        , 7.        , 7.        , 7.        ],
           [7.        , 7.        , 7.        , 7.        ],
           [0.78852535, 0.        , 0.58967264, 0.        ],
           [1.16155404, 1.47606197, 0.        , 0.30604953]])



## 花式索引


```python
arr = np.empty([8,4])
for i in range(8):
    arr[i] = i 
arr
```




    array([[0., 0., 0., 0.],
           [1., 1., 1., 1.],
           [2., 2., 2., 2.],
           [3., 3., 3., 3.],
           [4., 4., 4., 4.],
           [5., 5., 5., 5.],
           [6., 6., 6., 6.],
           [7., 7., 7., 7.]])




```python
arr[[4,3,0,6]]
```




    array([[4., 4., 4., 4.],
           [3., 3., 3., 3.],
           [0., 0., 0., 0.],
           [6., 6., 6., 6.]])




```python
arr = np.arange(32).reshape((8,4))
arr
```




    array([[ 0,  1,  2,  3],
           [ 4,  5,  6,  7],
           [ 8,  9, 10, 11],
           [12, 13, 14, 15],
           [16, 17, 18, 19],
           [20, 21, 22, 23],
           [24, 25, 26, 27],
           [28, 29, 30, 31]])




```python
arr[[1,5,7,2],[3,2,1,0]]
```




    array([ 7, 22, 29,  8])




```python
arr[[1,5,7,2]][:,[3,2,1,0]]
```




    array([[ 7,  6,  5,  4],
           [23, 22, 21, 20],
           [31, 30, 29, 28],
           [11, 10,  9,  8]])




```python
arr[np.ix_([1,5,7,2],[3,2,1,0])]
```




    array([[ 7,  6,  5,  4],
           [23, 22, 21, 20],
           [31, 30, 29, 28],
           [11, 10,  9,  8]])



## 数组转置和轴对换


```python
arr = np.arange(15).reshape((3,5))
arr
```




    array([[ 0,  1,  2,  3,  4],
           [ 5,  6,  7,  8,  9],
           [10, 11, 12, 13, 14]])




```python
arr.T
```




    array([[ 0,  5, 10],
           [ 1,  6, 11],
           [ 2,  7, 12],
           [ 3,  8, 13],
           [ 4,  9, 14]])




```python
arr = np.random.randn(6,3)
np.dot(arr.T,arr)
```




    array([[ 8.50170961, -2.41167809,  0.95396673],
           [-2.41167809,  7.15906783, -2.35714638],
           [ 0.95396673, -2.35714638,  3.95845294]])



# 通用函数：快速的元素级数组函数


```python
arr = np.arange(10)
arr
```




    array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])




```python
np.sqrt(arr)
```




    array([0.        , 1.        , 1.41421356, 1.73205081, 2.        ,
           2.23606798, 2.44948974, 2.64575131, 2.82842712, 3.        ])




```python
np.exp(arr)
```




    array([1.00000000e+00, 2.71828183e+00, 7.38905610e+00, 2.00855369e+01,
           5.45981500e+01, 1.48413159e+02, 4.03428793e+02, 1.09663316e+03,
           2.98095799e+03, 8.10308393e+03])




```python
x = np.random.randn(8)
y = np.random.randn(8)
x,y
```




    (array([ 0.80455581,  0.04626711, -0.38618932,  0.60021361,  0.54400187,
            -0.60285687, -1.58655449, -0.22322289]),
     array([ 1.15682961, -0.15680231, -0.07089371, -2.88841229, -1.0299903 ,
            -0.12694929, -0.51279952,  1.13611007]))




```python
np.maximum(x,y)
```




    array([ 1.15682961,  0.04626711, -0.07089371,  0.60021361,  0.54400187,
           -0.12694929, -0.51279952,  1.13611007])



# 利用数组进行数据处理


```python
points = np.arange(-5,5,0.01)

```


```python
xs,ys = np.meshgrid(points,points)# 接受两个一维数组，并产生两个二维矩阵
ys
```




    array([[-5.  , -5.  , -5.  , ..., -5.  , -5.  , -5.  ],
           [-4.99, -4.99, -4.99, ..., -4.99, -4.99, -4.99],
           [-4.98, -4.98, -4.98, ..., -4.98, -4.98, -4.98],
           ...,
           [ 4.97,  4.97,  4.97, ...,  4.97,  4.97,  4.97],
           [ 4.98,  4.98,  4.98, ...,  4.98,  4.98,  4.98],
           [ 4.99,  4.99,  4.99, ...,  4.99,  4.99,  4.99]])




```python
import matplotlib.pyplot as plt

z = np.sqrt(xs**2 +ys**2)
z
```




    array([[7.07106781, 7.06400028, 7.05693985, ..., 7.04988652, 7.05693985,
            7.06400028],
           [7.06400028, 7.05692568, 7.04985815, ..., 7.04279774, 7.04985815,
            7.05692568],
           [7.05693985, 7.04985815, 7.04278354, ..., 7.03571603, 7.04278354,
            7.04985815],
           ...,
           [7.04988652, 7.04279774, 7.03571603, ..., 7.0286414 , 7.03571603,
            7.04279774],
           [7.05693985, 7.04985815, 7.04278354, ..., 7.03571603, 7.04278354,
            7.04985815],
           [7.06400028, 7.05692568, 7.04985815, ..., 7.04279774, 7.04985815,
            7.05692568]])




```python
plt.imshow(z,cmap=plt.cm.gray)
plt.colorbar()
plt.title('Image plot of $\sqrt{x^2 +y^2}$ for a grid of values')
```




    Text(0.5,1,'Image plot of $\\sqrt{x^2 +y^2}$ for a grid of values')




![png](output_70_1.png)


## 将条件逻辑表述为数组运算


```python
xarr = np.array([1.1,1.2,1.3,1.4,1.5])
yarr = np.array([2.1,2.2,2.3,2.4,2.5])
cond = np.array([True,False,True,True,False])

result = [(x if c else y) for x,y,c in zip(xarr,yarr,cond)]
result
```




    [1.1, 2.2, 1.3, 1.4, 2.5]




```python
result = np.where(cond,xarr,yarr)
result
```




    array([1.1, 2.2, 1.3, 1.4, 2.5])




```python
arr = np.random.randn(4,4)
arr
```




    array([[ 1.52136069, -0.87273412, -0.62702601, -0.09222936],
           [ 0.14238153, -0.10676843,  0.4116277 ,  0.11858751],
           [-0.42049253, -0.04327179, -3.030477  , -0.76130805],
           [ 0.28145745,  1.08549125, -0.17710349, -1.62434259]])




```python
np.where(arr>0,2,-2)
```




    array([[ 2, -2, -2, -2],
           [ 2, -2,  2,  2],
           [-2, -2, -2, -2],
           [ 2,  2, -2, -2]])



## 数学和统计方法


```python
arr = np.random.randn(5,4)
arr
```




    array([[ 1.98184531, -1.31031762, -0.40928628, -1.31108334],
           [-2.56837876, -0.73823337, -0.01346733, -0.28437   ],
           [-0.7019003 , -0.91232474,  1.57505169,  0.3533256 ],
           [ 0.11617622, -0.55885896, -0.57719704,  0.45029594],
           [-0.40761255, -0.16395479,  1.15379737, -0.60458239]])




```python
arr.mean()
```




    -0.2465537664298915




```python
arr.sum()
```




    -4.93107532859783




```python
np.mean(arr,axis = 0)#列的平均
```




    array([-0.31597401, -0.73673789,  0.34577968, -0.27928284])




```python
np.mean(arr,axis = 1)#行的平均
```




    array([-0.26221048, -0.90111236,  0.07853806, -0.14239596, -0.00558809])



## 用于布尔型数组的方法


```python
arr = np.random.randn(100)
(arr>0).sum()
```




    50




```python
bools = np.array([False,False,True,True])
bools.any() #测试数组中是否存在一个或多个True
bools.all() #检查数组中所有值是否都是True
```




    False



## 排序


```python
arr = np.random.randn(8)
arr
```




    array([ 1.19567235,  0.26870644,  1.74672574,  0.02618487, -0.91736138,
           -0.07414401, -0.9797643 ,  1.09266402])




```python

arr
```




    array([-0.9797643 , -0.91736138, -0.07414401,  0.02618487,  0.26870644,
            1.09266402,  1.19567235,  1.74672574])




```python

```


```python
arr = np.random.randn(5,3)
arr.sort(1)
arr
```




    array([[-0.81088228,  1.08226128,  1.64117031],
           [-0.78324249, -0.16481292,  1.75523044],
           [-1.51297216,  0.99313952,  1.49405113],
           [-0.30029775,  0.41671417,  1.48313768],
           [-0.27056867,  0.32788967,  0.75985025]])




```python
arr = np.arange(10)
np.save('some_array',arr)
```


```python
np.load('some_array.npy')
```




    array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])



# 线性代数


```python
x = np.array([[1,2,3],[4,5,6]])
y = np.array([[6,23],[-1,7],[8,9]])
x
```




    array([[1, 2, 3],
           [4, 5, 6]])




```python
y
```




    array([[ 6, 23],
           [-1,  7],
           [ 8,  9]])




```python
x.dot(y)
```




    array([[ 28,  64],
           [ 67, 181]])




```python
np.dot(x,y)
```




    array([[ 28,  64],
           [ 67, 181]])




```python

```
