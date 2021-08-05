FCN
Fully Convolutional Networks[^fcn]

[^fcn]: Fully Convolutional Networks for Semantic Segmentation

将具体的事物抽象化。

FCNでは、⼀般物体認識の畳み込みニューラルネットワーク (e.g.VGG-16)の全結合層を1×1の畳み込み層に置き換えて いる。

全結合層を無くすことで、従来の畳み込みニューラルネット ワークのように⼊⼒画像のサイズを固定する制約がなくなっ た。また、クラス分類の結果がヒートマップ(Heatmap)と して出⼒されるようになる。

特徴マップをupsamplingで⼊⼒画像と同サイズに拡⼤する だけなら、物体の境界が模糊になる。

特徴抽出の最終層だけでなく、途中のpooling層で出⼒さ れる⼤きいサイズの特徴マップも活⽤する。特徴マップのサ イズは各層で異なるので、最終層の特徴マップから順にアッ プサンプリングで前の層と同サイズに拡⼤し、チャンネルご とに⾜し算する。

Fully Convolutional Networks for Semantic Segmentation Jonathan Long et al.

1. Only pooling and prediction layers are shown; intermediate convolution layers (including our converted fully connected layers) are omitted.
2. Solid line (FCN-32s): Our single-stream net, upsamples stride 32 predictions back to pixels in a single step.
3. Dashed line (FCN-16s): Combining predictions from both the final layer and the pool4 layer, at stride 16, lets our net predict finer details, while retaining high-level semantic information.⾼レベルのセ マンティック情報を持ちながら、より細かい詳細を予測 できるようになる。
4. Dotted line (FCN-8s): Additional predictions from pool3, at stride 8, provide further precision



1. 将分类网络改编为全卷积神经网络,具体包括全连接层转化为卷积层以及通过反卷积进行上采样
2. 使用迁移学习的方法进行微调
3. 使用跳跃结构使得语义信息可以和表征信息相结合,产生准确而精细的分割
4. FCN证明了端到端、像素到像素训练方式下的卷积神经网络超过了现有语义分割方向最先 进的技术
5. FCN成为了 PASCAL VOC最出色的分割方法,较2011和2012分割算法的 MloU提高了将 近20%


局部信息 (Local Information)
提取位置：浅层网络中提取局部信息
特点：物体的几何信息比较丰富，对应的感受野较小
目的：有助于分割尺寸较小的目标 有利于提高分割的精确程度

全局信息 (Global Information)
提取位置：深层网络中提取全局信息
特点：物体的空间信息比较丰富对应的感受野较大
目的：有助于分割尺寸较大的目标，有利于提高分割的精确程度

