# sort命令

`-n` 按照数字大小排序。需要指定位数 `sort -n -k2` 按照第二位数字排序。[eg](https://paste.ubuntu.com/p/jCMRCnwhnH/)

`-r` 反序reverse。

 

对每行进行排序。

```
cut -d $'\t' -f1 classes.txt |sort|head -n 15
BINF3010
BINF6111
BINF9010
COMP1000
COMP1000
COMP1000
COMP1000
COMP1000
COMP1000
COMP1000
COMP1000
COMP1511
COMP1511
COMP1511
COMP1511

```

配合`uniq`命令去除多余行，因为`uniq`只会对相临两行判断是否一致，因此需要把相同的内容放在一起。

```
cut -d $'\t' -f1 classes.txt |sort|uniq|head -n 15
BINF3010
BINF6111
BINF9010
COMP1000
COMP1511
COMP1521
COMP2041
COMP2121
COMP2511
COMP2521
COMP3151
COMP3331
COMP3411
COMP3421
COMP3900
```

对结果降序排列可用 `sort -nr`。

```
cut -d $'\t' -f1 classes.txt |sort|uniq -c |sort -nr |head -n 15
     31 COMP1521
     30 COMP9417
     24 COMP1511
     21 COMP2511
     20 COMP9044
     20 COMP6841
     20 COMP6441
     20 COMP2041
     19 COMP9331
     19 COMP3331
     19 COMP2521
     16 COMP6771
     15 COMP9414
     15 COMP3411
     14 ENGG1811

```

