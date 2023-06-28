---
layout: article
title: 体渲染-0 体渲染概述和资料归档
tags: ["ComputerGraphics", "Volume Rendering"]
key: 
aside:
  toc: true
sidebar:
  nav: VolumeRendering
---




> 这个系列的文章介绍了和体渲染相关的内容。本文对体渲染进行了一定程度的概述，同时记录一些可参考的学习资料。本文长期更新。


# 概述
基于网格（mesh）的渲染无疑占据了图形渲染领域的大头，体渲染无论是工业界的使用份额还是讲解和学习的资料，都相对较少。最近的工作中在研究体数据，所以本文记录一些目前为止了解到的体渲染相关资料，以供后续查找。

## 游戏中的体渲染
游戏中使用体素渲染器，一般是处于某种美术风格的偏好或是玩法的需求。最出名的体素游戏是：
- 我的世界，有一个开源的java版本，不过遗憾的是体素引擎应该是没有开源的。

一个以java为开发语言的开源体素游戏
- [Terasology](https://github.com/MovingBlocks/Terasology)


PolyVox: PolyVox 是一个开源的 C++ 体素库，用于创建和操作体素数据。它提供了高性能的体素操作算法，并支持体素渲染和碰撞检测。PolyVox 可以用于创建体素化的游戏世界、医学可视化和科学模拟等应用。
- [PolyVox](https://bitbucket.org/volumesoffun/polyvox/) 以及他的[主页](http://www.volumesoffun.com/polyvox-about/)



## 医疗影像中的体渲染
体渲染的最传统使用领域就是医疗影像的渲染。通过体素对病人内部组织结构的展示来判断病情，与体素渲染的特性天生契合。

## 游戏引擎中的体渲染
游戏引擎中往往利用体渲染来实现各种云、烟、雾等粒子效果。
- ThreeJS中的体素渲染 https://threejs.org/examples/?q=perlin#webgl2_volume_perlin



UE中一般用于实现一些粒子效果，您可以查看他们的源码链接
Volumetric Fog（体积雾）：UE提供了内置的体积雾特效，可以通过添加Volumetric Fog组件来创建逼真的雾效果。体积雾可以用于模拟大气效果、烟雾、云层等。
[UE中的体积雾](https://github.com/EpicGames/UnrealEngine/blob/463443057fb97f1af0d2951705324ce8818d2a55/Engine/Source/Runtime/Renderer/Private/VolumetricFog.cpp#L2)
Volumetric Light（体积光）：通过使用Volumetric Lightmaps（体积光照片）或Volumetric Lightmaps（体积光照片），可以在UE中实现逼真的体积光效果。体积光可以用于模拟阳光透射、室内照明效果等。
[UE中的体积光]()
Volumetric Clouds（体积云）：通过使用UE的特效工具和材质系统，可以创建逼真的体积云效果。体积云可以用于模拟动态云层、天空效果等。
[UE中的体积云]()
Material Volumetric（材质体积）：UE的材质系统支持体积纹理（Volume Texture）和体积材质（Volume Material），这使得开发者可以在材质中实现自定义的体积效果，如体积火焰、流体等。
[UE中的材质体积]()

一个为ue体渲染做的插件
[体渲染插件](https://github.com/Phyronnaz/VoxelPlugin)


# 资料

## 视频资料

## 书籍资料

**[Morgan Kaufmann] Visual Computing for Medicine Theory, Algorithms, and Applications 2nd Edition**
**real_time_volume_render**
**Real-Time Volume Graphics**

以上书籍的[下载链接]().

## 文章资料
xxx这个系列的书籍内部xxxx  


Volumetric Lighting，Fog，Atmospheric Scattering：  
**《Gpu Gems2》Accurate Atmospheric Scattering**：精确的大气散射效果，结算大气散射方程（Nishita），Rayleigh Scattering，Mie Scattering，最后增加HDR。

**《Gpu Gems3》Volumetric Light Scattering as a Post-Process**：用径向模糊后处理实现体积光效果，Prepass处理遮挡。

**《Gpu Pro3》An Approximation to the Chapman Grazing-Incidence Function for Atmospheric Scattering**：RayTracing，简化的Chapman function，模拟大气散射效果。

**《Gpu Pro5》High Performance Outdoor Light Scattering Using Epipolar Sampling**：Ray Marching，epipolar sampling，1D minimum/maximum binary trees，Physically

**《Gpu Pro5》Volumetric Light Effects in Killzone: Shadow Fall** ： 体积光，Dithered Ray Marching，3D Noise Tex

**《Gpu Pro6》Volumetric Fog and Lighting**：刺客信条4黑旗中的体积雾和体积光技术，理论还是比尔兰伯特定律和MieScatting，使用了Cumpute Shader计算，首先并行计算3D密度（噪声）图和雾效光照，再进行RayMarching，不同于KZ的Depth Ray Marching，直接在体素3DRayMarching，最后结果和Forward或Deferred的结合，Deferred可以和光照合并计算，还给出了down sample计算后up sample时aliasing的解决方案。

**《Gpu Pro6》Realistic Volumetric Explosions in Games**：思想类似于Ray Marching体积光，Ray Marching方式实现爆炸效果，使用Tessellation，3DNoise Texture，可以实现光照。不过相比于普通粒子，GPUpixel阶段消耗太高。

**《Gpu Pro6》Sparse Procedural Volume Rendering**：RayMarching体素实现爆炸浓烟等特效，使用层级的结构，降低Marching的消耗，使用CubeMap作为3DNoise。

**《Gpu Zen》Participating Media Using Extruded Light Volumes**：NVIDIA提供的一套体积光解决方案，更加基于物理的体积光大气散射效果，需要Tessellation生成载体Mesh，然后Raymarching。

Volumetirc Rendering：  
**《Gpu Gems1》Volume Rendering Techniques**：介绍了用排列观察面上的代理几何体实现基于纹理的体系渲染，并增加了阴影体，半透，随机细节等，优化了体渲染的效果。

**《Gpu Gems1》Applying Real-Time Shading to 3D Ultrasound Visualization**：类似上篇文章，介绍了体渲染的实际应用，根据三维超声波可视化实现着色。

**《Gpu Pro1》Efficient Rendering of Highly Detailed Volumetric Scenes with GigaVoxels**：Octree，Hierarchical Volume Ray Casting ，Voxel Mipmap，Mipmap based Blur，Dof，AA，优化体素内存Bandwidth。

**《Gpu Pro2》Adaptive Volumetric Shadow Maps**：对于粒子，烟雾，头发等体渲染实现软阴影效果，需要per-pixel linked lists，然后Filter。

**《Gpu Pro3》Volumetric Transparency with Per-Pixel Fragment Lists**：OIT，渲染烟雾，透明物体，Ray Tracing，Compute Shader，透明物体阴影。

**《Gpu Pro3》Practical Binary Surface and Solid Voxelization with Direct3D 11**：体素渲染，可以扩展实现GI，AO等。

**《Gpu Pro6》Smooth Probabilistic Ambient Occlusion for Volume Rendering**：体渲染中无法用深度图，通过3D Filter的方式实现AO效果，用多层嵌套的cube模拟计算遮蔽概率。

**《Gpu Pro6》Block-Wise Linear Binary Grids for Fast Ray-Casting Operations**：使用二分区块方法，实现更加快速的体素碰撞计算，可以更容易地计算简介光照，VPL等内容。




## 其他资料


# 参考链接
> [《Gpu Gems》《Gpu Pro》《Gpu Zen》系列读书笔记](https://blog.csdn.net/puppet_master/article/details/87172148)

<br />
