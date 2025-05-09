Eu consegui criar uma estrutura básica para montagem de um projeto C++

A estrutura segue o seguinte padrão:
![[diagrama_arvore_arquivos_cmake.png | center]]
Note que o nó raiz possui um CMakeLists.txt que define as características principais do projeto através de:
```c
cmake_minimum_required(VERSION 3.10)

project(MyProject)

set(CMAKE_CXX_STANDARD 17)
add_subdirectory(source)
```
Dentro de source preciso tenho o seguinte cmake
```c
add_subdirectory(lib)
add_subdirectory(math)

add_executable(Main main.cpp)
target_link_libraries(Main PRIVATE gabriel_utils_lib)
target_include_directories(Main PRIVATE lib)

target_link_libraries(Main PRIVATE gabriel_utils_math)
target_include_directories(Main PRIVATE math)
```
em source/lib/CMakeLists.txt
```c
add_library(gabriel_utils_lib STATIC
    print_vector.cpp
)

target_include_directories(gabriel_utils_lib PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
```
em source/math/CMakeLists.txt
```c
add_library(
    gabriel_utils_math
    STATIC
    my_sqrt.cpp
)

target_include_directories(gabriel_utils_math PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
```