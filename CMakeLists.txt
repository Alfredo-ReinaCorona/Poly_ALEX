# cmake_minimum_required(VERSION 3.12)
# project(alex)

# set(CMAKE_CXX_STANDARD 14)

# # Define the macro ‘DEBUG' in the debug mode
# if(CMAKE_BUILD_TYPE STREQUAL Debug)        
#     ADD_DEFINITIONS(-DDEBUG)               
# endif()

# if(MSVC)
#     set(CMAKE_CXX_FLAGS "/O2 /arch:AVX2 /W1 /EHsc")
# elseif (CMAKE_CXX_COMPILER_ID STREQUAL "Intel")
#     set(CMAKE_CXX_FLAGS "-O3 -xHost")
# else()
#     # clang and gcc
#     set(CMAKE_CXX_FLAGS "-O3 -march=native -Wall -Wextra")
# endif()

# include_directories(src/core)

# add_executable(example src/examples/main.cpp)
# add_executable(benchmark src/benchmark/main.cpp)

# set(DOCTEST_DOWNLOAD_DIR ${CMAKE_CURRENT_BINARY_DIR}/doctest)
# file(DOWNLOAD
#     https://raw.githubusercontent.com/onqtam/doctest/2.4.6/doctest/doctest.h
#     ${DOCTEST_DOWNLOAD_DIR}/doctest.h
#     EXPECTED_HASH SHA1=40728d2bed7f074e80cb095844820114e7d16ce0
# )

# add_executable(test_alex test/unittest_main.cpp)
# target_include_directories(test_alex PRIVATE ${DOCTEST_DOWNLOAD_DIR})

# enable_testing()
# add_test(test_alex test_alex)

cmake_minimum_required(VERSION 3.12)
project(alex)

set(CMAKE_CXX_STANDARD 14)

# Define the macro ‘DEBUG' in debug mode
if(CMAKE_BUILD_TYPE STREQUAL Debug)
    add_definitions(-DDEBUG)
endif()

if(MSVC)
    set(CMAKE_CXX_FLAGS "/O2 /arch:AVX2 /W1 /EHsc")
elseif(CMAKE_CXX_COMPILER_ID STREQUAL "Intel")
    set(CMAKE_CXX_FLAGS "-O3 -xHost")
elseif(CMAKE_SYSTEM_PROCESSOR MATCHES "arm64" OR CMAKE_SYSTEM_PROCESSOR MATCHES "aarch64")
    # Apple Silicon or ARM64
    set(CMAKE_CXX_FLAGS "-O3 -Wall -Wextra")
else()
    # Default for clang/gcc on x86_64
    set(CMAKE_CXX_FLAGS "-O3 -march=native -Wall -Wextra")
endif()

include_directories(src/core)

add_executable(example src/examples/main.cpp)
add_executable(benchmark src/benchmark/main.cpp)

# tensorflow:
# set(TENSORFLOW_C_DIR "/Users/sanchit/Documents/ADS/Projects/Project 2/test/libtensorflow-cpu-darwin-arm64")
# include_directories(${TENSORFLOW_C_DIR}/include)
# link_directories(${TENSORFLOW_C_DIR}/lib)
# target_link_libraries(example ${TENSORFLOW_C_DIR}/lib/libtensorflow.dylib)

set(DOCTEST_DOWNLOAD_DIR ${CMAKE_CURRENT_BINARY_DIR}/doctest)
file(DOWNLOAD
    https://raw.githubusercontent.com/onqtam/doctest/2.4.6/doctest/doctest.h
    ${DOCTEST_DOWNLOAD_DIR}/doctest.h
    EXPECTED_HASH SHA1=40728d2bed7f074e80cb095844820114e7d16ce0
)

add_executable(test_alex test/unittest_main.cpp)
target_include_directories(test_alex PRIVATE ${DOCTEST_DOWNLOAD_DIR})

enable_testing()
add_test(test_alex test_alex)