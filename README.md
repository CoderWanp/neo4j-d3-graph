# 根据Neo4j导出的JSON数据做D3可视化展示

启动服务，再打开 `index.html` 查看效果

效果图如下及说明：

- 在搜索、鼠标进入该节点时会展示临近的关系节点
- 点击节点、文字切换显示
- 加入了碰撞检测模型，已注释，取消即可与效果图相同

![效果图](img/pic.png)

效果展示：
[https://coderwanp.github.io/neo4j-d3-graph/](https://coderwanp.github.io/neo4j-d3-graph/)

# 代码使用说明

## JSON格式要求

以 **p** 为键值对表示，每个 **p** 为一个查询关系。

按如下Cypher查询语句导出均可以展示：

```cypher
MATCH p=(n:节点类型)-[r:关系类型]->() RETURN p limit 20
```

## 如何配置为自己的数据

在 `<script>` 标签中定位，修改如下几行代码即可，不需要在到处去找位置了

```js
// 自定义图标及颜色（数组保证一一对应）
// names		图例名称变量制作图标
// labels		节点的标签名称（与records.json中保证相同）
// colors		图例颜色
// url 			json文件的路径
var names = ['企业', '贸易类型', '地区', '国家']
var labels = ['Enterprise', 'Type', 'Region', 'Country']
var colors = ['#55ffff', '#aaaaff', '#4e88af', '#ca635f']
var url = 'data/records.json'
```

# 修改说明

## 2021.04.01

之前的代码只支持 **距离为1** 的关系路径导入。

如果你从Neo4j导出的 `records.json` 中关系路径长度大于1，如下图这种情况会导致节点全部移至左上角。**现在已经修改完毕，支持长距离路径的图，只要满足JSON格式要求，即可进行可视化展示。**

![image-20210401170404874](img\json.png)

