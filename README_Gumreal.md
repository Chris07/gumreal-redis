# Branch gumreal-base-4.0.9

# Modified: zinterstore
## 增加谓词 limit
可选值：
* limit 1: 结果集合中仅保留 Min Score 元素，如果该Score对应多个元素，随机选择其一；
* limit -1: 结果集合中仅保留 Max Score 元素，如果该Score对应多个元素，随机选择其一.

## 语法
ZINTERSTORE destination numkeys key [key ...] [WEIGHTS weight [weight ...]] [AGGREGATE SUM|MIN|MAX] [LIMIT 1|-1]

例如
ZINTERSTORE sum_point 2 mid_test fin_test LIMIT -1

# Added: zintergetn
进行 zinter 操作， 不保留结果集合，返回结果集合中指定数量的 max score 或 min score 元素。
min 或者 max， 取决于参数 limit 的值。

## 语法
ZINTERGETN numkeys key [key ...] [WEIGHTS weight [weight ...]] [AGGREGATE SUM|MIN|MAX] [LIMIT n|-n]


# Added: zinterdiffgetn
首先进行 zinter 操作， 然后进行 diff 操作求差集， 返回结果集合中指定数量的 max score 或 min score 元素。
min 或者 max， 取决于参数 limit 的值。
* limit < 0: max
* limit > 0: min

## 语法
ZINTERDIFFGETN numkeys key [key ...] [WEIGHTS weight [weight ...]] [AGGREGATE SUM|MIN|MAX] [DIFF numDiffKeys diffKey [diffKey ...]] [LIMIT n|-n]

例如：

    ZINTERDIFFGETN 2 s1 z1 WEIGHTS 0 1 AGGREGATE SUM DIFF 1 s2 LIMIT 1

表示： 
1. 先对 s1,z1求交集，分值s1占0%，z1占100%求和, 得到中间结果集合1；
2. 将中间结果集合1 与s2求差集, 得到中间结果集合2;
3. 从中间结果集合2中获取分值最小的1个元素。

如果:
* s1={a,b,c}
* s2={a}
* z1={a:1, b:2, c:3, d:4, e:5}

那么，命令执行后：
* 结果为 b