# OpenCv

## C++版

### 1.1 读取摄像头并保存图片

文件名_**video.cpp**_

```cpp
#include <opencv2/opencv.hpp>
#include <iostream>

#ifdef _WIN32
#include <direct.h>
#else
#include <sys/stat.h>
#endif

using namespace std;
using namespace cv;

int main()
{
    // 创建一个目录用于保存图片
    string directory = "output/";

#ifdef _WIN32
    _mkdir(directory.c_str());
#else
    mkdir(directory.c_str(), 0777);
#endif

    // 读取摄像头图像并保存
    VideoCapture cap(0);
    Mat frame;
    int num = 5;
    while (num)
    {
        num--;
        cap >> frame;
        string name = directory + "frame" + to_string(num) + ".jpg";
        imwrite(name, frame);
        if (waitKey(30) >= 0)
            break;
    }
    cap.release();
    destroyAllWindows();

    return 0;
}

```

无论是在linux还是windows上面都可以用，_**注意**_，在linux上使用时需要使用cmake这里放一个参考

```cmake
cmake_minimum_required(VERSION 3.4...3.18)
project(intelligentCar)

set (CMAKE_CXX_STANDARD 17)

find_package( OpenCV REQUIRED )#导入opencv包
include_directories( ${OpenCV_INCLUDE_DIRS} )#寻找头文件

set(PROJECT_NAME "video")#设置项目名
set(INTELLIGENTCAR_CAR_PROJECT_SOURCES ${PROJECT_SOURCE_DIR}/video.cpp)#选择编译文件名
add_executable(${PROJECT_NAME} ${INTELLIGENTCAR_CAR_PROJECT_SOURCES})
target_link_libraries(${PROJECT_NAME} PRIVATE ${OpenCV_LIBS})#寻找lib链接库
```
