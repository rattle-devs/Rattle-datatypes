cmake_minimum_required(VERSION 3.21)

# set the project name
project(Rattle-data-types VERSION 0.1)

#config file
configure_file(config.h.in config.h)
include_directories(${PROJECT_BINARY_DIR})

# specify the C standard
set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_C_STANDARD 17)
set(CMAKE_C_EXTENSIONS OFF)
set(CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS} -std=c17 -Wall -Wall -Werror -Wshadow -Wdouble-promotion -Wformat -Wformat -Wformat-overflow -Wformat-truncation -Wundef -fno-common -Wconversion -ffunction-sections -Wpadded -g3")

add_subdirectory("Vector")
add_subdirectory("List")
add_subdirectory("Queue")
add_subdirectory("Stack")
message("sub")
add_library(data-types null.c)
target_link_libraries(data-types PUBLIC Vector)
target_link_libraries(data-types PUBLIC List)
target_link_libraries(data-types PUBLIC Queue)
target_link_libraries(data-types PUBLIC Stack)

IF(CMAKE_BUILD_TYPE MATCHES DEBUG)
    enable_testing()

    add_executable(VectorTest Tests/VectorTest.c)
    target_link_libraries(VectorTest PUBLIC Vector)

    add_executable(QueueTest Tests/QueueTest.c)
    target_link_libraries(QueueTest PUBLIC Queue)

    add_executable(StackTest Tests/StackTest.c)
    target_link_libraries(StackTest PUBLIC Stack)

    add_test(NAME Vector_Test_10_10 COMMAND VectorTest 10 10)
    add_test(NAME Vector_Test_50000000_10 COMMAND VectorTest 50000000 10)

    add_test(NAME Queue_Test_10_10 COMMAND QueueTest 10 10)
    add_test(NAME Queue_Test_50000000_10 COMMAND QueueTest 50000000 10)

    add_test(NAME Stack_Test_10_10 COMMAND StackTest 10 10)
    add_test(NAME Stack_Test_50000000_10 COMMAND StackTest 50000000 10)

ENDIF(CMAKE_BUILD_TYPE MATCHES DEBUG)
