# Pytorch

### numpy 转到 torch

```
numpy_tensor = np.random.randn(10, 20)
pytorch_tensor1 = torch.Tensor(numpy_tensor)
pytorch_tensor2 = torch.from_numpy(numpy_tensor)
```

参考：[L1aoXingyu/code-of-learn-deep-learning-with-pytorch: This is code of book "Learn Deep Learning with PyTorch"](https://github.com/L1aoXingyu/code-of-learn-deep-learning-with-pytorch)

## 运算类

### 矩阵相乘

#### torch.mm()

矩阵相乘用`torch.mm(a,b)`。

```
AB = A.mm(B) # computes A.B (matrix multiplication)
# or
AB = torch.mm(A, B)
# or
AB = torch.matmul(A, B)
# or, even simpler
AB = A @ B # Python 3.5+
```

不要用`torch.dot(a,b)`，因为`dot()`会将矩阵转为一维再操作，[向量长不相同时会报错](https://stackoverflow.com/questions/44524901/how-to-do-product-of-matrices-in-pytorch)。

`torch.dot()`与`numpy.dot()`功能有差异，具体讨论参见：[torch dot function consistent with numpy · Issue #138 · pytorch/pytorch](https://github.com/pytorch/pytorch/issues/138)

#### torch.mul()

矩阵上对应点（对应元素）相乘。

```
weights = torch.FloatTensor([1.0, -1.0, 2.0])
inputs = torch.FloatTensor([2, 3, 4])
inputs.mul(weights)
```

#### torch.matmul()

高维矩阵运算，支持[广播](https://pytorch.org/docs/stable/notes/broadcasting.html)。

```
>>> tensor1 = torch.randn(3, 4)
>>> tensor2 = torch.randn(4)
>>> torch.matmul(tensor1, tensor2).size()
```

[torch — PyTorch master documentation](https://pytorch.org/docs/stable/torch.html?highlight=torch%20mul#torch.mul)

详见：[torch.Tensor 的 4 种乘法 - da_kao_la 的博客 - CSDN 博客](https://blog.csdn.net/da_kao_la/article/details/87484403)

## 学习资料 📚

- [主页 - PyTorch 中文文档](https://pytorch-cn.readthedocs.io/zh/latest/)
- [pytorch 入坑一 | Tensor 及其基本操作 - 知乎](https://zhuanlan.zhihu.com/p/36233589)
- [L1aoXingyu/code-of-learn-deep-learning-with-pytorch: This is code of book "Learn Deep Learning with PyTorch"](https://github.com/L1aoXingyu/code-of-learn-deep-learning-with-pytorch)
