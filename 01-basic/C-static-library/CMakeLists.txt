cmake_minimum_required(VERSION 3.5)

project(hello_library)

############################################################
# Create a library
############################################################

#Generate the static library from the library sources
add_library(hello_library STATIC 
    src/Hello.cpp
)

target_include_directories(hello_library
    PUBLIC 
        ${PROJECT_SOURCE_DIR}/include
)

# 在 build 目录下，就可以看到我们编译出来的一个 .a 文件：
# qixian@qixiandeMBP ~/m/c/0/C/build (learn)> tree -L 1
# .
# ├── CMakeCache.txt
# ├── CMakeFiles
# ├── Makefile
# ├── cmake_install.cmake
# ├── hello_binary
# └── libhello_library.a

# 整体上还是很好理解的

############################################################
# Create an executable
############################################################

# Add an executable with the above sources
add_executable(hello_binary 
    src/main.cpp
)

# link the new hello_library target with the hello_binary target
target_link_libraries( hello_binary
    PRIVATE 
        hello_library
)
