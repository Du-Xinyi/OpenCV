#指定cmake最低版本 
cmake_minimum_required(VERSION 3.2)

#指定项目的名称
PROJECT(run)

#支持C++11
SET(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -std=gnu++0x")
SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=gnu++0x")

#查找依赖包
set(CMAKE_PREFIX_PATH /opt/intel/openvino_2021/deployment_tools/inference_engine/share)
find_package(OpenCV)
find_package(InferenceEngine)

if(${OpenCV_FOUND})
	INCLUDE_DIRECTORIES(${OpenCV_INCLUDE_DIRS})
endif(${OpenCV_FOUND})

if(${InferenceEngine_FOUND})
	INCLUDE_DIRECTORIES(${InferenceEngine_INCLUDE_DIRS})
endif(${InferenceEngine_FOUND})

#头文件目录
INCLUDE_DIRECTORIES(Headers)

#源文件目录
AUX_SOURCE_DIRECTORY(Sources DIR_SRCS)

#设置环境变量
SET(PATH ${DIR_SRCS})

#添加要编译的可执行文件
ADD_EXECUTABLE(${PROJECT_NAME} ${PATH})

#添加可执行文件所需要的库
TARGET_LINK_LIBRARIES(${PROJECT_NAME} ${OpenCV_LIBS} ${InferenceEngine_LIBS})

