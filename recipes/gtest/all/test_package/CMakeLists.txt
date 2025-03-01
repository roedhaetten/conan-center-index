cmake_minimum_required(VERSION 3.15)
project(test_package CXX)

find_package(GTest REQUIRED)

if(WITH_MAIN)
    add_executable(${PROJECT_NAME} test_package.cpp)
else()
    add_executable(${PROJECT_NAME} main.cpp test_package.cpp)
endif()

if(WITH_MAIN)
    target_link_libraries(${PROJECT_NAME} GTest::gtest GTest::gtest_main)
    if(WITH_GMOCK)
        target_link_libraries(${PROJECT_NAME} GTest::gmock GTest::gmock_main)
    endif()
else()
    target_link_libraries(${PROJECT_NAME} GTest::gtest)
    if(WITH_GMOCK)
        target_link_libraries(${PROJECT_NAME} GTest::gmock)
    endif()
endif()

set_property(TARGET ${PROJECT_NAME} PROPERTY CXX_STANDARD 11)
