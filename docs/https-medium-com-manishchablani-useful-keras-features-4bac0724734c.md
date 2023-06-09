# 有用的 Keras 功能

> 原文：<https://towardsdatascience.com/https-medium-com-manishchablani-useful-keras-features-4bac0724734c?source=collection_archive---------0----------------------->

以下是一些有趣功能的总结，我觉得在我构建深度学习管道时，我会发现参考这些功能很有用，也就是我通常不记得的东西。来自 Keras 文档 https://keras.io 和其他在线帖子。

# 当验证损失不再减少时，我如何中断培训？

您可以使用`EarlyStopping`回调:

```
**from** keras.callbacks **import** EarlyStopping
early_stopping = EarlyStopping(monitor='val_loss', patience=2)
model.fit(X, y, validation_split=0.2, callbacks=[early_stopping])
```

# 如何获得中间层的输出？

一个简单的方法是创建一个新的`Model`，它将输出您感兴趣的图层:

```
**from** keras.models **import** Modelmodel = ...  *# create the original model*layer_name = 'my_layer'
intermediate_layer_model = Model(inputs=model.input,
                                 outputs=model.get_layer(layer_name).output)
intermediate_output = intermediate_layer_model.predict(data)
```

或者，您可以构建一个 Keras 函数，在给定特定输入的情况下返回特定图层的输出，例如:

```
**from** keras **import** backend **as** K*# with a Sequential model*
get_3rd_layer_output = K.function([model.layers[0].input],
                                  [model.layers[3].output])
layer_output = get_3rd_layer_output([X])[0]
```

类似地，您可以直接构建一个 Theano 和 TensorFlow 函数。

请注意，如果您的模型在训练和测试阶段有不同的行为(例如，如果它使用`Dropout`、`BatchNormalization`等)。)，您需要将学习阶段标志传递给您的函数:

```
get_3rd_layer_output = K.function([model.layers[0].input, K.learning_phase()],
                                  [model.layers[3].output])*# output in test mode = 0*
layer_output = get_3rd_layer_output([X, 0])[0]*# output in train mode = 1*
layer_output = get_3rd_layer_output([X, 1])[0]
```

# 如何在 Keras 中使用预训练模型？

代码和预训练权重可用于以下影像分类模型:

*   例外
*   VGG16
*   VGG19
*   ResNet50
*   盗梦空间 v3

它们可以从`keras.applications`模块导入:

```
**from** keras.applications.xception **import** Xception
**from** keras.applications.vgg16 **import** VGG16
**from** keras.applications.vgg19 **import** VGG19
**from** keras.applications.resnet50 **import** ResNet50
**from** keras.applications.inception_v3 **import** InceptionV3model = VGG16(weights='imagenet', include_top=**True**)
```

关于一些简单的使用示例，请参见[应用模块](https://keras.io/applications)的文档。

有关如何使用这种预训练模型进行特征提取或微调的详细示例，请参见[这篇博文](http://blog.keras.io/building-powerful-image-classification-models-using-very-little-data.html)。

VGG16 模型也是几个 Keras 示例脚本的基础:

*   [风格转移](https://github.com/fchollet/keras/blob/master/examples/neural_style_transfer.py)
*   [特征可视化](https://github.com/fchollet/keras/blob/master/examples/conv_filter_visualization.py)
*   [深梦](https://github.com/fchollet/keras/blob/master/examples/deep_dream.py)

# [使用非常少的数据构建强大的图像分类模型](https://blog.keras.io/building-powerful-image-classification-models-using-very-little-data.html)

## [https://blog . keras . io/building-powerful-image-class ification-models-using-very-little-data . html](https://blog.keras.io/building-powerful-image-classification-models-using-very-little-data.html)

## 数据预处理和数据扩充

```
from keras.preprocessing.image import ImageDataGenerator

datagen = ImageDataGenerator(
        rotation_range=40,
        width_shift_range=0.2,
        height_shift_range=0.2,
        rescale=1./255,
        shear_range=0.2,
        zoom_range=0.2,
        horizontal_flip=True,
        fill_mode='nearest')
```

这些只是可用选项中的一部分(更多信息，请参见文档)。让我们快速回顾一下我们刚刚写的内容:

*   `rotation_range`是以度为单位的值(0-180)，在此范围内随机旋转图片
*   `width_shift`和`height_shift`是随机垂直或水平平移图片的范围(作为总宽度或高度的一部分)
*   `rescale`是一个值，在进行任何其他处理之前，我们会将数据乘以该值。我们的原始图像由 0-255 的 RGB 系数组成，但是这样的值对于我们的模型来说太高而无法处理(给定典型的学习率)，所以我们通过 1/255 的缩放将目标值设置在 0 和 1 之间。因素。
*   `shear_range`用于随机应用[剪切变换](https://en.wikipedia.org/wiki/Shear_mapping)
*   `zoom_range`用于图片内部随机缩放
*   `horizontal_flip`用于在没有水平不对称假设的情况下，随机翻转一半水平相关的图像(如真实图片)。
*   `fill_mode`是用于填充新创建像素的策略，可在旋转或宽度/高度移动后出现。

现在，让我们开始使用该工具生成一些图片，并将它们保存到一个临时目录中，这样我们就可以感受一下我们的增强策略正在做什么——在这种情况下，我们禁用了重新缩放，以保持图像可显示:

让我们准备我们的数据。我们将使用`.flow_from_directory()`直接从各自文件夹中的 jpg 生成批量图像数据(及其标签)。

```
img = load_img('data/train/cats/cat.0.jpg')  # this is a PIL image
x = img_to_array(img)  # this is a Numpy array with shape (3, 150, 150)
x = x.reshape((1,) + x.shape)  # this is a Numpy array with shape (1, 3, 150, 150)

# the .flow() command below generates batches of randomly transformed images
# and saves the results to the `preview/` directory
i = 0
for batch in datagen.flow(x, batch_size=1,
                          save_to_dir='preview', save_prefix='cat', save_format='jpeg'):
    i += 1
    if i > 20:
        break  # otherwise the generator would loop indefinitelybatch_size = 16

# this is the augmentation configuration we will use for training
train_datagen = ImageDataGenerator(
        rescale=1./255,
        shear_range=0.2,
        zoom_range=0.2,
        horizontal_flip=True)

# this is the augmentation configuration we will use for testing:
# only rescaling
test_datagen = ImageDataGenerator(rescale=1./255)

# this is a generator that will read pictures found in
# subfolers of 'data/train', and indefinitely generate
# batches of augmented image data
train_generator = train_datagen.flow_from_directory(
        'data/train',  # this is the target directory
        target_size=(150, 150),  # all images will be resized to 150x150
        batch_size=batch_size,
        class_mode='binary')  # since we use binary_crossentropy loss, we need binary labels

# this is a similar generator, for validation data
validation_generator = test_datagen.flow_from_directory(
        'data/validation',
        target_size=(150, 150),
        batch_size=batch_size,
        class_mode='binary')
```

我们现在可以使用这些生成器来训练我们的模型。每个历元在 GPU 上需要 20–30 秒，在 CPU 上需要 300–400 秒。所以如果你不着急的话，在 CPU 上运行这个模型是完全可行的。

```
model.fit_generator(
        train_generator,
        steps_per_epoch=2000 // batch_size,
        epochs=50,
        validation_data=validation_generator,
        validation_steps=800 // batch_size)
model.save_weights('first_try.h5')  # always save your weights after training or during training
```

这种方法使我们在 50 个时期后达到 0.79–0.81 的验证精度(这是一个任意选取的数字，因为模型很小，并且使用了积极的压降，所以到那时它似乎不会过度拟合)

## 使用预训练网络的瓶颈功能:一分钟内 90%的准确率

我们的策略如下:我们将只实例化模型的卷积部分，直到全连接层。然后，我们将在我们的训练和验证数据上运行该模型一次，在两个 numpy 阵列中记录输出(来自 VGG16 模型的“瓶颈特性”:全连接层之前的最后激活映射)。然后，我们将在存储的特征之上训练一个小的全连接模型。

我们离线存储特征而不是在冻结的卷积基础上直接添加全连接模型并运行整个过程的原因是计算效率。运行 VGG16 是很昂贵的，尤其是如果你在 CPU 上工作，我们希望只做一次。请注意，这阻止了我们使用数据扩充。

我们达到了 0.90–0.91 的验证精度:一点也不差。这肯定部分是由于基础模型是在已经有狗和猫的数据集上训练的(在数百个其他类中)。

## 微调预训练网络的顶层

为了进一步改善我们之前的结果，我们可以尝试在顶级分类器旁边“微调”VGG16 模型的最后一个卷积块。微调包括从训练好的网络开始，然后使用非常小的权重更新在新的数据集上重新训练它。在我们的案例中，这可以通过 3 个步骤来完成:

*   实例化 VGG16 的卷积基并加载其权重
*   在顶部添加我们之前定义的全连接模型，并加载其权重
*   冻结 VGG16 模型的层，直到最后一个卷积块

请注意:

*   为了进行微调，所有层都应该从经过适当训练的权重开始:例如，你不应该在预先训练的卷积基础上，加上随机初始化的全连接网络。这是因为由随机初始化的权重触发的大梯度更新会破坏卷积基中的学习权重。在我们的情况下，这就是为什么我们首先训练顶级分类器，然后才开始微调卷积权重。
*   我们选择仅微调最后一个卷积块，而不是整个网络，以防止过拟合，因为整个网络将具有非常大的熵容量，因此很容易过拟合。低级卷积块学习到的特征比高级卷积块更通用，更不抽象，因此保持前几个块固定(更通用的特征)并且只微调最后一个(更专用的特征)是明智的。
*   微调应该以非常慢的学习速率进行，通常使用 SGD 优化器，而不是自适应学习速率优化器，如 RMSProp。这是为了确保更新的幅度保持很小，以免破坏先前学习的功能。

# 什么是全球平均池？

## 引用谷歌搜索“全球平均池”的第一篇论文。[http://arxiv.org/pdf/1312.4400.pdf](http://arxiv.org/pdf/1312.4400.pdf)

> *CNN 没有采用传统的全连接层进行分类，而是通过全局平均池层直接输出最后一层 mlpconv 特征图的空间平均值作为类别的置信度，然后将得到的向量送入 softmax 层。在传统的 CNN 中，很难解释来自目标成本层的类别级信息如何传递回先前的卷积层，因为完全连接的层在它们之间充当黑盒。相比之下，全局平均池更有意义和可解释性，因为它加强了特征地图和类别之间的对应性，这通过使用微观网络的更强的局部建模而成为可能。此外，完全连接的层容易过拟合，并严重依赖于下降正则化[4] [5]，而全局平均池本身就是一个结构正则化，它本身可以防止整个结构的过拟合。*

和

> *在本文中，我们提出了另一种称为全局平均池的策略来取代 CNN 中传统的全连接层。其思想是在最后的 mlpconv 层中为分类任务的每个相应类别生成一个特征图。我们没有在特征地图上添加完全连接的层，而是取每个特征地图的平均值，并将结果向量直接输入 softmax 层。与完全连接的图层相比，全局平均池的一个优势是，它通过加强要素地图和类别之间的对应关系，更适合卷积结构。因此，特征图可以很容易地解释为类别置信度图。另一个优点是在全局平均池中没有要优化的参数，因此在这一层避免了过拟合。此外，全局平均池汇总了空间信息，因此对输入的空间平移更具鲁棒性。*
> 
> *我们可以将全局平均池视为一种结构正则化器，它明确地将特征映射强制为概念(类别)的置信度映射。这通过 mlpconv 层成为可能，因为它们比 GLMs 更好地逼近置信图。*

在有 10 个分类的情况下(CIFAR10，MNIST)。

这意味着，如果在最后一次卷积结束时有一个 3D 8，8，128 张量，在传统方法中，你要将其展平为大小为 8x8x128 的 1D 矢量。然后添加一个或几个完全连接的层，最后添加一个 softmax 层，将大小减少到 10 个分类类别，并应用 softmax 运算符。

全局平均池意味着你有一个 3D 8，8，10 张量，计算 8，8 切片的平均值，你最终得到一个形状为 1，1，10 的 3D 张量，你将它整形为形状为 10 的 1D 向量。然后添加一个 softmax 运算符，中间没有任何运算。平均池之前的张量应该具有与您的模型具有的分类类别一样多的通道。

该文件并不清楚，但当他们说“softmax 层”时，他们指的是 softmax 操作符，而不是与 softmax 激活完全连接的层。

不是 y=softmax(W*flatten(GAP(x))+b)而是 y=softmax(flatten(GAP(x)))。

# 在一组新的类上微调 InceptionV3

```
**from** keras.applications.inception_v3 **import** InceptionV3
**from** keras.preprocessing **import** image
**from** keras.models **import** Model
**from** keras.layers **import** Dense, GlobalAveragePooling2D
**from** keras **import** backend **as** K*# create the base pre-trained model*
base_model = InceptionV3(weights='imagenet', include_top=**False**)*# add a global spatial average pooling layer*
x = base_model.output
x = GlobalAveragePooling2D()(x)
*# let's add a fully-connected layer*
x = Dense(1024, activation='relu')(x)
*# and a logistic layer -- let's say we have 200 classes*
predictions = Dense(200, activation='softmax')(x)*# this is the model we will train*
model = Model(inputs=base_model.input, outputs=predictions)*# first: train only the top layers (which were randomly initialized)*
*# i.e. freeze all convolutional InceptionV3 layers*
**for** layer **in** base_model.layers:
    layer.trainable = **False***# compile the model (should be done *after* setting layers to non-trainable)*
model.compile(optimizer='rmsprop', loss='categorical_crossentropy')*# train the model on the new data for a few epochs*
model.fit_generator(...)*# at this point, the top layers are well trained and we can start fine-tuning*
*# convolutional layers from inception V3\. We will freeze the bottom N layers*
*# and train the remaining top layers.**# let's visualize layer names and layer indices to see how many layers*
*# we should freeze:*
**for** i, layer **in** enumerate(base_model.layers):
   print(i, layer.name)*# we chose to train the top 2 inception blocks, i.e. we will freeze*
*# the first 172 layers and unfreeze the rest:*
**for** layer **in** model.layers[:172]:
   layer.trainable = **False**
**for** layer **in** model.layers[172:]:
   layer.trainable = **True***# we need to recompile the model for these modifications to take effect*
*# we use SGD with a low learning rate*
**from** keras.optimizers **import** SGD
model.compile(optimizer=SGD(lr=0.0001, momentum=0.9), loss='categorical_crossentropy')*# we train our model again (this time fine-tuning the top 2 inception blocks*
*# alongside the top Dense layers*
model.fit_generator(...)
```

# 如何使用有状态 rnn？

使 RNN 有状态意味着每批样本的状态将被重新用作下一批样本的初始状态。

因此，当使用有状态 rnn 时，假设:

*   所有批次都有相同数量的样本
*   如果`X1`和`X2`是连续批次的样品，那么`X2[i]`是`X1[i]`的后续序列，对于每个`i`。

要在 RNNs 中使用状态，您需要:

*   通过向模型中的第一层传递一个`batch_size`参数，显式指定您正在使用的批量大小。例如`batch_size=32`对于 10 个时间步长的 32 样本批次序列，每个时间步长具有 16 个特征。
*   在你的 RNN 图层中设置`stateful=True`。
*   调用 fit()时指定`shuffle=False`。

要重置累积的状态:

*   使用`model.reset_states()`重置模型中所有层的状态
*   使用`layer.reset_states()`重置特定有状态 RNN 层的状态

示例:

```
X  *# this is our input data, of shape (32, 21, 16)*
*# we will feed it to our model in sequences of length 10*model = Sequential()
model.add(LSTM(32, input_shape=(10, 16), batch_size=32, stateful=**True**))
model.add(Dense(16, activation='softmax'))model.compile(optimizer='rmsprop', loss='categorical_crossentropy')*# we train the network to predict the 11th timestep given the first 10:*
model.train_on_batch(X[:, :10, :], np.reshape(X[:, 10, :], (32, 16)))*# the state of the network has changed. We can feed the follow-up sequences:*
model.train_on_batch(X[:, 10:20, :], np.reshape(X[:, 20, :], (32, 16)))*# let's reset the states of the LSTM layer:*
model.reset_states()*# another way to do it in this case:*
model.layers[0].reset_states()
```

注意，方法有`predict`、`fit`、`train_on_batch`、`predict_classes`等。所有的将更新模型中有状态层的状态。这不仅允许您进行状态训练，还允许您进行状态预测。