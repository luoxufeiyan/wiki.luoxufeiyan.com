# 计算机视觉

## OpenCV

图片叠加的坑，叠加时不能简单相加，会造成overflow.

See here for more information on how opencv and numpy handle addition in this case: https://docs.opencv.org/master/d0/d86/tutorial_py_image_arithmetics.html

```
>>> x = np.uint8([250])
>>> y = np.uint8([10])
>>> print( cv.add(x,y) ) # 250+10 = 260 => 255
[[255]]
>>> print( x+y )          # 250+10 = 260 % 256 = 4
[4]
```