# 推理(部署)

## 常用框架

### 读前须知

后面的代码都是\_**Python**_的代码，但是实际上应用的话大多都是C++的代码_**，但是**\_C++的代码配置很麻烦这里不多介绍.很多人不理解人工智能到底是怎么进行使用的比如我搞智能车的时候，很多人认为，人工智能推动一切，其实并不是的，人工智能只做一个推理预测，有没有检测到东西，并不会推动一切，其他的都是通过代码推动的，自动化控制.部署的难度较大，这边只放了一些很简单的代码，具体的话需要查阅API文档去实现你自己需要的功能，这边只做一个参考

## Pytorch框架

pytorch框架用自己的模型进行推理,修改path路径和图片路径即可

```python
import torch

model = torch.hub.load('ultralytics/yolov5', 'custom', path='model.pt', device=0)  # local model
# Images
img = "image.jpg"  # or file, Path, PIL, OpenCV, numpy, list

# Inference
results = model(img)
results.show()#展示
results.save()#保存
```

### opencv读取图片

老样子替换图片路径和模型路径

```python
import torch
import cv2

model = torch.hub.load('ultralytics/yolov5', 'custom', path='model.pt', device=0)  # local model
img = cv2.imread('img.jpg')[..., ::-1]  # OpenCV image (BGR to RGB)
# Inference
results = model(img)
results.show()
```

## 飞浆框架

### fastdeploy

示例代码

```python
import cv2  #导入库
import fastdeploy 
import paddle
paddle.utils.run_check()
print(paddle.__version__) #输出版本用GPU推理
# 读取视频文件
video_path = "sample.mp4"
cap = cv2.VideoCapture(video_path)
option = fastdeploy.RuntimeOption()
option.use_gpu(device_id=0)
model = fastdeploy.vision.detection.PPYOLOE(
    "model.pdmodel", "model.pdiparams", "infer_cfg.yml", runtime_option=option)#配置文件读取
print(model.model_name())

# 逐帧进行推理
while cap.isOpened():
    ret, frame = cap.read()
    if not ret:
        break
    result = model.predict(frame)
    for i, value in enumerate(result.scores):
        if value > 0.9:
            if result.label_ids[i] == 0:
                print("减速带")
            if result.label_ids[i] == 1:
                print("粮仓识别")
            elif result.label_ids[i] == 2:
                print("斑马线识别")
            elif result.label_ids[i] == 3:
                print("锥桶识别")
            elif result.label_ids[i] == 4:
                print("桥")
            elif result.label_ids[i] == 5:
                print("猪")
            elif result.label_ids[i] == 6:
                print("拖拉机")
            elif result.label_ids[i] == 7:
                print("玉米")
    vis_im = vision.vis_detection(frame, result, score_threshold=0.5)
    cv2.imshow("frame", vis_im)

    key = cv2.waitKey(1)
    if key == 27:
        break

# 释放资源
cap.release()
cv2.destroyAllWindows()
```

### paddle lite

### Paddle Inference

### Paddle Serving

### Paddle.js

## onnxruntime

建议如果不是必须的情况下，建议不用onnxruntime进行推理，因为首先代码很难写，而且结果不一定是你想要的，花了一天没跑出来然而上面的fastdeploy读练好的模型配置就出了，如果用onnxruntime的话需要用\_**Netron**\_查看输入输出维度，去做对应的调整，建议准备读研的同学去研究一下，把文档补充完整

### yolov5转onnx推理

```python
'''
@Author: 刘施恩
@date:2023-11-22-22:22
@function: 用于pytorch转换onnx模型的推理预测返回四个框的位置置信度和类别,同时可以进行量化
'''
import os
import cv2
import numpy as np
import onnxruntime

CLASSES = ['E2', 'J20', 'B2', 'F14', 'Tornado', 'F4', 'B52', 'JAS39', 'Mirage2000']

class YOLOV5():
    def __init__(self,onnxpath):
        self.onnx_session=onnxruntime.InferenceSession(onnxpath)
        self.input_name=self.get_input_name()
        self.output_name=self.get_output_name()

    def get_input_name(self):
        input_name=[]
        for node in self.onnx_session.get_inputs():
            input_name.append(node.name)
        return input_name
    def get_output_name(self):
        output_name=[]
        for node in self.onnx_session.get_outputs():
            output_name.append(node.name)
        return output_name

    def get_input_feed(self,img_tensor):
        input_feed={}
        for name in self.input_name:
            input_feed[name]=img_tensor
        return input_feed

    def inference(self,img_path):
        img=cv2.imread(img_path)
        or_img=cv2.resize(img,(640,640))
        img=or_img[:,:,::-1].transpose(2,0,1)  
        img=img.astype(dtype=np.float16)
        img/=255.0
        img=np.expand_dims(img,axis=0)
        input_feed=self.get_input_feed(img)
        pred=self.onnx_session.run(None,input_feed)[0]
        return pred,or_img

def getx_c(width, xmin, xmax):
    x_c = (xmin + xmax) / 2;
    x_c = '%.16f' % (x_c / width)
    return x_c


def gety_c(height, ymin, ymax):
    y_c = (ymin + ymax) / 2
    y_c = '%.16f' % (y_c / height)
    return y_c


def getbbox_width(width, xmin, xmax):
    bbox_width = xmax - xmin
    bbox_width = '%.16f' % (bbox_width / width)
    return bbox_width


def getbbox_height(height, ymin, ymax):
    bbox_height = ymax - ymin
    bbox_height = '%.16f' % (bbox_height / height)
    return bbox_height

def nms(dets, thresh):
    x1 = dets[:, 0]
    y1 = dets[:, 1]
    x2 = dets[:, 2]
    y2 = dets[:, 3]

    areas = (y2 - y1 + 1) * (x2 - x1 + 1)
    scores = dets[:, 4]
    keep = []
    index = scores.argsort()[::-1] 

    while index.size > 0:
        i = index[0]
        keep.append(i)

        x11 = np.maximum(x1[i], x1[index[1:]]) 
        y11 = np.maximum(y1[i], y1[index[1:]])
        x22 = np.minimum(x2[i], x2[index[1:]])
        y22 = np.minimum(y2[i], y2[index[1:]])

        w = np.maximum(0, x22 - x11 + 1)                              
        h = np.maximum(0, y22 - y11 + 1) 

        overlaps = w * h

        ious = overlaps / (areas[i] + areas[index[1:]] - overlaps)
        idx = np.where(ious <= thresh)[0]
        index = index[idx + 1]
    return keep


def xywh2xyxy(x):

    y = np.copy(x)
    y[:, 0] = x[:, 0] - x[:, 2] / 2
    y[:, 1] = x[:, 1] - x[:, 3] / 2
    y[:, 2] = x[:, 0] + x[:, 2] / 2
    y[:, 3] = x[:, 1] + x[:, 3] / 2
    return y


def filter_box(org_box,conf_thres,iou_thres):

    org_box=np.squeeze(org_box)
    conf = org_box[..., 4] > conf_thres
    box = org_box[conf == True]

    cls_cinf = box[..., 5:]
    cls = []
    for i in range(len(cls_cinf)):
        cls.append(int(np.argmax(cls_cinf[i])))
    all_cls = list(set(cls))     

    output = []
    for i in range(len(all_cls)):
        curr_cls = all_cls[i]
        curr_cls_box = []
        curr_out_box = []
        for j in range(len(cls)):
            if cls[j] == curr_cls:
                box[j][5] = curr_cls
                curr_cls_box.append(box[j][:6])
        curr_cls_box = np.array(curr_cls_box)
        curr_cls_box = xywh2xyxy(curr_cls_box)
        curr_out_box = nms(curr_cls_box,iou_thres)
        for k in curr_out_box:
            output.append(curr_cls_box[k])
    output = np.array(output)
    return output

def get_result(image,box_data):
    boxes=box_data[...,:4].astype(np.int32) 
    scores=box_data[...,4]
    classes=box_data[...,5].astype(np.int32)
    res_list = []
    for box, score, cl in zip(boxes, scores, classes):
        top, left, right, bottom = box
        # print('class: {}, score: {}'.format(CLASSES[cl], score))
        # print('box coordinate left,top,right,down: [{}, {}, {}, {}]'.format(top, left, right, bottom))
        # 转化
        x_c = getx_c(650,top,right)
        y_c = gety_c(650,left,bottom)
        get_width = getbbox_width(650,top,right)
        get_height = getbbox_height(650,left,bottom)
        res_list.append([x_c,y_c,get_width,get_height,score,cl])
        # print('----------------------------------------')
        # print(x_c,y_c,get_width,get_height)
    return res_list

        # cv2.rectangle(image, (top, left), (right, bottom), (255, 0, 0), 2)
        # cv2.putText(image, '{0} {1:.2f}'.format(CLASSES[cl], score),
        #             (top, left ),
        #             cv2.FONT_HERSHEY_SIMPLEX,
        #             0.6, (0, 0, 255), 2)



if __name__=="__main__":
    onnx_path=r'last.onnx'
    model=YOLOV5(onnx_path)
    # 结果，转换的图片
    output,or_img=model.inference(r"main.jpg")
    outbox=filter_box(output,0.5,0.5)#返回框和置信度和类别
    res = get_result(or_img,outbox)
    print(res)
    # cv2.imwrite('res.jpg',or_img)
    
    


```

## 代码示例

## 1.1模型读取

### model\_config.hpp代码

```c++
#include <vector>
#include <fstream>
#include <iostream>
#include "json.hpp"
#include <opencv2/opencv.hpp>

using nlohmann::json;

struct ModelConfig
{
	std::string model_parent_dir;

	std::string network_type;

	std::string model_file;
	std::string model_params_dir;
	std::string params_file;

	std::string format;
	uint16_t input_width;
	uint16_t input_height;

	float means[3];
	float scales[3];
	float threshold;

	bool is_yolo;
	bool is_combined_model;

	std::vector<std::string> labels;

	void assert_check_file_exist(std::string fileName, std::string modelPath)
	{
		std::ifstream infile(modelPath + fileName);
		if (!infile.good())
		{
			printf("Error!!!! ModelConfig: File %s not exit, Please Check your model "
				"path:%s .\n",
				fileName.c_str(), modelPath.c_str());
			exit(-1);
		}
	}
	ModelConfig(std::string model_path) : model_parent_dir(model_path + "/")
	{

		std::string json_config_path = model_parent_dir + "config.json";
		std::ifstream is(json_config_path);
		if (!is.good())
		{
			std::cout << "Error:ModelConfig file path:[" << json_config_path
				<< "] not find ." << std::endl;
			exit(-1);
		}

		json value;
		is >> value;
		std::cout << "Config:" << value << std::endl;

		input_width = value["input_width"];
		input_height = value["input_height"];
		format = value["format"];
		std::transform(format.begin(), format.end(), format.begin(), ::toupper);

		std::vector<float> mean = value["mean"];
		for (int i = 0; i < mean.size(); ++i)
		{
			means[i] = mean[i];
		}

		std::vector<float> scale = value["scale"];
		for (int i = 0; i < scale.size(); ++i)
		{
			scales[i] = scale[i];
		}

		if (value["threshold"] != nullptr)
		{
			threshold = value["threshold"];
		}
		else
		{
			threshold = 0.5;
			std::cout << "Warnning !!!!,json key: threshold not found, default :"
				<< threshold << "\n";
		}

		is_yolo = false;
		if (value["network_type"] != nullptr)
		{
			network_type = value["network_type"];
			if (network_type == "YOLOV3")
			{
				is_yolo = true;
			}
		}

		if ((value["model_file_name"] != nullptr) &&
			(value["params_file_name"] != nullptr) &&
			(value["model_dir"] == nullptr))
		{
			is_combined_model = true;
			params_file =
				model_parent_dir + value["params_file_name"].get<std::string>();
			model_file =
				model_parent_dir + value["model_file_name"].get<std::string>();
			model_params_dir = "";
		}
		else if ((value["model_file_name"] == nullptr) &&
			(value["params_file_name"] == nullptr) &&
			(value["model_dir"] != nullptr))
		{
			is_combined_model = false;
			model_params_dir =
				model_parent_dir + value["model_dir"].get<std::string>();
			params_file = "";
			model_file = "";
		}
		else
		{
			std::cout
				<< "json config Error !!!! \n combined_model: need params_file_name "
				"model_file_name, separate_model: need model_dir only.\n";
			exit(-1);
		}

		if (value["labels_file_name"] != nullptr)
		{
			std::string labels_file_name = value["labels_file_name"];
			std::string label_path = model_parent_dir + labels_file_name;
			std::ifstream file(label_path);
			if (file.is_open())
			{
				std::string line;
				while (getline(file, line))
				{
					labels.push_back(line);
				}
				file.close();
			}
			else
			{
				std::cout << "Open Lable File failed, file path: " << label_path
					<< std::endl;
			}
		}

		if (is_combined_model)
		{
			assert_check_file_exist(value["model_file_name"], model_parent_dir);
			assert_check_file_exist(value["params_file_name"], model_parent_dir);
		}
		else
		{
			assert_check_file_exist(value["model_dir"], model_parent_dir);
		}

		std::cout << "Model Config Init Success !!!" << std::endl;
	}
	~ModelConfig() {}
};
```

json用的是[nlohmann](https://github.com/nlohmann/json)

使用示例，针对于\_**飞浆的模型**\_

```c++
#include<iostream>
#include"model_config.hpp"
using namespace std;
std::string model_file_path = "../../mobilenet-ssd";//模型路径



int main()
{
	ModelConfig modelConfig(model_file_path);
	std::string modelFile = modelConfig.model_file;
	std::string paramsDir = modelConfig.model_params_dir;
	std::vector<std::string> labels = modelConfig.labels;
	cout << modelFile << endl;
	for (auto i : labels) {
		cout << i << " ";
	}
}
```
