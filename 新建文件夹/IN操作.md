>本部分内容来源与《从MySQL特性思考优化》这一网络文档

IN操作优化
======
- IN后面只能接常量，且最多不超过200个
- IN后面不能接子查询

```sql
select * from tb1 where tb1.id in (select id from tb2 where tb2.c1...)
// 优化后：
select tb1.* from tb1, (select id from tb2 where tb2.c1...)t where tb1.id = t.id;
```