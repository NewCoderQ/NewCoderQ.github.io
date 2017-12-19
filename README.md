# Diabetic-Retinopathy-Detection
A private repository for Diabetic Retinopathy Detection.

## data
**train dataset:** 

|class_name | number|
|:---------:|:------:|
|total | 35126|
|0_NoDR |25810|
|1_Mild |2443|
|2_Moderate |5292|
|3_Severe |873|
|4_ProliferativeDR | 708|
|**train**|**25126**|
|**validation**|**10000**|

**web_page:** a folder for web pages

## 代码文件说明
`split_images_class.py`将图像数据从原始的各个类别都在同一个文件夹下整理成分类别存放，分别存在不同的文件夹下，
这样所有图像就从原始的一个文件夹分成了五个相互独立的五个子文件夹，子文件夹的名称就是图像所对应的类别名称。

`arrange_convert_data.py  dataset_utils.py  convert_diabete_images.py`
这三个python文件的作用就是将根据图像的label分好的图像整合成TFRecords格式的数据，
这样在训练过程中可以提高效率，减少读取图像文件的时间消耗。


## 项目进程
**2017/12/16 - 2017/12/17:** download the diabetic retinopathy dataset

**2017/12/18:**

将训练图像数据整理成这样的组织形式进行存储
* train_dataset/diabetes_images
	* 0_NoDR   				
	* 1_Mild				
	* 2_Moderate			
	* 3_Severe				
	* 4_ProliferativeDR

将图像文件转化成[TFRecords](https://www.tensorflow.org/versions/r0.10/api_docs/python/python_io.html#tfrecords-format-details)格式的数据，加快读取速度

* 将所有的图像数据分成两份：trian(25126), validation(10000)
* 分别将两个图像数据集分成5等分，保存在tfrecord文件中

|dataset_name|tfrecord_file_name|
|:----------:|:-----------:|
|train|diabetes_train_0000(0 - 4)-of-00005.tfrecord|
|validation|diabetes_validation_0000(0 - 4)-of-00005.tfrecord|

使用[Tensorflow](https://www.tensorflow.org/)官方提供的[`inception_v3`](https://arxiv.org/abs/1512.00567)网络来fine-tune pre-trained模型。

**2017/12/19:**

测试了一下昨天fine-tune的模型，在整个验证集的准确率大概在`73.8%`左右，没有做各个类别的准确率计算。

不选择从pre-trained模型进行fine-tune，直接从初始化的参数训练网络，网络还是选择[`inception_v3`](https://arxiv.org/abs/1512.00567).

准备做：
	1.通过图像预处理，挑选出原图中的眼球的部分
	2.尝试是用其他的网络来完成分类任务



## reference
[Google](https://www.google.com):[Development and Validation of a Deep Learning Algorithm for Detection of Diabetic Retinopathy in Retinal Fundus Photographs](https://static.googleusercontent.com/media/research.google.com/zh-CN//pubs/archive/45732.pdf)