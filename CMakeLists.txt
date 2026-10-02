cmake_minimum_required(VERSION 3.20)
project(Nebula C)

if(CMAKE_CROSSCOMPILING)
    add_library(stub STATIC tests/target/stub.c)
else()
    add_executable(hello tests/host/hello.c)
endif()

find_program(CPPCHECK_EXE cppcheck)
if(CPPCHECK_EXE)
    add_custom_target(cppcheck
        COMMAND ${CPPCHECK_EXE}
                --enable=warning,style,performance,portability
                --std=c11
                --language=c
                --inline-suppr
                --error-exitcode=1
                tests
        WORKING_DIRECTORY ${CMAKE_SOURCE_DIR}
        COMMENT "Running cppcheck on the C sources"
        VERBATIM)
else()
    message(STATUS "cppcheck not found: the 'cppcheck' target is unavailable")
endif()