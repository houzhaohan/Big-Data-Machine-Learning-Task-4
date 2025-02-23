# Identification of chicken heat stress behavior based on YOLOv5 基于YOLOv5的鸡热应激行为识别
大数据及农业应用-课程作业\
大三上

### 一、实验目的
基于YOLOv5的鸡热应激行为识别\
热应激是指在较高温度环境下肉鸡机体对热环境所做的非特异性反应的总和，包括生理生化反应、行为反应等。目前，环境参数法和行为分析法可用于快速判断肉鸡热应激，其中环境参数中常用温湿度指数（Temperature and Humidity Index, THI）进行判断，但此为间接指标，无法准确评估热应激。行为分析法则是通过行为动作判断鸡只状态。随着视觉技术与人工智能算法的发展，利用图像分析行为方法更多地应用于家禽行为的监测，这已成为一个重要研究领域。

### 二、实验原理
（1）图像采集系统\
![image](https://github.com/user-attachments/assets/fb804c3b-5653-43e6-a6ae-8824dc283845)\
![image](https://github.com/user-attachments/assets/22fe248c-db30-4bb9-a323-78825a9c0c16)\
![image](https://github.com/user-attachments/assets/55310923-94ea-4519-be1a-1d1af433969a)\
（2）张正友标定法\
![image](https://github.com/user-attachments/assets/c93e7d45-fbcf-4356-a7c5-0199fcf7086e)\
标定模版图

![image](https://github.com/user-attachments/assets/1aa051b8-2842-43a2-a8d1-a6aaa78ddd64)\
摄像机拍摄的不同角度的棋盘格图片
$$
\begin{pmatrix}
a & b \\
c & d
\end{pmatrix}
$$
$K= \begin{bmatrix} 505.4552 & 0 & 0 \\ 0.1921 & 507.391 & 0 \\ 429.491 & 252.5465 & 1 \end{bmatrix}$  
此次校正误差为0.18pixel属于合理误差，在0-0.5pixel范围以内。

![image](https://github.com/user-attachments/assets/38153535-1170-4bf7-9323-060fe0750fb4)\
![image](https://github.com/user-attachments/assets/5ba655d2-f4ca-40a2-9b8f-d4afb7e04efd)\
(a) 校正前图

![image](https://github.com/user-attachments/assets/2f387c66-a6f9-4854-b21b-ab9a54cfbb61)\
![image](https://github.com/user-attachments/assets/5683920a-36d0-46e6-b8bc-cc3b52a56ace)\
(b) 校正后图

（3）行为分类\
![image](https://github.com/user-attachments/assets/39713e16-69e0-4bae-8879-ed6e97c13191)\
（4）PyTorch\
PyTorch是torch的python版本，是由Facebook开源的神经网络框架。\
Torch是一个经典的对多维矩阵数据进行操作的张量（tensor）库，在机器学习和其他数学密集型应用有广泛应用。与Tensorflow的静态计算图不同，PyTorch的计算图是动态的，可以根据计算需要实时改变计算图。
作为经典机器学习库Torch的端口，PyTorch为 Python语言使用者提供了舒 适的写代码选择。\
（5）YOLO模型\
“You Only Look Once”或“ YOLO”是一个对象检测算法的名字，这是 Redmon等人在2016年的一篇研究论文中命名的。YOLO实现了自动驾驶汽车等前沿技术中使用的实时对象检测。\
YOLO将对象检测重新定义为一个回归问题。它将单个卷积神经网络(CNN)应用于整个图像，将图像分成网格，并预测每个网格的类概率和边界框。例如，以一个100x100的图像为例。我们把它分成网格，比如7x7。\
然后，对于每个网格，网络都会预测一个边界框和与每个类别（汽车，行人，交通信号灯等）相对应的概率。\
YOLO非常快。由于检测问题是一个回归问题，所以不需要复杂的管道。它比“R-CNN”快 1000倍，比“Fast R-CNN”快100倍。它能够处理实时视频流，延迟小于25毫秒。它的精度 是以前实时系统的两倍多。同样重要的是，YOLO遵循的是“端到端深度学习”的实践。

### 三、实验步骤
（1）鸡图像数据集的制作\
• 图像重新命名\
• 图像数据集增广（旋转、平移等）\
• Labelme软件的制作\
• Labelme标准格式转化\
（2）模型训练\
• 用train.py文件训练模型\
• 训练好的模型会得到一个权重文件后缀名为.pth，存放位置如下。\
• 根据对模型精度的要求，我们可以重复训练自己的模型直到有一个最优的epoch


### 四、实验结果
![image](https://github.com/user-attachments/assets/0cb91d4d-f9e0-4aac-b449-2a4a3e719dfc)\
正在用train.py训练模型

![image](https://github.com/user-attachments/assets/7f6a9c2e-f1c7-4837-87e6-322f8d782d86)\
ep001-loss3.711-val_loss3.728.pth为新训练的模型

![image](https://github.com/user-attachments/assets/fd6a4779-2419-4413-a9a1-67473470c8b7)\
正在运行predict.py生成标注的图片，右侧文件夹是正在生成的图片

![image](https://github.com/user-attachments/assets/c95c79ca-ec5d-49de-b652-100555d3c950)\
predict.py最终生成结果

![image](https://github.com/user-attachments/assets/dd41df24-548d-4718-8089-efc6f67ceab6)\
以运行072706300103.png结果为例

### 五、实验总结
在本次基于YOLOv5的鸡热应激行为识别实验中，成功构建了图像采集系统，并利用该系统采集了肉鸡在不同状态下的图像数据。通过对图像数据的预处理和标注，可以得到一个包含啄食、饮水、热应激和其他行为类别的图像数据集。\
在模型搭建阶段，选择了PyTorch作为深度学习框架，并采用了YOLOv5模型进行对象检测。通过对标注好的json格式数据集进行训练，可以得到一个能够识别鸡只不同行为类别的模型。训练过程中，根据模型精度的要求，不断调整训练参数，并重复训练模型，直到获得了一个最优的epoch。\
在结果输出阶段，运行predict.py文件，对测试集中的图像进行了行为识别，并得到了相应的识别结果。
