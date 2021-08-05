HRNet
Deep High-Resolution Representation Learning for Visual Recognition
用于视觉识别的深度高分辨率表示学习

SoTA は state-of-the-artの略で、機械学習の分野では「もっとも高精度」であることを指します。

Low-resolutioin Representation Learning[^hrnet]
- Classification networks: connect the convolutions in series from high resolution to low resolution

[^hrnet]: (2019实践空间站-基于高分辨率网络（HRNet）的案例创新)[https://www.bilibili.com/video/BV12J411R7cH]

High-resolution Representation Learning


Previous high-resolution representation learning(表現学習) look different, essentially the same
 (1) U-Net (2) SegNet (3) DeconvNet (4) Hourglass

Essentially, the previous methods remediate/extend classification networks (e.g., ResNet)
- Stage 1: compute low-resolution representations using a classification network 
- Stage 2: recover high resolution from low resolution by sequentially-connected convolutions

😢 The position-sensitivity of the representation is weak

HRNet 特徴
1. Learn high-resolution representations with stronger position sensitivity
2. Design from scratch instead of from classification networks 
3. Maintain high resolution representations through the whole network other than recovering from low resolution

Fundamental architecture changes
3. Repeat fusions across resolutions to strengthen high- & low-resolution representations

HRNet can learn high-resolution representations with strong position sensitivity
HRNet 可以学习具有强位置敏感性的高分辨率表示