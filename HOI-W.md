# HOI-W 数据集介绍

![image-20200305145054229](https://github.com/moonie6568/HOI/blob/master/img/1.png)

HOI-W数据集只包含一些比较常见的relationships

总共包含来自不同的场景的38636张图片。其中，训练集29842张，测试集8794张。

训练验证集与测试集的数据集格式均不统一，以png格式为主，有部分的jpg,jpeg格式

![image-20200309194302033](https://github.com/moonie6568/HOI/blob/master/img/2.png)

包含的objects类别为11类：

![image-20200309161205606](https://github.com/moonie6568/HOI/blob/master/img/3.png)

包含的relations类别为10类：

![image-20200309161247636](https://github.com/moonie6568/HOI/blob/master/img/4.png)

给定的annotation包括人和物体的bbox,以及人和物体/人之间的relation，具体如下：

```python
{"file_name": "trainval_000000.png", 
 
 "annotations": [{"bbox": [486, 174, 1219, 1080], "category_id": "1"}, {"bbox": [787, 474, 955, 669], "category_id": "4"}], 
 
 "hoi_annotation": [{"subject_id": 0, "object_id": 1, "category_id": 5}, {"subject_id": 0, "object_id": 1, "category_id": 7}]}
```

可视化了相关的图片及标准，如下：
大部分为灰色图片，部分为彩色图片

![image-20200309162112702](https://github.com/moonie6568/HOI/blob/master/img/5.png)

![image-20200309162139410](https://github.com/moonie6568/HOI/blob/master/img/6.png)

标定存在的问题：
没有relation的object有时候标定，有时候不标定

![image-20200309162211268](https://github.com/moonie6568/HOI/blob/master/img/7.png)

![image-20200309162259825](https://github.com/moonie6568/HOI/blob/master/img/8.png)

![image-20200309162634982](https://github.com/moonie6568/HOI/blob/master/img/9.png)

一些标注错误的图片，food hold drink?

![image-20200313192908587](https://github.com/moonie6568/HOI/blob/master/img/11.png)

目前是可视化30张图片的结果，主要以单人为主，后续有时间再多可视化看一下

比赛结果评测方法

采用mAP作为评测指标

classification:与目标检测不同,只有当human detection, object detection and the interaction class都正确的情况下，才视为true positive。

regression:人和物体bboxes的检测仍然与目标检测相同，当与GT之间的IOU大于0.5时，即视为true positive。

![image-20200309161742977](https://github.com/moonie6568/HOI/blob/master/img/12.png)

输出的prediction.json文件的格式如下：（http://picdataset.com/static/challenge/results.json）

```python
[{"file_name": "test_000000.png",
  
  "predictions": [{"bbox": [486, 174, 1219, 1080], "category_id": "1"}, {"bbox": [787, 474, 955, 669], "category_id": "4"}], 
  
  "hoi_prediction": [{"subject_id": 0, "object_id": 1, "category_id": 5, "score": 0.89}, {"subject_id": 0, "object_id": 1, "category_id": 7, "score": 0.74}]}, ...]
```

可视化以及评测代码可以见官方给的代码：https://github.com/YueLiao/PIC_HOIW