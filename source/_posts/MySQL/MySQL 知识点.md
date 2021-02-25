---
title: MySQL 知识点
date: 2021-02-25
category:
  - 数据库
  - MySQL
tag: MySQL
---

# MySQL 知识点

## `DISTINCT`

**语法：**

```mysql
SELECT DISTINCT select_list
```

-   `NULL` 合成一个
-   多个字段只要有一个不同就认为不同
-   可以认为是简单的 `GROUP BY`，区别是后者会排序
-   可用于聚合函数，比如 `COUNT(DISTINCT colume)`
-   有 `LIMIT` 时，`DISTINCT` 先执行

>   MySQL 8 中 `GROUP BY` 默认不会排序了

## 参考资料

[^1]: [MySQL Tutorial](https://www.mysqltutorial.org/)