# RV1106 DRM LVGL Project

使用交叉编译, 为ubuntu22.04系统的rv1106编译lvgl工程, 使用drm驱动
已通过测试验证

## 使用方法 -- GUI-GUIDER

生成好工程代码之后, 仅需将其中的custom和generated文件夹覆盖到此工程之中即可

## 编译环境切换 BuildRoot/ubuntu

如果目标板上运行的是ubuntu系统, 则无需切换

如果目标板上运行的是buildroot系统, 则打开Makefile, 将其中的TOOLCHAIN_FILE改为本工程文件夹cmake之中的另一个
