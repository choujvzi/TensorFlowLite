# TensorFlowLite
## 基于TensorFlow Lite实现的Android花卉识别应用
#### 1.在Android studio上导入项目，将手机设置为开发者模式，并打开USB调试和“仅充电”模式下运行ADB调试，用USB连接手机和电脑，运行项目，实现如下图所示效果：
![效果图](https://github.com/choujvzi/TensorFlowLite/blob/master/screenshots/fake.jpg)

#### 2.右键“start”模块，然后New>Other>TensorFlow Lite Model，选择finish模块中ml文件下的FlowerModel.tflite，点击“Finish”完成模型导入。
#### 3.View>Tool Windows>TODO
#### 4.定位“start”模块MainActivity.kt文件的TODO 1，添加初始化训练模型的代码：
```kotlin
 // TODO 1: Add class variable TensorFlow Lite Model
 private val flowerModel = FlowerModel.newInstance(ctx)
```
#### 5.在CameraX的analyze方法内部，需要将摄像头的输入ImageProxy转化为Bitmap对象，并进一步转化为TensorImage 对象
```kotlin
// TODO 2: Convert Image to Bitmap then to TensorImage
val tfImage = TensorImage.fromBitmap(toBitmap(imageProxy))
```
#### 6.
```kotlin
// TODO 3: Process the image using the trained model, sort and pick out the top results
  val outputs = flowerModel.process(tfImage)
      .probabilityAsCategoryList.apply {
          sortByDescending { it.score } // Sort with highest confidence first
      }.take(MAX_RESULT_DISPLAY) // take the top results
 ```
 #### 7.将识别的结果加入数据对象Recognition 中，包含label和score两个元素。后续将用于RecyclerView的数据显示
 ```kotlin
// TODO 4: Converting the top probability items into a list of recognitions
  for (output in outputs) {
      items.add(Recognition(output.label, output.score))
  }
 ```
#### 8.将原先用于虚拟显示识别结果的代码注释掉或者删除
```kotlin
// START - Placeholder code at the start of the codelab. Comment this block of code out.
for (i in 0..MAX_RESULT_DISPLAY-1){
    items.add(Recognition("Fake label $i", Random.nextFloat()))
}
// END - Placeholder code at the start of the codelab. Comment this block of code out.
```
#### 9.重新运行项目，实现如下结果：
![识别花卉](https://github.com/choujvzi/TensorFlowLite/blob/master/screenshots/huahui.jpg)
