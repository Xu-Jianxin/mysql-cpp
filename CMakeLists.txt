cmake_minimum_required(VERSION 2.8)

###################################################################################
project(mysql_cpp)

if (CMAKE_BUILD_TYPE)
else()
    #set(CMAKE_BUILD_TYPE RELEASE)
    set(CMAKE_BUILD_TYPE DEBUG)
endif()

message("------------ Options -------------")
message("  CMAKE_BUILD_TYPE: ${CMAKE_BUILD_TYPE}")
message("  CMAKE_COMMAND: ${CMAKE_COMMAND}")
message("-------------- Env ---------------")
message("  CMAKE_SOURCE_DIR: ${CMAKE_SOURCE_DIR}")
message("  CMAKE_BINARY_DIR: ${CMAKE_BINARY_DIR}")
message("----------------------------------")

if (UNIX)
    set(CMAKE_CXX_FLAGS "-std=c++11 -fPIC -Wall -m64 ${CMAKE_CXX_FLAGS}")
    set(CMAKE_CXX_FLAGS_DEBUG "-g ${CMAKE_CXX_FLAGS}")
    set(CMAKE_CXX_FLAGS_RELEASE "-g -O3 ${CMAKE_CXX_FLAGS}")
elseif (WIN32)
    # windows platform
    add_definitions(-D_CRT_SECURE_NO_WARNINGS)
    set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} /MDd")
    set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} /MD")
    # set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} /MTd /EHsc")
    # set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} /MT /EHsc")
endif()

# mysql library
set(MYSQL "D:/mysql")
set(MYSQL_INCLUDE ${MYSQL}/include)
set(MYSQL_LIB ${MYSQL}/lib)

# boost
set(BOOST "F:/demos/libgonet/boost_1_78_0")

include_directories(${MYSQL_INCLUDE} ${BOOST})
link_directories(${MYSQL_LIB})

link_libraries(mysqlclient)

file(GLOB SRC_LIST *.cpp *.h *.hpp)
#aux_source_directory(${PROJECT_SOURCE_DIR} SRC_LIST)

add_executable(mysql_cpp ${SRC_LIST})