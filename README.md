# TensorFlowLite
## 基于TensorFlow Lite实现的Android花卉识别应用
#### 1.在Android studio上导入项目，将手机设置为开发者模式，并打开USB调试和“仅充电”模式下运行ADB调试，用USB连接手机和电脑，运行项目，实现如下图所示效果：
![效果图](https://github.com/choujvzi/TensorFlowLite/blob/master/screenshots/fake.jpg)

#### 2.右键“start”模块，然后New>Other>TensorFlow Lite Model，选择finish模块中ml文件下的FlowerModel.tflite，点击“Finish”完成模型导入。
#### 3.View>Tool Windows>TODO
#### 4.定位“start”模块MainActivity.kt文件的TODO 1，添加初始化训练模型的代码：
```kotlin
private class ImageAnalyzer(ctx: Context, private val listener: RecognitionListener) :
        ImageAnalysis.Analyzer {

  ...
  // TODO 1: Add class variable TensorFlow Lite Model
  private val flowerModel = FlowerModel.newInstance(ctx)

  ...
}
```
