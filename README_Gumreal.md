# Branch gumreal-base-4.0.9

# Modified: zinterstore
增加谓词 limit, 可选值：
* limit 1: 结果集合中仅保留 Max Score 元素，如果该Score对应多个元素，随机选择其一；
* limit -1: 结果集合中仅保留 Min Score 元素，如果该Score对应多个元素，随机选择其一.

# Added: zinterGet
进行 zinter 操作，不保留结果集合，仅返回结果集合中的某个max score 或 min score 元素。
min 或者 max，取决于参数 limit 的值。