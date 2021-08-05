# R-CNN 
Region Based Convolutional Neural Networks
基于区域的卷积神经网络

1. Input image
2. Extract <u>Region Proposals</u>(~2k) (传统方法) Get warped region
3. Compute CNN features
4. Classify regions

Selective Search[^ss] 选择性搜索
自底向上的图像分割，在不同的尺度上面合并区域。
用于目标检测的区域提议算法，它计算速度快，具有很高的召回率，基于颜色，纹理，大小和形状兼容计算相似区域的分层分组。

主要包含：
- Hierarchical Grouping Algorithm
- Diversification Strategies

三大优势：
1. 捕捉不同尺度（Capture All Scales）
2. 多样化（Diversification）
3. 快速计算（Fast to Compute）

# Fast R-CNN
将R-CNN中下面3个独立模块整合在一起，减少计算量: 
+ CNN: 提取图像特征
+ SVM:目标分类识别
+ Regression模型: 定位
不对每个候选区域独立通过CNN提取特征，将整个图像通过CNN提取特征，然后从CNN的特征图中根据Selection Search的候选区域通过Rol Pooling层提取区域特征。

+ An input image and multiple <u>Regions of Interest</u> (RoIs) are input into a fully convolutional network. Each Rol is pooled into a fixed-size feature map and then mapped to a feature vector by fully connected layers (FCs). 
+ The network has two output vectors per RoI: (1) softmax probabilities and (2) per-class bounding-box regression offsets. 
+ The architecture is trained end-to-end with a multi-task loss.

Rol Pooling Layer
+ 将CNN的输出的任意大小的特征图使用Max Pooling转换为固定小的特征图
+ 假设ROl Popling的输入 $H_1 * W_1$ ，输出 $H_2 * W_2$ $(H_2 < H_1 \text{ and } W_2 < W_1)$，那么输入特征图会被平均分为$H_2 * W_2$，输出特征图的每一个格子包含输入特征图的 $H_1/H_2 * W_1/W_2$ 个像素。   然后对每一个格子做Max Pooling。

总结
+ 由于图像只通过CNN一次, 而不是让每一个候选区独立通过CNN, 减少了运算量
+ 将R-CNN中的多个SVM的分类合并为一个DNN, 让分类和定位可以同时训练 ,但是任然依靠Selective Search选择候选区域

# Faster R-CNN
去掉Selective Search，将候选区域的选择整合到深度学习网络模型中 RPN(Region Proposal Network)和 Fast R-CNN 结合

$k$ anchor boxes:

Faster R-CNN 训练步骤
1. 预训练一个用于分类的CNN 
2. 使用CNN的特征图作为输出，端到端的 fine-tune RPN + CNN。当loU > 0.7 为正样本，loU < 0.3 为负样本。
	1. 在特征图上面使用滑动窗口对每一个滑动窗口，产生多个Archor (相当于Selective Search选中的候选区域)。
	2. 对每一个滑动窗口, 产生多个Archor (相当于Selective Search选中的候选区域)。一个Archor由滑动窗口的中心位置、窗口尺寸、窗口宽高比决定。论文中使用3个尺寸和3个宽高比，所以一个滑动窗口位置对应9个($3*3$)Archor。
3. 固定RPN的权值，使用当前的RPN训练一个Fast R-CNN
4. 固定CNN，Fast R-CNN的权值，训练RPN
5. 固定CNN，RPN，训练 Fast R-CNN 的权值
6. 重复步骤4和5直到满意为止
