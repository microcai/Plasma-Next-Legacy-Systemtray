cmake_minimum_required(VERSION 3.0)

project(plasma-systray C)

include(CheckCXXCompilerFlag)
check_cxx_compiler_flag(-std=c++11 HAS_CXX11)
if (HAS_CXX11)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 ")
endif()


set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -std=gnu11 ")


add_definitions(-DVERSION="0.1")

find_package(Threads)
find_package(Qt5Widgets REQUIRED)
find_package(Boost REQUIRED COMPONENTS regex thread system locale context coroutine)

link_libraries(X11 Xpm Xext Xfixes Xmu)

add_executable(plasma-systray fdtray.c  wmsystemtray.c)

target_link_libraries(plasma-systray ${CMAKE_THREAD_LIBS_INIT})

install(TARGETS plasma-systray RUNTIME DESTINATION bin)
