# PostgreSQL

## Pl/pgSQL 函数

- the body of every PostgreSQL function (including SQL functions) is defined as a single long string, wrapped in unusual quotes $$ ... $$. Because of their unusual quoting, they are different from other strings in PostgreSQL in that embedded single quotes do not need to be doubled.
- we have given a name to the parameter of the function, but within the function body, this name may not be used; in SQL functions, parameters must be referred to via positional notation $1, $2, etc. (named parameters may, however, be used in other kinds of functions e.g. plpgsql ones)

传参数时为$加参数序号

```
create or replace function BeerStyle(brewer text, beer text) returns text
as $$
select s.name
from   Beer b, Brewer br, BeerStyle s
where  lower(br.name) = lower($1) and lower(b.name) = lower($2)
	 and b.brewer = br.id and b.style = s.id
$$ language sql
;
```

[39.3.1.声明函数参数](https://wiki.postgresql.org/wiki/9.1%E7%AC%AC%E4%B8%89%E5%8D%81%E4%B9%9D%E7%AB%A0)

- an SQL function consists of a single SQL statement, similar to a view; unlike a view, the function has parameters and the SQL statement may refer to these parameters (using positional notation)

## 字符

### 拼接

使用|| 拼接

```
select loc.state||', '||loc.country
```

[PostgreSQL 学习手册(函数和操作符&lt;一&gt;) - Stephen_Liu - 博客园](https://www.cnblogs.com/stephen-liu74/archive/2011/12/19/2294071.html)

### 换行

```
return E'\n'
```

### NULL 判断

注意是 IS NULL 而不是 = NULL

```
WHERE aff.ending IS NULL
```
