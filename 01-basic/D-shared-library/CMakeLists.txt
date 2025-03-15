cmake_minimum_required(VERSION 3.5)

project(hello_library)

############################################################
# Create a library
############################################################

#Generate the shared library from the library sources
# 注意中间的 SHARED
add_library(hello_library SHARED 
    src/Hello.cpp
)
# 这里是新增了两个 lib 吗？hello_library 和 hello::library?
# 这里是为 hello_library 这个 lib 起了一个别名，后续 link 到 hello_library 的时候
# 就可以使用 hello::library ，通过中间的 ALIAS 来指定的
add_library(hello::library ALIAS hello_library)

target_include_directories(hello_library
    PUBLIC 
        ${PROJECT_SOURCE_DIR}/include
)

############################################################
# Create an executable
############################################################

# Add an executable with the above sources
add_executable(hello_binary
    src/main.cpp
)

# link the new hello_library target with the hello_binary target
# 从这里看，似乎前面的 add_library 本质上只增加了一个 lib
target_link_libraries(hello_binary
    PRIVATE 
        hello::library
)
