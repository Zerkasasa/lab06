cmake_minimum_required(VERSION 3.22.1)

project(formatter_ex)

set(CMAKE_CXX_STANDART 20)
set(CMAKE_CXX_STANDART_REQUIRED ON)
set(CMAKE_CURRENT_SOURCE_DIR /home/vboxuser/Zerkasasa/workspace/projects/lab06/formatter_ex_lib)

add_library(formatter_ex STATIC formatter_ex.cpp)

add_subdirectory("../formatter_lib" formatter)

target_link_libraries(formatter_ex PUBLIC formatter)
target_include_directories(formatter_ex PUBLIC
				"../formatter_ex_lib"
				"../formatter_lib")

target_include_directories(formatter_ex PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}) 

