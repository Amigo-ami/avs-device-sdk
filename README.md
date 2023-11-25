### What is the Alexa Voice Service (AVS)?

The Alexa Voice Service (AVS) enables developers to integrate Alexa directly into their products, bringing the convenience of voice control to any connected device. AVS provides developers with access to a suite of resources to build Alexa-enabled products, including APIs, hardware development kits, software development kits, and documentation.

[Learn more »](https://developer.amazon.com/alexa-voice-service)

### What is the AVS Device SDK

The Alexa Voice Service (AVS) Device SDK provides you with a set of C ++ libraries to build an Alexa Built-in product, meaning your device has direct access to cloud-based Alexa capabilities to receive voice responses instantly. You can create a wide range of devices — a smartwatch, speaker, headphones, smart TV, set-top boxes, soundbar, AV receiver, home theater hub, or a gaming console — the choice is yours.

[Learn more »](https://developer.amazon.com/docs/alexa/avs-device-sdk/overview.html)

### Release Notes and Known Issues

Feature enhancements, updates, and resolved issues from all releases are available on the [Amazon developer portal](https://developer.amazon.com/docs/alexa/avs-device-sdk/release-notes.html).

### Get Started

You can [set up the SDK](https://developer.amazon.com/en-US/docs/alexa/avs-device-sdk/quick-start-guides.html) on the following platforms:
* Ubuntu Linux
* Raspberry Pi
* macOS

### SDK Architecture

The SDK is modular and abstract. It provides [separate components](https://developer.amazon.com/docs/alexa/avs-device-sdk/overview.html#sdk-architecture) to handle necessary Alexa functionality including processing audio, maintaining persistent connections, and managing Alexa interactions. Each component exposes [Alexa APIs](https://developer.amazon.com/docs/alexa/alexa-voice-service/api-overview.html) to customize your device integrations as needed. The SDK also includes a Sample App, so you can  test interactions before integration.

[Learn more »](https://developer.amazon.com/docs/alexa/avs-device-sdk/overview.html#sdk-architecture)

### API References

View the [C++ API References](https://alexa.github.io/avs-device-sdk/) for detailed information about implementation.

### Security Requirements

All Alexa products must meet the [AVS Security Requirements](https://developer.amazon.com/en-US/docs/alexa/alexa-voice-service/avs-security-reqs.html). In addition, when building the AVS Device SDK, you are required to adhere to the [following security principles](https://developer.amazon.com/en-US/docs/alexa/avs-device-sdk/overview.html#security-requirements).
   
### 关于分支Kitty_AI nihap
分支Kitty-AI 在上面V3.00.0版本的SDK上面，参照V1.18.0版本SDK重新增加了对Kitty-AI 和 Sensory 第三方语言模型的支持，实现了关键词唤醒功能
### 编译说明： 
因为 cmakeBuild/cmake/KeywordDetector.cmake 增加了Kitty-AI 和 Sensory的模型支持，因此如果想要编译支持keywordDetectory可以增加下面构造参数构造cmake结构
cmake /home/alexa/sdk-folder/sdk-source/avs-device-sdk/ \      // 使用cmake命令从源码中读取CmakeLists.txt 安装CmakeLists.txt 中的规则构造cmake 编译框架
-DGSTREAMER_MEIDA_PLAY=ON \     //构造参数宏， cmake文件根据参数宏 开启/关闭相应功能模块，这里开启Gstream 模块
-DPKDCS11=OFF \                 // 
-DKITTAI_KEY_WORD_DETECTOR=ON \   // 使能Kitty-AI 模块
-DKITTAI_KEY_WORD_DETECTOR_LIB_PATH=/home/alexa/sdk-folder/libkwd/lib/libsnowboy-detect.a \  //设置Kitt-AI算法库文件地址// 
-DKITTAI_KEY_WORD_DETECTOR_INCLUDE_DIR=/home/alexa/skd-folder/libkwd/include \  //设置Kitt-AI库头文件地址  
-DPATHTOINPUT_MODE_DIR=/home/alexa/sdk-folder/inputs \   // 设置Kitt-AI 输入模型文件的地址，该输入模型地址在V1.18.0的版本由应用输入接口传递给关键词检测模型算法，现在改为在编译时直接传入输入模型地址
-DPORTAUDIO_LIB_PATH=/usr/lib/x86_64-linux-gnu/libportaudio.so \  //设置libportaudio.so 库地址
-DPORTAUDIO_INCLUDE_DIR=/usr/include \   // 设置portaudio的头文件地址
-DCMAKE_BUILD_TYPE=DEBUG // 调试模式

### 关于Kitty-AI 一些文件的获取
1. 首先可以使用git clone --single-branch https:github.com/Kitt-AI/snowboy.git 拉取整个snowboy 工程(关于snowboy整个项目的编译与使用，可以去snowboy项目查看， 这里只做Kitt-AI移植所需文件获取的说明）
2. 关于libsnoyboy-detector.a 文件的获取， 该文件在snowboy/lib/平台/libsonwboy-detect.a 文件夹内，该文件夹内有不同平台支持的库文件，选择相应平台的库文件即可
3. Kitt-AI头文件位置 snowboy/include/snowboy.detect.h
4. 输入模型分为两个，一个参数设置模型包含语言选择及其它参数设置的common.res文件和关键词模型.umdl文件，这两个文件的位置如下
5. common.res snowboy/resource/common.res
6. .umdl 以常用的alexa关键词为例 snowboy/resource/alexa/alexa_02092019.umdl, 还有其它的关键词模型在文件夹 snowboy/resource/models 中
