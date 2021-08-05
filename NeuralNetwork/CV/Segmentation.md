Semantic Segmentation 语义分割
Instance Segmentation 实例分割
Panoptic Segmentation 全景分割

实例分割
实例分割比语义分割更进一步,除了像素级分类,还需要分别对类的每个实例进行分类。语义分割不区分特定类的实例。

语义分割研究现状
1. 传统方法
	1. Normalized cut
	2. Structured Random Forests
	3. SVM
2. 深度学习卷积神经网络
	1. FCN
	2. SegNet
	3. LinkNet


常用数据集（双流数据集）
SUNRGBD、NYUDv2、RASCAL VOC、CityScapes、CamVid


## 指标
假设：共有 $k+1$ 个类，$p_{ij}$ 表示本属于 $i$ 类但被预测为类 $j$ 的像素数量。即，$p_{ii}$ 表示真正的数量，而 $p_{ij}$ 和 $p_{ji}$ 则分别被解释为假正或假负。

Pixel Accuracy (PA 像素精度)：标记正确的像素占总像素的比例。
$$\text{PA}=\frac{\sum_{i=0}^{k} p_{i i}}{\sum_{i=0}^{k} \sum_{j=0}^{k} p_{i j}}$$
Mean Pixel Accuracy (MPA 均像素精度)：计算每个类内被正确分类像素数的比例，再求所有类的平均。
$$\text{MPA}=\frac{1}{k+1} \sum_{i=0}^{k} \frac{p_{i i}}{\sum_{j=0}^{k} p_{i j}}$$
Mean Intersection over Union (MloU 均交并比)：计算算真实值和预测值的交集和并集
$$\text{IOU}=\frac{A_{\text {pred}} \cap A_{\text {true}}}{A_{\text {pred}} \cup A_{\text {true}}}$$
$$\text{MIoU}=\frac{1}{k+1} \sum_{i=0}^{k} \frac{p_{i i}}{\sum_{j=0}^{k} p_{i j}+\sum_{j=0}^{k} p_{j i}-p_{i i}}$$