# Neo4j
## 一、安装、启动 
```java
 neo4j console
```

## 二、实战（语法）
### 建立人物、地点结点以及他们之间的关系
#### 插入节点及关系
1. 建立人物节点
```neo4j
CREATE (n:Person {name:'Mike'}) return n 
//CREATE是创建操作,(n)代表一个节点，Person是标签，{}代表节点的属性（关系的属性同样适用）
```
2. 建立城市节点

```neo4j
CREATE (n:Location {city:'Boston',state:'MA'})
```
3. 建立人物之间的关系
```neo4j
MATCH (a:Person {name:'Mike'}),(b:Person {name:'Lily'}) MERGE (a)-[:FRIENDS {since:1999}]->(b)
```
4. 建立人物与地点之间的关系
```neo4j
MATCH (a:Person {name:'Mike'}),(b:Location {city:'Boston'}) MERGE (a)-[:BORN_IN {year:1980}]->(b)
```
5. 创建节点时就创建好关系
```neo4j
CREATE (a:Person {name:'John'})-[r:FRIENDS]->(b:Person {name:'Mary'})
```
#### 查询
1. 查询所有出生在Boston的人
```neo4j
MATCH (a:Person)-[:BORN_IN]-(b:Location {city:'Boston'}) RETURN a,b //MATCH 匹配操作
```
2. 查询所有对外有关系的节点
```neo4j
MATCH (a)-[]->() RETURN a
```
3. 查询所有有关系的节点
```neo4j
MATCH (a)--() return a
```
4. 查询所有对外有关系的节点以及关系类型
```neo4j
MATCH (a)-[r]->() return a.name,type(r)
```
5. 查询所有有朋友（FRIENDS）关系的节点
```neo4j
MATCH (n)-[:FRIENDS]-() RETURN n
```
6. 查找某人朋友的朋友
```neo4j
MATCH (a:Person{name:'Mike'})-[r1:FRIENDS]->()-[r2:FRIENDS]->(b) RETURN b
```
#### 增加/修改节点的属性
```neo4j
MATCH (a:Person {name:'Mike'}) SET a.age=34
//SET 是修改操作
```
#### 删除
1. 删除节点的属性
```neo4j
MATCH (a:Person {name:'Mike'}) REMOVE a.age
```
2. 删除节点
```neo4j
MATCH (a:Person {name:'Mike'}) DELETE a
```

![20211212190940](https://raw.githubusercontent.com/sqwang02/sqwang02/main/20211212190940.png)
