# 快速入门

## YOLOV8

深度学习的入门其实非常的简单，这里我们用人工智能计算机视觉中的一个小分支_**目标检测**_来进行教学，使用的是到2023/9/26为止的最新的YOLOv8模型进行模型的预测，接下来打开Pycharm

首先安装一下库

![](https://raw.githubusercontent.com/lsewcx/markdown/main/img/%E7%BB%88%E7%AB%AF.png)

```python
!pip install ultralytics
```

```python
from ultralytics import YOLO

if __name__ == '__main__':
    model = YOLO("yolov8n.yaml")
    model = YOLO("yolov8n.pt")

    # Use the model
    model.train(data="coco128.yaml", epochs=3)  # 训练
    metrics = model.val()  # 评估
    results = model("https://ultralytics.com/images/bus.jpg")
    path = model.export(format="onnx")  # 导出onnx模型
```

然后在运行完的下面会显示评估后的照片在哪里，/runs/detect/val/文件夹下可以点击照片类似这样的

![](https://raw.githubusercontent.com/lsewcx/markdown/main/img/yolov8%E6%88%AA%E5%9B%BE.png)

_**恭喜你你已经入门深度学习拉**_

[如果需要视频教程的话可以参考](https://www.bilibili.com/video/BV1p84y1D7fM/?spm\_id\_from=333.999.0.0\&vd\_source=7dec7c8531017085df990bfd303b108f)

## Pytoch

```python
# 以 CIFAR10 数据集为例，展示一下完整的模型训练套路，完成对数据集的分类问题
import torchvision

from torch import nn
from torch.utils.data import DataLoader
from torch.utils.tensorboard import SummaryWriter
import torch
import time

# 定义训练的设备
device = torch.device("cuda")


# 准备数据集
train_data = torchvision.datasets.CIFAR10(root="dataset", train=True, transform=torchvision.transforms.ToTensor(),
                                          download=True)
test_data = torchvision.datasets.CIFAR10(root="dataset", train=False, transform=torchvision.transforms.ToTensor(),
                                         download=True)

# 获得数据集的长度 len(), 即length
train_data_size = len(train_data)
test_data_size = len(test_data)

# 格式化字符串, format() 中的数据会替换 {}
print("训练数据集的长度为: {}".format(train_data_size))
print("测试数据集的长度为: {}".format(test_data_size))

# 利用DataLoader 来加载数据
train_dataloader = DataLoader(train_data, batch_size=64)
test_dataloader = DataLoader(test_data, batch_size=64)


# 创建网络模型
class Model(nn.Module):
    def __init__(self) -> None:
        super().__init__()
        self.model = nn.Sequential(
            nn.Conv2d(3, 32, 5, 1, 2),
            nn.MaxPool2d(2),
            nn.Conv2d(32, 32, 5, 1, 2),
            nn.MaxPool2d(2),
            nn.Conv2d(32, 64, 5, 1, 2),
            nn.MaxPool2d(2),
            nn.Flatten(),
            nn.Linear(64 * 4 * 4, 64),
            nn.Linear(64, 10)
        )

    def forward(self, input):
        input = self.model(input)
        return input


model = Model()
model = model.to(device)  # 在 GPU 上进行训练

# 创建损失函数
loss_fn = nn.CrossEntropyLoss()
loss_fn = loss_fn.to(device)  # 在 GPU 上进行训练

# 优化器
learning_rate = 1e-2  # 1e-2 = 1 * (10)^(-2) = 1 / 100 = 0.01
optimizer = torch.optim.SGD(model.parameters(), lr=learning_rate)

# 设置训练网络的一些参数
total_train_step = 0  # 记录训练的次数
total_test_step = 0  # 记录测试的次数
epoch = 20  # 训练的轮数

# 添加tensorboard
writer = SummaryWriter("logs_train")
start_time = time.time()  # 开始训练的时间
for i in range(epoch):
    print("------第 {} 轮训练开始------".format(i + 1))

    # 训练步骤开始
    for data in train_dataloader:
        imgs, targets = data
        imgs = imgs.to(device)
        targets = targets.to(device)
        outputs = model(imgs)  # 将训练的数据放入
        loss = loss_fn(outputs, targets)  # 得到损失值

        optimizer.zero_grad()  # 优化过程中首先要使用优化器进行梯度清零
        loss.backward()  # 调用得到的损失，利用反向传播，得到每一个参数节点的梯度
        optimizer.step()  # 对参数进行优化
        total_train_step += 1  # 上面就是进行了一次训练，训练次数 +1

        # 只有训练步骤是100 倍数的时候才打印数据，可以减少一些没有用的数据，方便我们找到其他数据
        if total_train_step % 100 == 0:
            end_time = time.time()  # 训练结束时间
            print("训练时间: {}".format(end_time - start_time))
            print("训练次数: {}, Loss: {}".format(total_train_step, loss))
            writer.add_scalar("train_loss", loss.item(), total_train_step)

    # 如何知道模型有没有训练好，即有咩有达到自己想要的需求
    # 我们可以在每次训练完一轮后，进行一次测试，在测试数据集上跑一遍，以测试数据集上的损失或正确率评估我们的模型有没有训练好

    # 顾名思义，下面的代码没有梯度，即我们不会利用进行调优
    total_test_loss = 0
    total_accuracy = 0  # 准确率
    with torch.no_grad():
        for data in test_dataloader:  # 测试数据集中取数据
            imgs, targets = data
            imgs = imgs.to(device)
            targets = targets.to(device)
            outputs = model(imgs)
            loss = loss_fn(outputs, targets)  # 这里的 loss 只是一部分数据(data) 在网络模型上的损失
            total_test_loss = total_test_loss + loss  # 整个测试集的loss
            accuracy = (outputs.argmax(1) == targets).sum()  # 分类正确个数
            total_accuracy += accuracy  # 相加

    print("整体测试集上的loss: {}".format(total_test_loss))
    print("整体测试集上的正确率: {}".format(total_accuracy / test_data_size))
    writer.add_scalar("test_loss", total_test_loss)
    writer.add_scalar("test_accuracy", total_accuracy / test_data_size, total_test_step)
    total_test_loss += 1  # 测试完了之后要 +1

    torch.save(model, "model_{}.pth".format(i))
    print("模型已保存")

writer.close()

```

## tensorflow

```python
import tensorflow as tf
mnist = tf.keras.datasets.mnist

(x_train, y_train), (x_test, y_test) = mnist.load_data()
x_train, x_test = x_train / 255.0, x_test / 255.0
model = tf.keras.models.Sequential([
  tf.keras.layers.Flatten(input_shape=(28, 28)),
  tf.keras.layers.Dense(128, activation='relu'),
  tf.keras.layers.Dropout(0.2),
  tf.keras.layers.Dense(10)
])
predictions = model(x_train[:1]).numpy()
predictions
tf.nn.softmax(predictions).numpy()
loss_fn = tf.keras.losses.SparseCategoricalCrossentropy(from_logits=True)
loss_fn(y_train[:1], predictions).numpy()
model.compile(optimizer='adam',
              loss=loss_fn,
              metrics=['accuracy'])
model.fit(x_train, y_train, epochs=5)
model.evaluate(x_test,  y_test, verbose=2)
probability_model = tf.keras.Sequential([
  model,
  tf.keras.layers.Softmax()
])
probability_model(x_test[:5])
```

#### 在后面的教程中，我们会教导如何使用自己的数据集，去训练，部署自己的模型，同时会分享一些常用的资料等
