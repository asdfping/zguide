cmake_minimum_required(VERSION 3.5)
project(zmq_example)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_FLAGS "-O0 -ggdb")

set(MAJ_PATTERN_CLI_SRC  mdcliapi.c mdclient.c)
set(MAJ_PATTERN_WRK_SRC mdworker.c mdwrkapi.c)
set(MAJ_PATTERN_BRK_SRC mdbroker.c)



find_library (ZMQ_LIB_STATIC
        NAMES libzmq.a
        REQUIRED)
message("zmq library static:" ${ZMQ_LIB_STATIC})

add_executable(mdc_cli ${MAJ_PATTERN_CLI_SRC})
add_executable(mdc_wrk ${MAJ_PATTERN_WRK_SRC})
add_executable(mdc_brk ${MAJ_PATTERN_BRK_SRC})

target_link_libraries(mdc_cli ${ZMQ_LIB_STATIC} pgm sodium rt pthread)
target_link_libraries(mdc_wrk ${ZMQ_LIB_STATIC} pgm sodium rt pthread)
target_link_libraries(mdc_brk ${ZMQ_LIB_STATIC} pgm sodium rt pthread)