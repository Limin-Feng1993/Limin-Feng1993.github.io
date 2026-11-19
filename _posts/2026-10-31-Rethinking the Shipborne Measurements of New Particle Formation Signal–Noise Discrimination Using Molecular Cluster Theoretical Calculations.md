---
layout:     post                    # 使用的布局（不需要改）
title:      2026-10-31-Rethinking the Shipborne Measurements of New Particle Formation           # 标题 
subtitle:   Signal–Noise Discrimination Using Molecular Cluster Theoretical Calculations #副标题
date:       2026-10-31             # 时间
author:     Limin                      # 作者
header-img: img/Fox.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    - 科研随笔
---

>注：本文是作者于2026年4月29日PPT报告的文字版本，有修改。报告原标题为：分子团簇计算约束下的海洋大气新粒子观测数据校正。

#### 1. 研究背景
 
大气中超细颗粒物 (粒径小于100 nm) 的光散射强度不足，无法被传统的光学粒子计数法检测。光学粒子计数法主要探测粒径300 nm以上粒子的米氏散射信号，例如美国TSI公司的仪器Optical Particle Sizer Model 3330，监测粒径段范围为300 nm-10 μm。

当粒子直径远小于入射光波长时，属于瑞利散射区。瑞利散射强度正比于粒径的六次方，当粒径从 300 nm 降到 10 nm，散射强度会剧烈下降至低于仪器的触发阈值，直接淹没在背景信号噪声里。

![米散射与瑞利散射](https://upload-images.jianshu.io/upload_images/17085473-d54fec09506da824.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

因此，对于纳米颗粒物，要实现实时单颗粒计数来表征其数浓度 (个/cm^3^)，必须采用凝聚技术：利用工作液 (例如正丁醇) 产生蒸汽，蒸汽在纳米颗粒表面冷凝，使其长大到可被光学检测的尺寸。随后，长大后的颗粒穿过激光器与检测器，从而对样品气流中的每一个颗粒进行计数。

![凝聚技术：采集的空气，在35°条件下产生正丁醇蒸汽使其饱和，然后通过10°冷凝器，正丁醇蒸汽凝结在颗粒表面，使单个纳米颗粒的粒径增加到约10 µm，然后再用光散射方法来探测。](https://upload-images.jianshu.io/upload_images/17085473-e6e80120c968f08d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

> 正丁醇、异丙醇和丙酮加热易蒸发、冷却易冷凝；醇、酮含极性基团，能与纳米颗粒 (硫酸盐、铵盐、有机物等) 表面的羟基、羧基、氨基形成氢键或偶极作用，优先吸附在颗粒表面，触发异相成核而无需高过饱和度；醇、酮表面张力远低于水，临界成核半径更小 (即更易克服开尔文效应)，更容易在1–10 nm 超细颗粒上启动冷凝，可在毫秒级成核与增长。

除了凝聚技术，粒子计数器还用到了电迁移率测量技术，根据电迁移率对气溶胶进行分级分离。电迁移率取决于颗粒的粒径与荷电状态。电迁移率更高的颗粒向中心电极杆移动的速度，快于电迁移率较低的颗粒。颗粒的电迁移率与仪器施加的电场强度共同决定了颗粒会撞击在中心电极杆的哪个位置。用这个原理测得的纳米颗粒物直径称之为为电迁移直径 (Electrical Mobility Diameter)。

![电迁移测量技术，Model 3091 FMPS™ Spectrometer](https://upload-images.jianshu.io/upload_images/17085473-61cdcfe68c173877.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

粒子计数器的探测下限通常定义为仪器至少能够探测到50%颗粒时对应的粒径。如下图，表现最佳的仪器水平达到探测到50%颗粒时，电迁移直径在2 nm以上。因此目前商业化仪器的检出限基本上在2-3 nm。

![Detection efficiencies of the Airmodus A20 and A11, and TSI 3772 and 3776 with modified condenser and saturator temperatures. KANGASLUOMA J, ATTOUI M. Review of sub-3 nm condensation particle counters, calibrations, and cluster generation methods [J]. Aerosol Science and Technology, 2019, 53(11): 1277-310.](https://upload-images.jianshu.io/upload_images/17085473-e27cd50ca8ff7106.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

基于凝聚和电迁移测量计数原理，一些商业公司例如TSI已经生产的粒子计数器，可对粒径低至 2.5 nm的纳米颗粒进行在线单颗粒计数。例如仪器型号Nanoparticle Sizer, Scanning Mobility Particle Sizer (SMPS) Spectrometer Series 3938，无需使用透射电镜 (TEM) 或扫描电镜 (SEM)时的等待延迟，实时测量，测量范围为2.5 nm–1000 nm。比SMPS使用和维修更为简便的仪器是Fast Mobility Particle Sizer™ (FMPS™) Spectrometer Model 3091，实现1秒内测量全部粒径段的粒子数，检测粒径范围是5.6 nm–560 nm。

由于粒子计数器的采样频率是每秒扫描全部粒径段，难免受到不同来源的粒子干扰，例如船载监测平台本身产生的污染。在长时间序列数据处理时，为了对数据平滑，一般取10分钟甚至更长时间的平均值。不能简单的剔除离群异常值，因为纳米颗粒物数浓度的突然爆发是有科学意义的，即新粒子形成 (new particle formation, NPF) 事件。

FMPS仪器野外监测中，理想状态下的新粒子形成事件，无其他源干扰。

![理想状态下的新粒子形成事件](https://upload-images.jianshu.io/upload_images/17085473-aaaf5da43ea49e7d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

在实际采样中，经常在秒的级别出现干扰信号，纳米颗粒物确实增加，但这些信号不一定是气态前体物成核导致，可能是实验平台本身受到污染或者是仪器本身运行不稳定而产生的噪音。

![船舶航测过程中，纳米颗粒物在线采样界面，2014年西太平洋航次。](https://upload-images.jianshu.io/upload_images/17085473-6971b38f8e79580e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

综上所述，目前通过1-100 nm纳米级别颗粒物数浓度的观测来发现新粒子形成事件，一是没有彻底打通1-3 nm分子团簇级别的高精度在线监测技术，二是在3 nm以上仍存在仪器的检测误差，三是全粒径段都有可能受到不同来源的信号干扰。
*********************************************************************************
近年来，量子化学计算方法和分子团簇理论的发展，为探索**1-3 nm“仪器看不见”的粒径段**奠定了基础。海洋大气中新粒子成核的本质，是含硫 (如硫酸、甲磺酸)、含氮 (如氨、有机胺) 、含碘 (如碘酸、亚碘酸) 等气态前体物分子通过氢键、卤键及质子转移等非共价弱相互作用结合成分子团簇， 并不断长大的过程。

![典型成核团簇](https://upload-images.jianshu.io/upload_images/17085473-ac7bbfbc917da3fe.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

在近地面大气中，中性成核途径在多组分系统中更高效 (Lehtipalo et al., 2018)。现场观测发现近地面大气中离子诱导成核对NPF的贡献较小，因为大气中始终存在多种气态前体物。

海洋中藻类释放的碘化物气体具有极强的自聚合能力，直接通过同类相吸作用形成团簇。有机胺气体与碘酸之间通过酸碱相互作用、复杂氢键网络的构建、以及碘酸分子独特的卤键作用，使得碘酸-二甲胺等团簇具有较高的热力学稳定性，成核效率比硫酸-胺体系高出几个数量级。例如对于HIO~3~−DMA−NH~3~三元成核体系，DMA和NH~3~可以共同稳定碘酸分子簇 (Li et al., 2024)。

![碘酸-二甲胺−氨三元成核体系](https://upload-images.jianshu.io/upload_images/17085473-48ac2b2b04c9c51c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

甲磺酸 (MSA) 是藻类排放的二甲基硫 (DMS) 被氧化的产物，在海洋大气中浓度较高。例如对于HIO~3~-HIO~2~-MSA三元成核，MSA将显著提⾼HIO~3~-HIO~2~团簇的形成，尤其是含有MSA含量较高而碘含量较低的极地寒冷海洋区域 (Li et al., 2024)。

![碘酸-亚碘酸-甲磺酸三元成核体系](https://upload-images.jianshu.io/upload_images/17085473-d5218c8a4f56de0f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

作为DMS的典型氧化产物，甲磺酸MSA在海洋大气中无处不在，且通常存在较高浓度，实地观测显示，MSA在海洋大气中经常与碘酸IA和二甲胺DMA共存，且这三种物质在气溶胶颗粒中同时被检测到 (Salignat et al., 2024)。例如对于HIO~3~–MSA–DMA三元成核，在硫和氮含量高但碘含量低的区域更稳定，尤其是在极地寒冷海洋区域 (Li et al., 2026)。

![碘酸–甲磺酸–二甲胺三元成核](https://upload-images.jianshu.io/upload_images/17085473-86d33f86e70ae531.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

在量子化学计算领域，通常利用密度泛函理论 (DFT) 结合分子团簇动力学模型 (例如ACDC模型)，计算成核速率_J_ (cm^−3^ s^−1^) 。目前ACDC计算结果的成核速率是_J~1~_，即直径约在1 nm左右达到热力学临界尺寸的团簇 (**McGrathIt et al., 2012: it should be noted here that the largest clusters in our system are approximately 1 nm in diameter**)。

分子团簇动力学模型计算所需要的凝结汇系数 、温度等输入参数，需要使用云箱实验中的数值，甚至计算结果也要与云箱实验对比。例如欧洲核子研究中心的CLOUD实验中的云室，体积为 26.1立方米，一般在固定温度 (例如 278 K) 下进行实验。

![CLOUD云室](https://upload-images.jianshu.io/upload_images/17085473-d55850732d0b59a3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

在CLOUD云箱实验中，气体前体物浓度、温度、湿度等参数是人为控制的，不能反应真实海洋大气中，从近岸海域到开阔大洋海域的组分浓度梯度变化、以及气象条件的不同。

目前经常被理论计算所采纳的高山站、森林站观测结果，例如位于芬兰南部的SMEAR II Hyytiälä 站，自1996年开始对新粒子成核的观测，历史最悠久，以及位于芬兰赫尔⾟基大学的SMEAR III Helsinki站。

![SMEAR II Hyytiälä 站位置。Janssen, R. H. H. et al. Estimating seasonal variations in cloud droplet number concentration over the boreal forest from satellite observations. Atmos. Chem. Phys. 11, 7701-7713, (2011).](https://upload-images.jianshu.io/upload_images/17085473-c90f288f4885cd2b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

大多数大气颗粒物测量点是固定的，即以“欧拉系统 (Eulerian System)”记录数据。欧拉系统是选择一个固定不动的点，观察随着时间流逝，流经这个点的气团性质。单凭一个站点观测到的颗粒物浓度变化，无法判断是“当地正在发生成核和增长反应”，还是因为“远处的一个高粒子浓度气团传输过来”，因此必须假设在大尺度范围内空气是均匀混合的。

而在航海观测中，仪器实际上以“拉格朗日系统 (Lagrangian System)”记录数据，观测坐标系跟随气团一起移动。当考察船在海上航行，且航行速度与风向、风速在某种程度上匹配时，仪器记录的数据更接近于同一个气团的成核和增长过程。此时混合均匀的假设不成立，因为可能几个小时后就到了另外一个大气条件完全不同的海域。

![欧拉系统与拉格朗日系统](https://upload-images.jianshu.io/upload_images/17085473-e767ba84676b0628.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

船舶一旦停止抛锚在某个海域，烟囱尾气的影响较大，数据不可用。仪器采样口必须在距离烟囱较远的前甲板顶楼。

对于航海观测，如前文所述，受限于观测仪器、观测平台，采样存在误差，因此需要对理论计算结果与航海观测的结果进行交叉验证，一是验证理论计算的准确性，二是辨别观测数据的误差。本研究针对的主要问题如下：

（1）在真实的远海和近海大气条件下，在温暖的中纬度海域，甲磺酸和碘酸含量都丰富，IA-MSA-DMA主导的理论成核体系是否还有效、计算成核速率能否与观测成核速率结果相匹配；

（2）在离线和在线仪器采样中，如何区分区分船舶自身排放等不稳定因素带来的噪声，从而鉴别真实的新粒子形成信号。
*********************************************************************************
#### 2. 研究方法

##### 2.1 成核体系描述

以下主要讨论碘酸-甲磺酸-二甲胺：HIO~3~ (IA)~-MSA-DMA。碘酸-甲磺酸-二甲胺体系的成核速率与气体浓度之间的关系满足广义线性函数：

![碘酸-甲磺酸-二甲胺体在不同气体浓度下的成核速率。Li, J., Ning, A., Liu, L., Deng, X. & Zhang, X. Mechanistic insights into marine boundary layer nucleation: synergistic interactions of typical sulfur, iodine, and nitrogen precursors. Atmos. Chem. Phys. 26, 4423-4437, doi:10.5194/acp-26-4423-2026 (2026).](https://upload-images.jianshu.io/upload_images/17085473-9eeac8a168c77424.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

亦即成核速率_J_ (cm^−3^ s^−1^) 与前体物浓度C (molec⋅cm^−3^) 之间的拟合关系为：

![拟合关系](https://upload-images.jianshu.io/upload_images/17085473-8f09cb4693568efb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这是因为成核速率通常遵循幂律定律 (Lehtipalo et al., 2018)：

![成核速率通常遵循幂律定律](https://upload-images.jianshu.io/upload_images/17085473-906fc03fa11a0deb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

取对数后得到：

![拟合关系](https://upload-images.jianshu.io/upload_images/17085473-3afaf4580ea9106f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### 2.2 船舶航测数据描述

选择2014年3-4月西北太平洋航次观测数据。纳米粒子数浓度 (个/cm^3^) 来自于顶层甲板室内放置的FMPS仪器，采样口伸出窗外。当忽略预先存在的凝结汇和外来传输粒子的影响时，观测粒子形成速率_J_obs_ 取小时内最大的粒子浓度秒增长速率。

新粒子形成速率是指团簇超过某一尺寸亦即流出动力学模拟体系的通量 (cm^-3^ s^-1^)。通常不能估计瞬时的粒子形成速率， 而是估计新粒子事件持续时间内的平均形成速率 (Kulmala, et al. 2004)。当忽略预先存在的凝结汇和外来传输粒子的影响时，有：

![粒子形成速率-极简化版, N is the total particle number concentration in the size range [D, Dmax]。](https://upload-images.jianshu.io/upload_images/17085473-3fe2eda14f28a510.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

然而，当背景颗粒数浓度非常高时，该简化公式会显著低估真实的颗粒生成速率。

颗粒态有机胺、甲磺酸浓度来自于滤膜采样法，滤膜持续采样时间大约为一天，滤膜经过萃取溶液注射进IC离子色谱法检测，滤膜搭载在分级式撞击采样器MOUDI上，具体方法见Xie et al. (2018)、Chen et al.(2021)。温度湿度等气象参数来自于船载气象站VMS系统。

![西北太平洋航次，航线图。](https://upload-images.jianshu.io/upload_images/17085473-f0f3b7e79d316642.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

选择DMA-MSA成核体系作为新粒子成核速率的指示物，而不是其他的例如硫酸、氨、硝酸的原因：开阔大洋中DMA和MSA的边际效应更大 (Li et al., 2026)，硫酸易形成大颗粒，会造成更强的凝结汇，压缩其他前体的边际贡献，降低成核速率。IA–MSA–DMA 三元成核在硫和氮含量高但碘含量低的区域中，热力学上更有利，协同效应提升了 4 至 8 个数量级 (Li et al., 2026)。

在渤海和黄海区域，海洋大气受到大陆污染气团影响，含有高浓度的凝结汇和硫酸气体，而在日本以东的西北太平洋，距离大陆较远，凝结汇浓度低，生物活动旺盛，DMS、MSA、HIO~3~等气体含量较高。日本东侧有黑潮 (日本暖流) 爆发，藻类的增加和减少，影响含硫气体、有机胺的释放。

![从中国近海到西太平洋DMA空间分布图，数据来源于2014年东方红2号科考船航测。](https://upload-images.jianshu.io/upload_images/17085473-bfe45e07895d1ace.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

碘酸需要极高灵敏度的仪器，且检测方法与常规的有机胺/氨不同，因此在本文采用实际海洋大气的观测中未予检测。本文中，碘酸浓度设定为固定值，即[HIO~3~] = 1.0 × 10^7^ molec⋅cm^−3^ ((Li et al., 2026))。

![碘酸检测方法与有机胺/氨不同。](https://upload-images.jianshu.io/upload_images/17085473-584878395adfcff1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### 2.3 对观测数据的后处理

在开阔大洋中，气体有机胺浓度较低 ，容易低于仪器的检测限，所以才本研究用浓度较高检测误差较低的颗粒态浓度反演。有机胺的气粒转化与粒径无关，而氨气的气粒转化在粗粒径上大于细粒径 (Xie et al., 2018)。本研究将0.1–2.5 μm粒径段颗粒态有机胺和甲磺酸浓度乘以一个固定的气粒分配系数0.05，作为气态DMA和MSA浓度。

气粒分配系数0.05参考了大气中硫酸气溶胶粒子对气态胺的摄取系数约为0.02-0.05 ( Wang et al., 2010)。硫酸气溶胶对气态胺是近乎不可逆的酸碱中和反应，不存在蒸气压驱动的热力学平衡，因此气粒两相的浓度比例完全由动力学稳态决定：单位时间内气相被颗粒摄取的量 = 单位时间内颗粒相从大气中清除的量。当γ~P~摄取系数取0.03时，DMA 分子热运动速率取3.7×10^4^ cm/s，气溶胶总表面积浓度取2–5×10^-7^ cm^2^/cm^3^，0.1–2.5 μm粒径段细颗粒一级去除速率取2–5×10^-6^ S^-1^，气态与颗粒态的比值C~g~/C~p~ ≈ 0.03-0.09 (Yu and Luo, 2014)。

![气粒分配比值计算](https://upload-images.jianshu.io/upload_images/17085473-cdf3251e5a97bf5f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

由于ACDC理论计算的结果是1 nm左右的成核速率_J~1~_，故需结合5 nm粒径段的观测数据_J~5~_，共同反推出我们感兴趣的_J~1~_，以便得到完整的粒径谱。使用 Kerminen-Kulmala 公式 (Kulmala et al., 2012) 进行推导：

![Kerminen-Kulmala equation](https://upload-images.jianshu.io/upload_images/17085473-1d20bc4cef3b6744.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

其中，约化凝结汇系数CS’设置为18 m^-2^，经验校正系数η设置为 0.23 nm^-1^ (Li et al., 2026)。

> 凝结汇CS系数一般取值为2.0×10^−3^ s^−1^。换算为约化凝结汇系数CS’。默认以硫酸蒸汽的扩散系数为基准换算。

Kerminen-Kulmala公式中生长速率GR存在不确定性。在大陆的固定站点观测中，恒定的生长速率GR在区域性新粒子形成事件中很常见。因为对于粒径大于10 nm的粒子，开尔文效应的影响已经可以忽略，粒子的凝结增长由气相前体物浓度主导，因此生长速率会趋于恒定。

![粒子平均直径随时间的变化，该线的斜率即为直径增长率，仪器的最小粒径分辨率大于10 nm。Kulmala, M. et al. Formation and growth rates of ultrafine atmospheric particles: a review of observations. Journal of Aerosol Science 35, 143-176, (2004).](https://upload-images.jianshu.io/upload_images/17085473-56ae92b2d02239d2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

而在1–10 nm粒径段，开尔文效应导致蒸发速率随粒径呈非线性骤降，GR呈现阶梯性、非线性增长。观测到的GR在1.1–2.0 nm粒径范围内为3.2–4.4 nm·h^-1^ (Xia et al., 2020; Yu et al., 2019)。据Nieminen et al. (2018)，10 nm粒子的生成速率中值变化范围约为3个数量级 (0.01–10 cm^-3^ s^-1^)，增长率GR变化范围约为1个数量级 (1–10 nm h^-1^)。其中北京站点_J_ = 5.9-8.4 cm^-3^ s^-1^，GR =1.6-4.6 nm h^-1^；赫尔辛基测量站_J_ = 0.3-1.4 cm^-3^ s^-1^，GR =2.0-3.4 nm h^-1^。综上所述，本文中GR<sub>1-10 nm</sub> 统一取文献的最大值即4 nm·h^-1^。
*********************************************************************************
#### 3. 分析与讨论
######  3.1 A类数据

在A类数据中，观测成核速率_J_obs_ 与模拟成核速率_J_sim_相近， 犬牙交错，在一个数量级上。以2014-03-25为例，成核速率_J_ =3-7×10^1^ cm^-3^ s^-1^。成核速率的变化和粒子数浓度的变化同步，即形成的加速度与总浓度同步。这说明背景粒子凝结汇较少，观测得到的有机胺DMA和甲磺酸MSA浓度有效参与到新粒子形成当中。在背景粒子凝结汇较少的情况下，模拟的MSA-DMA成核体系有效还原观测新粒子形成。

![A类数据，2014-03-25。](https://upload-images.jianshu.io/upload_images/17085473-01761fba800e452b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![A类数据，2014-03-25。仪器监测界面。](https://upload-images.jianshu.io/upload_images/17085473-6f689caa8c6dcfb0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

A类数据中，还有一种情况：观测成核速率_J_obs_ 与模拟成核速率_J_sim_，本来有偏差，但是_J_obs_突然上升靠近_J_sim_。以2014-04-10为例，蓝色曲线5.6-6.5 nm粒径段浓度在12:00之前就已经有一个较宽的增长峰，但并未增长到较大粒径 (其他颜色曲线)。12:00之后， 光化学作用增强，突破之前已经生成小粒径凝结汇的临界点，_J_obs_突然上升。

![A类数据，2014-04-10。](https://upload-images.jianshu.io/upload_images/17085473-62fc066697ac236d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

最小粒径段生成后，没有增长，到12时之后才增长，这说明气体前体物供应的不可持续性。12:00 前可能出现了小规模成核现象，足以跨过 5-6 nm 的检测门槛，但随后光化学速率或前体物排放没有持续增强，导致气相中的超饱和度迅速下降。下午的光化学强度和前体物浓度达到了一个临界点，使得粒子能够克服凝结汇的清除，实现跨粒径段的连续增长。强烈的阳光维持了高浓度的OH等自由基。白天气体前体物在大气中的分压远高于粒子表面的饱和蒸气压。突破之前已经生成的凝结汇的临界点，是典型的光化学驱动成核并增长爆发。如果是预先存在的污染气团，是已经老化之后的，不会出现粒径持续增长的情况。

![A类数据，2014-04-10。仪器监测界面。](https://upload-images.jianshu.io/upload_images/17085473-aab6f125dd5ba598.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
*********************************************************************************
###### 3.2 B类数据

在B类数据中，观测成核速率大于模拟成核速率。以2014-03-21为例，观测得到的成核速率_J_obs_ 始终大于模拟得到的成核速率_J_sim_，二者差了一个数量级。亦即模拟_J_sim_时所需的DMA和MSA浓度较低，但是却出现了高于预期的粒子数浓度，这说明FMPS粒子计数器采集到了大量预先存在的背景场粒子。

![在B类数据中，观测成核速率大于模拟成核速率。](https://upload-images.jianshu.io/upload_images/17085473-3299628e5e41f6c4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

如下图仪器监测界面所示，2014-03-21，大量预先存在的背景场粒子+新粒子成核，导致的5-40 nm粒径段混杂信号。

![B类数据，仪器监测界面。](https://upload-images.jianshu.io/upload_images/17085473-3d2ce0e2ff86161a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
*********************************************************************************
###### 3.3 C类数据

在C类数据中，模拟成核速率大于观测成核速率。以2014-04-06为例，模拟得到的成核速率_J_sim_始终大于观测得到的成核速率_J_obs_，二者相差1个数量级。

![C类数据：模拟成核速率大于观测成核速率。](https://upload-images.jianshu.io/upload_images/17085473-49dbfe855c4c0c5c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

模拟成核速率较高的原因：有机胺气体浓度作为ACDC模型的输入参数之一，是由滤膜采样颗粒物有机胺浓度换算得来，即乘以一个固定的气粒分配系数。这一天0.1-2.5 μm粒径段颗粒态的有机胺浓度较高 (DMA<sub> < 2.5 μm</sub> =1.33 μg/m^3^，为整个西太平样航次最高浓度)，但反映到FMPS计数器观测数据中的成核效应却不明显。

从下图中的2014-04-06仪器监测界面来看，捕捉到污染气团 (特征是20-50 nm中心粒径不变) 经过，这是受船舶平台本身的污染。船舶燃油、厨房烟囱排放导致浓度异常高的有机胺气体，混杂在湿度较高的扩散形态烟羽中，会直接被周围大量存在的粗模态、大粒径的海盐液滴吸附。位于顶层甲板的FMPS粒子计数器采样口连接有干燥器、过滤器，以防止大粒径的海浪飞沫让仪器报废，因此船舶平台本身产生的大粒径段颗粒并未进入到粒子计数器中，只有20-200 nm小粒径段的颗粒能进入采样器，这部分颗粒并不是新粒子形成，而是已经存在的干扰源，不会影响到观测成核速率_J_obs_的计算。而滤膜采集法所用MOUDI采集器的进气口，没有连接干燥器，因为在撞击式分级采样中，干燥管会影响气流撞击膜片的速度、造成较大的误差。因此船舶排放含有机胺的颗粒在0.1-2.5 μm全部会被采集到。

![C类数据，仪器监测界面。](https://upload-images.jianshu.io/upload_images/17085473-20130923fe8e67c2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

因此，当出现C类数据，模拟成核速率远远大于观测成核速率时，应该考虑监测平台排放等异常源的干扰。
*********************************************************************************
#### 4. 初步结论与展望

以往的理论计算研究大多关注近地面大气的区域性成核事件。而在野外走航观测活动中，背景气溶胶粒子以及监测平台本身排放的细颗粒物，干扰了商业化粒子计数仪器对新粒子形成事件的识别。本研究探索出一条新的技术路线，采用团簇动力学计算的成核速率，与粒子计数器观测得到的成核速率对比，能够有效辅助对观测数据误差的鉴定。借此将理论计算的适用性可以扩展到识别非区域性的新粒子形成事件，例如拉格朗日系统中的船载或者机载走航观测。
*********************************************************************************
#### 参考文献

Janssen, R. H. H. et al. Estimating seasonal variations in cloud droplet number concentration over the boreal forest from satellite observations. Atmos. Chem. Phys. 11, 7701-7713, (2011).

KANGASLUOMA J, ATTOUI M. Review of sub-3 nm condensation particle counters, calibrations, and cluster generation methods [J]. Aerosol Science and Technology, 2019, 53(11): 1277-310.

KERMINEN V-M, KULMALA M. Analytical formulae connecting the “real” and the “apparent” nucleation rate and the nuclei number concentration for atmospheric nucleation events [J]. Journal of Aerosol Science, 2002, 33(4): 609-22.

Kulmala, M. et al. Formation and growth rates of ultrafine atmospheric particles: a review of observations. Journal of Aerosol Science 35, 143-176, (2004).

Kulmala, M. et al. On the growth of nucleation mode particles: source rates of condensable vapor in polluted and clean environments. Atmos. Chem. Phys. 5, 409-416,  (2005).

Kulmala, M. et al. Measurement of the nucleation of atmospheric aerosol particles. Nature Protocols 7, 1651-1667, doi:10.1038/nprot.2012.091 (2012).

Lehtipalo, K. et al. Multicomponent new particle formation from sulfuric acid, ammonia, and biogenic vapors. Science Advances 4, eaau5363 (2018).

Li, J., Wu, N., Chu, B., Ning, A. & Zhang, X. Molecular-level study on the role of methanesulfonic acid in iodine oxoacid nucleation. Atmos. Chem. Phys. 24, 3989-4000 (2024).

Li, J., Ning, A., Liu, L. & Zhang, X. Atmospheric Bases-Enhanced Iodic Acid Nucleation: Altitude-Dependent Characteristics and Molecular Mechanisms. Environmental Science & Technology 58, 16962-16973,  (2024).

Li, J., Ning, A., Liu, L., Deng, X. & Zhang, X. Mechanistic insights into marine boundary layer nucleation: synergistic interactions of typical sulfur, iodine, and nitrogen precursors. Atmos. Chem. Phys. 26, 4423-4437, doi:10.5194/acp-26-4423-2026 (2026).

McGrath, M. J. et al. Atmospheric Cluster Dynamics Code: a flexible method for solution of the birth-death equations. Atmos. Chem. Phys. 12, 2345-2355, doi:10.5194/acp-12-2345-2012 (2012).

NIEMINEN T, KERMINEN V M, PETäJä T, et al. Global analysis of continental boundary layer new particle formation based on long-term measurements [J]. Atmos Chem Phys, 2018, 18(19): 14737-56.

Salignat, R. et al. Measurement report: Insights into the chemical composition and origin of molecular clusters and potential precursor molecules present in the free troposphere over the southern Indian Ocean: observations from the Maïdo Observatory (2150 m a.s.l., Réunion). Atmos. Chem. Phys. 24, 3785-3812, (2024).

Xia D , Chen J , Yu H ,et al.Formation Mechanisms of Iodine-Ammonia Clusters in Polluted Coastal Areas Unveiled by Thermodynamics and Kinetic Simulations[J].Environmental Science & Technology: ES&T, 2020(15):54.

Xie, H. et al. Concentration and size distribution of water-extracted dimethylaminium and trimethylaminium in atmospheric particles during nine campaigns - Implications for sources, phase states and formation pathways. Science of The Total Environment 631–632, 130-141 (2018).

Yu H , Ren L , Huang X ,et al.Iodine speciation and size distribution in ambient aerosols at a coastal new particle formation hotspot in China[J].Atmospheric Chemistry and Physics, 2019.

Chen, D. et al. Mapping gaseous dimethylamine, trimethylamine, ammonia, and their particulate counterparts in marine atmospheres of China's marginal seas – Part 1: Differentiating marine emission from continental transport. Atmos. Chem. Phys. 21, 16413-16425, doi:10.5194/acp-21-16413-2021 (2021).

Yu, F. & Luo, G. Modeling of gaseous methylamines in the global atmosphere: impacts of oxidation and aerosol uptake. Atmos. Chem. Phys. 14, 12455-12464, doi:10.5194/acp-14-12455-2014 (2014).

Wang, L., Lal, V., Khalizov, A. F. & Zhang, R. Heterogeneous Chemistry of Alkylamines with Sulfuric Acid: Implications for Atmospheric Formation of Alkylaminium Sulfates. Environmental Science & Technology 44, 2461-2465, doi:10.1021/es9036868 (2010).
*********************************************************************************
