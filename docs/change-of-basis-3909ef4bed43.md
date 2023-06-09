# 变换

> 原文：<https://towardsdatascience.com/change-of-basis-3909ef4bed43?source=collection_archive---------8----------------------->

## 如果你认为这很容易，你可能做错了。

![](img/bd73308bf11c0eaa8fc3db1d8f738617.png)

If you’re struggling with coordinate system conversion, enjoy this sunset for a second, knowing your answer is just below.

我最近一直在做 [USD Unity SDK](https://github.com/Unity-Technologies/usd-unity-sdk/) ，有一个话题出现了几次，就是从右手系统(比如 OpenGL/USD)到左手系统(比如 Unity/DirectX)的基础转换。如果你需要将一个矩阵或向量从左手坐标系转换到右手坐标系，你知道我的痛苦；本着务实的精神，我将首先提出解决方案，然后我们可以深入讨论细节。我也将展示一个奇怪的技巧，谁知道呢，也许我们 ***可以*** 只是将 Z 乘以-1。

## TL；速度三角形定位法(dead reckoning)

下面是基本公式的完全通用的变化:

```
B = P * A * inverse(P)
```

博学的读者会将这种基变换公式识别为[相似变换](http://mathworld.wolfram.com/SimilarityTransformation.html)。它可以应用于右手坐标系中的矩阵`A`以产生左手坐标系中的等价矩阵`B`。矩阵`P`是基变换的变化。那么到底什么是基矩阵的变化呢？如果您的目的是将值从 DirectX 转换到 OpenGL 默认坐标系，这两个坐标系在 Z 轴上相差-1 的比例，那么基矩阵的变化就是这些坐标系之间的转换:

```
P = [[ 1  0  0  0]
     [ 0  1  0  0]
     [ 0  0 -1  0]
     [ 0  0  0  1]]
```

这个矩阵有一个特殊的性质，就是它是[对合](https://en.wikipedia.org/wiki/Involutory_matrix)(在求逆下不变)。还要注意，用这种基变换矩阵改变基公式只会导致六次不同的乘法。为了使解决方案完全具体化，下面是使用 Unity Engine API 的 C#实现:

```
Matrix4x4 ChangeBasis(Matrix4x4 input) {
    var basisChange = Matrix4x4.identity; // Invert the forward vector.
    basisChange[2, 2] = -1; // Note the inverse of this matrix is the matrix itself.
    var basisChangeInverse = basisChange; // This multiply could be simplified to
    // -1 * elements [2,6,8,9,11,14], which can be simplified 
    // further; see [Eberly's proof](https://answers.unity.com/storage/temp/12048-lefthandedtorighthanded.pdf) for details.
    return basisChange * input * basisChangeInverse;
}Vector3 ChangeBasis(Vector3 point) {
    UnityEngine.Matrix4x4 mat = UnityEngine.Matrix4x4.identity;
    mat[2, 2] = -1;
    return mat.MultiplyPoint3x4(point);
}
```

因此，对于矢量、变换、相机和灯光，你有了一个完全通用和对称的解决方案。请注意，更改整个资源的基础意味着转换点、变换、法线、切线和所有辅助数据(例如，作为着色器参数的方向向量)。这不是一个小任务。如果资源是动画的，您可能也需要每帧都这样做。

你可能会问自己，“但是我不能通过使用一个奇怪的技巧来避免所有这些乘法吗？”是的，但这实际上是两个技巧，而且是有代价的；但在进入技巧之前，让我们首先同意改变基础是正确的一般解决方案。

# 寻找火焰

任何需要在 DirectX 和 OpenGL 之间交换数据的人都感受到了需要在两个坐标系之间转换基础的痛苦。在找到完全通用的解决方案之前，我花了太多的时间寻找错误的解决方案，其中我试图简单地反转所有值的 Z 坐标。在检查位置时，这似乎是正确的，但是它没有考虑到旋转和转向。为了理解为什么这是不正确的，看一下一个矩阵的基的适当改变的效果是有帮助的:

```
[[ 1  0  0  0]      [[1 1 1 1]    [[1  0  0  0]     [[ 1  1 **-1**  1]
 [ 0  1  0  0]   x   [1 1 1 1]  x  [0  1  0  0]  =   [ 1  1 **-1**  1]
 [ 0  0 -1  0]       [1 1 1 1]     [0  0 -1  0]      [**-1 -1**  1 **-1**]
 [ 0  0  0  1]]      [1 1 1 1]]    [0  0  0  1]]     [ 1  1 **-1**  1]]
```

哦嗨，不止是 Z 翻译颠倒了！我们现在看到了我上面提到的六次乘法，很明显，这并不等同于 Z 乘以-1，但是为什么这个解是正确的呢？

也许你也偶然发现了大卫·埃伯利的这篇文章。虽然合乎逻辑，看似正确，并且只需要在三种特殊情况下进行四次矩阵乘法，但我很难看出它是如何推广的，我不想在没有真正理解我在做什么的情况下盲目应用该公式。

从线性代数中，我知道我真正想要的是执行基的变换，所以我开始为*而不是*寻找一些数学基础。我最终发现的是教科书中对基础变化的定义。

## 相似变换

在维基百科上，你会发现上面的公式，但是伴随着一个比艾伯利的更难以理解的描述。这种转变的基础实际上很容易计算和理解，但很难解释，所以在这里，我将引导您观看关于基础变化的 3Blue1Brown [视频](https://www.youtube.com/watch?v=P2LTAUO1TdA)。他在视频开始 11 分钟后到达相似性转换。

好了，现在我们都同意基的变化公式是完全通用的，完全正确的，让我们变得怪异。

# 一个奇怪的技巧:部分改变基础

我不喜欢这种转换需要每次转换两次矩阵乘法(模优化),并且必须应用于资产中的每个点、转换和法向(等等);同样，这对于动画来说可能特别慢——所以我们不能避免它吗？互联网的知识会告诉你，“不，这是无法避免的，忍着吧”，但这并不完全正确，假设你对一些警告感到满意。

让我们想一想基变换的变化是如何在我们的数据中体现出来的。假设我们有一个应用于顶点位置的变换链。在真实资产中，我们有大量的其他数据，但这种有限的世界观足以说明这个想法。我们的目标是将一个点从物体空间转换到世界空间。假设 T0..T2 是 4x4 矩阵变换，V 是要变换的 4x1 向量位置，当应用完全通用的基变换时，我们的矩阵乘法看起来像这样:

```
V' = P * T0 * inverse(P)
   * P * T1 * inverse(P)
   * P * T2 * inverse(P)
   * P * V
```

所有这些矩阵乘法看起来非常多余，难道我们不能在一个中间空间中操作，只在完成后应用转换吗？是的，但是我们希望避免在系统中的每个着色器中显式地编写这些代码。相反，我们利用了这样一个事实，即我们知道在一致的空间中有一个连续的子图(即一个输出对话步骤就足够了)。

```
V' = P * T0
       * T1
       * T2 * V
```

这是一个巨大的工作量减少！只有根变换需要转换，所有其他数据都可以保留在其原生坐标空间中。这行得通，因为 T0..T2 和 V 在同一个坐标系中，所以旋转按预期进行。此外，最终的输出转换 P 正确地转换了结果点，因为根据定义，它不能是旋转(它只是一个位置)。最后，摄像机位于 P 输出的空间中，因此结果场景看起来是正确的。那么有什么问题呢？

如果我们在包含相机变换时应用这个技巧，相机必须完全转换，或者我们将最终顶点值留在不同的坐标空间中，而不是通过这个相机查看它时它开始的位置。然而，为了将所有场景数据保持在一致的坐标空间中，我们可以改为通过相机的视图变换来完成基变换的部分改变:

```
C' = C * inverse(P)
```

现在，当我们在右手坐标系中渲染左手相机和数据时(例如)，典型的相机空间变换将导致正确的最终相似性变换，如下所示:

```
CameraSpaceV = (view) * (model) * (vertex)
             = C * T0 * T1 * T2 * V
             = inverse(P) * C * P * T0 * T1 * T2 * V
             = **P * C * inverse(P)** * T0 * T1 * T2 * V
```

现在我们有两个奇怪的把戏:)

最终结果是将输入资产数据的 O(N)次矩阵乘法减少到 O(1)。

## 警告选择器

实际上有几个值得一提的注意事项:

1.  导入时，这会将原始矩阵和顶点数据留在另一个坐标系中。任何手动检查这些数据的人可能会对他们所看到的与数据的值相比较而感到困惑。
2.  根变换将包含负比例。简单的矩阵分解算法将无法正确处理这种情况，并且会将缩放转换为旋转。当分解一个矩阵时，有可能检测到基标度的这种变化并正确地处理它。
3.  如果您正在操作直接应用于视图转换的矩阵数据，这个技巧将需要额外的修复。

# 结论

最重要的是，我希望这个完全通用的解决方案对任何在互联网上寻找快速解决方案的人都有帮助。其次，我希望指出所有数据都必须转换的事实揭示了这样一个推论，即它实际上充满了危险，并且“一个奇怪的把戏”/部分改变基础的警告在某些情况下可能实际上更可取，不仅是为了性能，而且是为了正确性。