cmake_minimum_required(VERSION 3.20)
project(Nebula C)

if(CMAKE_CROSSCOMPILING)
    add_library(stub STATIC tests/target/stub.c)
else()
    add_executable(hello tests/host/hello.c)
endif()