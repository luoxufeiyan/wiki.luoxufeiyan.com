# SQLite3

## 输出时打印表头

```
.headers on
```


eg:
```
sqlite> SELECT * FROM Movies LIMIT 5;
1|The Abyss|1989
2|Aliens|1986
3|Avatar|2009
4|Ghosts of the Abyss|2003
5|Terminator 2: Judgment Day|1991

sqlite> .headers on

sqlite> SELECT * FROM Movies LIMIT 5;
id|title|year
1|The Abyss|1989
2|Aliens|1986
3|Avatar|2009
4|Ghosts of the Abyss|2003
5|Terminator 2: Judgment Day|1991

```