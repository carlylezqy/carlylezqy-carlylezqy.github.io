CenterNet: Keypoint Triplets for Object Detection

最大特点
Anchor Free

原理
图像传入全卷积网络后得到一个热力图，热力图峰值点即中心点，每个特征图的峰值点位置预测了目标的宽高信息。

This paper presents an efficient solution which explores the visual patterns within each cropped region with minimal costs.
以最小的成本探索每个裁剪区域内的视觉模式

Detects each object as a triplet, rather than a pair, of keypoints, which improves both precision and recall.

two customized modules (1) cascade corner pooling; (2)center pooling


Let $tl_{x}$ and $tl_{y}$ denote the coordinates of the top-left corner of i and $br_x$ and bry denote the coordinates of the bottom-right corner of $i$. 

Define a central region j. Let ctlx and ctly denote the coordinates of the top-left corner of j and cbrx and cbry denote the coordinates of the bottom- right corner of j. Then tlx, tly, brx, bry, ctlx, ctly, cbrx and cbry should satisfy the following relationship:

$$
\left\{\begin{array}{l}
\operatorname{ctl}_{x}=\frac{(n+1) \mathrm{tl}_{\mathrm{x}}+(n-1) \mathrm{br}_{\mathrm{x}}}{2 n} \\
\operatorname{ctl}_{\mathrm{y}}=\frac{(n+1) \mathrm{tl}_{\mathrm{y}}+(n-1) \mathrm{br}_{\mathrm{y}}}{2 n} \\
\operatorname{cbr}_{\mathrm{x}}=\frac{(n-1) \mathrm{tl}_{\mathrm{x}}+(n+1) \mathrm{br}_{\mathrm{x}}}{2 n} \\
\operatorname{cbr}_{\mathrm{y}}=\frac{(n-1) \mathrm{tl}_{\mathrm{y}}+(n+1) \mathrm{br}_{\mathrm{y}}}{2 n}
\end{array}\right.
$$