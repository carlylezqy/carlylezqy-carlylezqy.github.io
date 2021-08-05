# 目标检测 Object Detection

  

## 关键词

### 候选区域 Region Proposal

主流的目标检测框架分为[one-stage]和[two-stage]，而[two-stage]多出来的这个stage就是Regional Proposal过程。

  

| - | one-stage系 | two-stage系 | multi-stage系(已淘汰) |
| --- | --- | --- | --- |
| 主要算法 | YOLOv1、SSD、YOLOv2、RetinaNet、YOLOv3 | Fast R-CNN、Faster R-CNN | R-CNN、SPPNet |
| 检测精度 | 较低 | 较高 | 极低 |
| 检测速度 | 较快 | 较慢 | 极慢 |
| 起源 | YOLOv1 | Fast R-CNN | R-CNN |

  

Detection算法的几个task[^dtcn]

[^dtcn]: https://blog.csdn.net/JNingWei/article/details/80039079

1. 对于不需要预生成RP的Detection算法而言，算法只需要完成三个任务：

(1) 特征抽取; (2) 分类; (3) 定位回归

2. 对于有预生成RP的Detection算法而言，算法要完成的主要有四个任务：

(1) 特征抽取; (2)生成RP; (3) 分类; (4) 定位回归

  

![](./image/7-1-1.png)

  

### fine-tuning

  

fine-tuning就是使用已用于其他目标、预训练好模型的权重或者部分权重，作为初始值开始训练。

那为什么我们不用随机选取选几个数作为权重初始值？原因很简单，第一，自己从头训练卷积神经网络容易出现问题；第二，fine-tuning能很快收敛到一个较理想的状态，省时又省心。

具体做法:

  

+ 复用相同层的权重，新定义层取随机权重初始值

+ 调大新定义层的的学习率，调小复用层学习率

  

### Region Proposal Network[^RPN]

  

RPN（区域生成网络）是Faster RCNN中新提出的。替代了之前RCNN和Fast RCNN中的selective search方法，将所有内容整合在一个网络中，大幅提高检测速度。

大致结构：

生成anchors -> softmax分类器提取fg anchors -> bbox reg回归fg anchors -> Proposal Layer生成proposals

  

[^RPN]: [(RegionProposal Network) RPN网络结构及详解](https://blog.csdn.net/qq_36269513/article/details/80421990)<br>[Faster RCNN原理分析 ：Region Proposal Networks详解](https://blog.csdn.net/YZXnuaa/article/details/79221189)<br>[目标检测中region proposal的作用？——知乎](https://www.zhihu.com/question/265345106)

  

1. anchors

所谓anchors，实际为一组由rpn/generate_anchors.py生成的9个可能的候选窗口[形状为矩形]。直接运行generate_anchors.py会得到数组的输出。

将特征看做一个尺度 $51*39$ 的256通道图像，对于该图像的每一个位置，考虑9个可能的候选窗口：

  

+ 三种面积 $[128,256,512]\times[128,256,512]$

+ 三种比例 $[1:1,1:2,2:1][1:1,1:2,2:1]$

+ 以及其自由组合

  

这些候选窗口称为`anchors`。下图示出 $51\times39$ 个anchor中心，以及9种`anchor`示例。

  

1. Softmax判定

计算每个像素256-d的9个尺度下，得到9个anchor的值。为每个anchor分配一个二进制的标签 [前景(foreground)/背景(background)]。

我们分配正标签前景给两类anchor：

(1) 与某个ground truth（GT）包围盒有最高的IoU重叠的anchor（也许不到0.7）

(2) 与任意GT包围盒有大于0.7的IoU交叠的anchor。注意到一个GT包围盒可能分配正标签给多个anchor。

我们分配负标签（背景）给与所有GT包围盒的IoU比率都低于0.3的anchor。非正非负的anchor对训练目标没有任何作用，由此输出维度为$(2*9)18$，一共18维。

  

假设在conv5 feature map中每个点上有k个anchor（默认k=9），而每个anhcor要分foreground和background，所以每个点由256d feature转化为cls=2k scores；而每个anchor都有 $[x, y, w, h]$ 对应4个偏移量，所以reg=4k coordinates

补充一点，全部anchors拿去训练太多了，训练程序会在合适的anchors中随机选取128个postive anchors+128个negative anchors进行训练。

  

综上所述，RPN网络中利用anchors和softmax初步提取出foreground anchors作为候选区域。

  

bounding box regression 原理

对proposals进行bounding box regression

  

## 评价函数

  

http://nooverfit.com/wp/做机器学习，再别把iou，roi-和-roc，auc-搞混了-！聊聊目标/