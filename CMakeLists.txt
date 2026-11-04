cmake_minimum_required(VERSION 3.25)

project(UINCampus VERSION 1.0.0 LANGUAGES CXX)

add_library(options_projet INTERFACE)
target_compile_features(options_projet INTERFACE cxx_std_23)

if(MSVC)
    target_compile_options(options_projet INTERFACE /W4 /permissive-)
else()
    target_compile_options(options_projet INTERFACE
        -Wall -Wextra -Wpedantic -Wshadow -Wconversion
    )
endif()

add_library(uincampus src/version.cpp)

target_include_directories(uincampus PUBLIC include)

target_compile_definitions(uincampus PRIVATE
    UIN_VERSION="${PROJECT_VERSION}"
)

target_link_libraries(uincampus PRIVATE options_projet)

add_executable(uin-campus app/main.cpp)

target_link_libraries(uin-campus PRIVATE
    uincampus
    options_projet
)
