

#### 缓存

<!-- @todo 找缓存答案 -->
- 为什么有了一级缓存还要有二级缓存。

- Mybatis的一级缓存在session中，只要通过session查过的数据，都会放在session里，
  下一次再查询相同id的数据，都直接冲缓存中取出来，而不用到数据库里去取了。

- Mybatis二级缓存是SessionFactory，如果两次查询基于同一个SessionFactory，那么
  就从二级缓存中取数据，而不用到数据库里去取了。

