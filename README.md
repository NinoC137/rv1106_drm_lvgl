# RV1106 DRM LVGL Project

使用交叉编译, 为ubuntu22.04系统的rv1106编译lvgl工程, 使用drm驱动    
已通过测试验证

效果为: 展示一张图片, 点击后图片消失 -- 2024.6.1

## 使用方法 -- GUI-GUIDER

生成好工程代码之后, 仅需将其中的custom和generated文件夹覆盖到此工程之中即可

## 编译环境切换 BuildRoot/ubuntu

如果目标板上运行的是ubuntu系统, 则无需切换

如果目标板上运行的是buildroot系统, 则打开Makefile, 将其中的TOOLCHAIN_FILE改为本工程文件夹cmake之中的另一个

## 备注: 关于工程文件丢失问题

在lv_drm文件夹下, lv_driver & lvgl & rlottie都需要去到对应的github仓库下载下来代码, 填充进去, rlottie需要额外初始化

如果不需要rlottie的话, 修改cmake & makefile文件, 删去rlottie部分即可


**建议参考的工程链接: https://github.com/wei-ruitong/tspi_lvgl**
