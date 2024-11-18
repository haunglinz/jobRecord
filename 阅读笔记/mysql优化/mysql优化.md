innoDB中的索引是B+树结构的，叶子节点包含了所有非叶子节点的数据，叶子节点简会通过指正链接。之所以采用B+Tree结构，是因为数据库中有>、<、between … and这类范围查询语句，直接扫描叶子节点即可。
### 聚集索引
- 主键默认为聚集索引
- 如果没主键，非空的唯一索引就是聚集索引
- 没有唯一索引就会自动生成rowid作为主键

名字定义：
- 基数： 基数是字段distinct后的值，主键或非NULL的唯一索引的基数等于表的总行数
- 选择性：  选择性是指==基数（字段不重复的数）与总行数==的比值乘以100%，选择性通常表示在字段上是否适合创建索引
- 回表:  基数是字段distinct后的值，主键或非NULL的唯一索引的基数等于表的总行数
```sql
# 查看基数数据
SELECT stat_value AS pages, index_name
    , stat_value ＊ @@innodb_page_size / 1024 / 1024 AS size
FROM mysql.innodb_index_stats
WHERE（table_name = 'sbtest1'
    AND database_name = 'sbtest'
    AND stat_description = 'Number of pages in the index'
    AND stat_name = 'size'）
GROUP BY index_name;

```
