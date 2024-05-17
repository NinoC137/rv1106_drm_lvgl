cmake_minimum_required(VERSION 3.10)
project(lvgl)

set(CMAKE_C_STANDARD 99)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
add_compile_options(-fPIC -Wall -Wno-error -O2 -g)

include_directories(
    include
    include/libdrm
    lv_drm
    lv_drm/rlottie/inc
    generated
    custom
    generated/guider_customer_fonts
    generated/guider_fonts
    generated/images
    src
)

link_directories(${CMAKE_SOURCE_DIR}/lib)

option(ENABLE_LOTTIE_SUPPORT "Enable Lottie support" OFF)

if(ENABLE_LOTTIE_SUPPORT)
    add_subdirectory(rlottie)
endif()

add_subdirectory(lv_drm/lvgl)
add_subdirectory(lv_drm/lv_drivers)

add_definitions(-DUSE_DRM -DUSE_EVDEV)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DUSE_DRM -DUSE_EVDEV")
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -DUSE_DRM -DUSE_EVDEV")

target_include_directories(lvgl PUBLIC ${PROJECT_SOURCE_DIR} rlottie/inc/)

FILE(GLOB_RECURSE app_sources generated/*.c custom/*.c src/*.c)

add_executable(my_lvglApp ${app_sources})

target_compile_definitions(my_lvglApp PRIVATE LV_LVGL_H_INCLUDE_SIMPLE)

target_link_libraries(my_lvglApp
    lvgl
    lv_drivers
    lvgl::drivers
    # lvgl::examples
    # lvgl::demos
    drm
    m
    pthread
)

if(ENABLE_LOTTIE_SUPPORT)
    target_link_libraries(my_lvglApp rlottie::rlottie)
endif()

