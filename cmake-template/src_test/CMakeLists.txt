
find_package(GTest REQUIRED)

set(PROJECT_TEST_NAME "${PROJECT_NAME_STR}_test")
include_directories(${GTEST_INCLUDE_DIRS} ${COMMON_INCLUDES})
LINK_DIRECTORIES( /usr/lib /usr/lib64 ${GTEST_LIBRARY} ${LIBRARY_OUTPUT_PATH})

add_executable(${PROJECT_TEST_NAME} "example_test.cxx")
target_link_libraries(${PROJECT_TEST_NAME} ${PROJECT_NAME_STR} cmake_example gtest gtest_main pthread)

install (TARGETS ${PROJECT_TEST_NAME} DESTINATION ${PROJECT_TEST_NAME})

add_test(${PROJECT_TEST_NAME} ${PROJECT_TEST_NAME})
