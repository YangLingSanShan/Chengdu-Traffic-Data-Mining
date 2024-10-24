# BUAA Data Mining Homework - ChengDu Traffic Data Mining

利用数据挖掘课程学习到的聚类、分类、回归等技术，结合成都交通轨迹数据，挖掘交通出行规律

**数据集**：https://github.com/yyf-buaa/DM_2024_Dataset

data目录下为原始数据

product_data下为任务一预处理的数据，以及路网匹配的结果

![analysis](.\pic\analysis.png)

## task 1

目前工作（已完成）：

将road.csv文件读入并处理为roads.shp文件和nodes.shp文件，这两个可以调用作为路网的Net进行处理。

将traj.csv处理为gps_data.csv，然后切分出一个test.csv文件，作为代码测试用（完整文件跑完很久很久）

然后最终的匹配结果在match_results里面，其中的html为可视化文件，其中的match_result.csv文件表头定义如下：

| 字段名称               | 字段含义                                                     | 字段类型 |
| ---------------------- | ------------------------------------------------------------ | -------- |
| agent_id               | gps点所属agent_id                                            | string   |
| seq                    | gps点的序列ID                                                | int      |
| sub_seq                | gps点的子序列ID, 如果子序列>0, 说明该点是在匹配后补出来的点, 称之为后补点, 不会去计算其在目标路段上的投影点 | int      |
| time                   | gps定位时间                                                  | datetime |
| loc_type               | gps点类型, 三类: s：源GPS点、d：增密点、c：后补点            | string   |
| link_id                | gps匹配路段的link_id，对应路网的link_id字段                  | int      |
| from_node              | gps匹配路段的起始节点(表征行车方向起点)                      | int      |
| to_node                | gps匹配路段的终到节点(表征行车方向终点)                      | int      |
| lng                    | gps点的经度, EPSG:4326                                       | float    |
| lat                    | gps点的纬度, EPSG:4326                                       | float    |
| prj_lng                | gps点在匹配路段上对应匹配点的经度, EPSG:4326, 后补点的该值为空 | float    |
| prj_lat                | gps点在匹配路段上对应匹配点的纬度, EPSG:4326, 后补点的该值为空 | float    |
| match_heading          | gps匹配点的航向角(从正北方向开始顺时针扫过的角度, 0~360度), 后补点的该值为空 | float    |
| dis_to_next            | gps投影点与后序相邻gps投影点的路径距离(不考虑后补点), 后补点的该值为空 | float    |
| route_dis              | gps匹配点在匹配路段上与路段起点的路径距离, 后补点的该值为空  | float    |
| 其他用户指定输出的字段 | 参照参数user_field_list                                      |          |

**目前需要做的事情：**

调参！！！！

调参的一些情况可以直接见库的说明文档：[🗺️ 地图匹配 — GoTrackIt 0.3 documentation](https://gotrackit.readthedocs.io/en/latest/地图匹配.html#id2) 库环境安装也在这里面

目前发现的有：

1. gps_buffer不宜小于150，否则会出现间断路径
2. 建议用网格搜索解决



可能插值多点会好一些？？？

## task2

现在有个问题：那个road_neighbor_cd文件，是否可能存在关系，某种路径大多数情况下会和某些路径相连，而不会和其他的相连，比如（假设）高速和乡村小道，感觉可以考虑进来

考虑了上面那个，现在有一些TODO的idea可以等后面做，现在的acc能到85%+



## task3

