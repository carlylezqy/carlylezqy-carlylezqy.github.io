CornerNet[^corner]

[^corner]: CornerNet: Detecting Objects as Paired Keypoints

We detect an object bounding box as a pair of keypoints, the top-left corner and the bottom-right corner, using a single convolution neural network. By detecting objects as paired keypoints, we eliminate the need for designing a set of anchor boxes commonly used in prior single-stage detectors.

Corner Pooling:  a new type of pooling layer that helps the network better localize corners.

-   主流の物体検出モデルのほとんどで用いられている Anchor Box を排除
-   Corner Poolingという新しいPooling手法を導入し、Bounding Boxの左上と右下のコーナーを検出
-   CornerNetでは、BBoxの中心座標と大きさではなく、左上と右下の頂点（corner）の座標(x, y)をそれぞれ推定します。
-   その後、同一物体の左上と右下の頂点を対応付けることで、物体を検出します。クラス予測は、頂点の検出と同時に行います。  

頂点の検出では、画像上の各ピクセルの頂点らしさを確率マップとして出力する方法をとっており、そのためAnchor Boxが不要となっています。  
  
- まず画像をHourglass Networkに入力して、特徴抽出を行います。
- 得られた特徴量を、左上と右下頂点それぞれを検出するネットワークに流し込み、それらの出力をCorner Poolingレイヤーを通した後、それぞれでHeatmap、Embedding、Offsetの３つ出力させます。
- 最後にこれらの出力を合わせて検出結果とします。

Hourglass Network 沙漏网络 砂時計ネットワーク
+ Hourglass NetworkはCornerNetで用いられている特徴抽出用ネットワークです。砂時計をいくつも繋げたような形になっていることからHourglass（砂時計）という名前がつけられているようです。
+ Hourglass Networkはもともと姿勢推定で提案されたアーキテクチャで、特徴マップのサイズを小さくしたり大きくしたりを繰り返すことで異なるスケールの情報を統合しようという意図で設計されています。  
+ Hourglass NetworkはResNetと同様、Residual構造を採用しており、特徴マップの拡大縮小をまたいで空間情報が落ちてしまうのを防いでいます。

Corner Pooling

Heatmap

Embedding

Offset