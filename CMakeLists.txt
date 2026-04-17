cmake_minimum_required(VERSION 3.16)
project(my_ci_project)

set(CMAKE_CXX_STANDARD 14)

add_library(core add.cpp)

add_executable(app main.cpp)
target_link_libraries(app core)

include(FetchContent)

FetchContent_Declare(
  googletest
  URL https://github.com/google/googletest/archive/refs/heads/main.zip
)

set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)

FetchContent_MakeAvailable(googletest)

enable_testing()

add_executable(unit_tests test/test_add.cpp)
target_link_libraries(unit_tests gtest_main core)

include(GoogleTest)
gtest_discover_tests(unit_tests)