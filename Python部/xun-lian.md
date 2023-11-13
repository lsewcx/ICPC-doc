# 训练

## 这次我们还将使用目标检测来作为培训的重点

## 1.数据集制作

### 1.1标注

标注是人工智能数据集制作的非常重要的环节，你可以不会\_**数据集清洗**\_，但是不能不会标注，在比赛中国即使是标注好的文件，也需要拿来看看有没有失误的地方无论是声音，图像，还是自然语言处理的数据集都需要进行标注，作为学习的资料

### 1.2常用标注的方法

#### 1.2.1使用软件

* labelme
* labelimg

这两个软件都可以通过pip安装来进行标注,这两个标注软件比较简单，同学们自行学习，这两个软件有什么缺点呢，就是图片需要一个一个的标，十分的费时费精力，

## 1.2.2使用百度的智能云平台

用百度的平台有什么好处呢，百度的平台是可以进行智能标注的，什么意思呢，用AI去标注AI训练的数据集，可以做到很快标注完大部分的照片这里的话我们具体的来介绍一下

[https://www.bilibili.com/video/BV1234y137Mt/?vd\_source=7dec7c8531017085df990bfd303b108f](https://www.bilibili.com/video/BV1234y137Mt/?vd\_source=7dec7c8531017085df990bfd303b108f)

### 注意点：

* 每个标签要标10个才可以智能标注，也就是自动标注

标注完后用roboflow去转换即可变成各种模型所需要的

## 1.2.3 yolov5划分数据集脚本

```python
import os
import shutil
import random

random.seed(0)


def split_data(file_path, xml_path, new_file_path, train_rate, val_rate, test_rate):
    each_class_image = []
    each_class_label = []
    for image in os.listdir(file_path):
        each_class_image.append(image)
    for label in os.listdir(xml_path):
        each_class_label.append(label)
    data = list(zip(each_class_image, each_class_label))
    total = len(each_class_image)
    random.shuffle(data)
    each_class_image, each_class_label = zip(*data)
    train_images = each_class_image[0:int(train_rate * total)]
    val_images = each_class_image[int(train_rate * total):int((train_rate + val_rate) * total)]
    test_images = each_class_image[int((train_rate + val_rate) * total):]
    train_labels = each_class_label[0:int(train_rate * total)]
    val_labels = each_class_label[int(train_rate * total):int((train_rate + val_rate) * total)]
    test_labels = each_class_label[int((train_rate + val_rate) * total):]

    for image in train_images:
        print(image)
        old_path = file_path + '/' + image
        new_path1 = new_file_path + '/' + 'train' + '/' + 'images'
        if not os.path.exists(new_path1):
            os.makedirs(new_path1)
        new_path = new_path1 + '/' + image
        shutil.copy(old_path, new_path)

    for label in train_labels:
        print(label)
        old_path = xml_path + '/' + label
        new_path1 = new_file_path + '/' + 'train' + '/' + 'labels'
        if not os.path.exists(new_path1):
            os.makedirs(new_path1)
        new_path = new_path1 + '/' + label
        shutil.copy(old_path, new_path)

    for image in val_images:
        old_path = file_path + '/' + image
        new_path1 = new_file_path + '/' + 'val' + '/' + 'images'
        if not os.path.exists(new_path1):
            os.makedirs(new_path1)
        new_path = new_path1 + '/' + image
        shutil.copy(old_path, new_path)

    for label in val_labels:
        old_path = xml_path + '/' + label
        new_path1 = new_file_path + '/' + 'val' + '/' + 'labels'
        if not os.path.exists(new_path1):
            os.makedirs(new_path1)
        new_path = new_path1 + '/' + label
        shutil.copy(old_path, new_path)

    for image in test_images:
        old_path = file_path + '/' + image
        new_path1 = new_file_path + '/' + 'test' + '/' + 'images'
        if not os.path.exists(new_path1):
            os.makedirs(new_path1)
        new_path = new_path1 + '/' + image
        shutil.copy(old_path, new_path)

    for label in test_labels:
        old_path = xml_path + '/' + label
        new_path1 = new_file_path + '/' + 'test' + '/' + 'labels'
        if not os.path.exists(new_path1):
            os.makedirs(new_path1)
        new_path = new_path1 + '/' + label
        shutil.copy(old_path, new_path)


if __name__ == '__main__':
    file_path = r"F:\python代码\aibisai123-2\valid\images" #都是图片的路径
    xml_path = r"F:\python代码\aibisai123-2\valid\labels"  #都是标注信息的路径
    new_file_path = r"F:\python代码\aibisai123-2\imageset" #自己建的想要塞进去的文件夹
    split_data(file_path, xml_path, new_file_path, train_rate=0.7, val_rate=0.1, test_rate=0.2)
```
