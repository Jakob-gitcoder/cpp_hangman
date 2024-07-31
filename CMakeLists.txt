cmake_minimum_required(VERSION 3.5.0)
project(a-project VERSION 0.1.0 LANGUAGES C CXX)


if(CMAKE_SYSTEM_NAME MATCHES "Windows")
    include_directories(${CMAKE_CURRENT_SOURCE_DIR}/vendor/Raylib_4.5/Windows_64bit_mingw_w64_compiler/include/) 
elseif(CMAKE_SYSTEM_NAME MATCHES "Linux")
    include_directories(${CMAKE_CURRENT_SOURCE_DIR}/vendor/Raylib_4.5/Linux_64Bit_gcc_compiler/include/) 
    find_package(Threads REQUIRED)
endif()
#include_directories(${CMAKE_CURRENT_SOURCE_DIR}/vendor/Raylib_4.5/Linux_64Bit_gcc_compiler/include/)

add_executable(main main.cpp)

if(CMAKE_SYSTEM_NAME MATCHES "Windows")
    target_link_libraries(main ${CMAKE_CURRENT_SOURCE_DIR}/vendor/Raylib_4.5/Windows_64bit_mingw_w64_compiler/lib/libraylib.a)
    target_link_libraries(main winmm)
elseif(CMAKE_SYSTEM_NAME MATCHES "Linux")
    target_link_libraries(main ${CMAKE_CURRENT_SOURCE_DIR}/vendor/Raylib_4.5/Linux_64Bit_gcc_compiler/lib/libraylib.a)
    target_link_libraries(main Threads::Threads)
    target_link_libraries(main dl)
else()
    message("This operating system is not supported")
endif()



# For some reason this is needed for Linux
#if(UNIX AND NOT APPLE)
#    set(LINUX TRUE)
#endif()

#if (LINUX)
#    target_link_libraries(main ${CMAKE_CURRENT_SOURCE_DIR}/vendor/Raylib_4.5/Linux_64Bit_gcc_compiler/lib/libraylib.a)
#endif(LINUX)