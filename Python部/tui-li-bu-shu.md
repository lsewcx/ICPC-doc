# 推理(部署)

## 常用框架

### 读前须知

后面的代码都是\_**Python**_的代码，但是实际上应用的话大多都是C++的代码_**，但是**\_C++的代码配置很麻烦这里不多介绍.很多人不理解人工智能到底是怎么进行使用的比如我搞智能车的时候，很多人认为，人工智能推动一切，其实并不是的，人工智能只做一个推理预测，有没有检测到东西，并不会推动一切，其他的都是通过代码推动的，自动化控制.部署的难度较大，这边只放了一些很简单的代码，具体的话需要查阅API文档去实现你自己需要的功能，这边只做一个参考

## Pytorch框架

pytorch框架用自己的模型进行推理

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
