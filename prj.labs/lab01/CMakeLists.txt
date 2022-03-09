cmake_minimum_required(VERSION 3.0.0)
project(lab01)

include(CTest)
enable_testing()

set (OpenCV_DIR "D:\\opencv\\build\\x64\\vc15\\lib") #change the path to match your complied
find_package( OpenCV REQUIRED )
include_directories( ${OpenCV_INCLUDE_DIRS} )

add_executable(lab01 lab01.cpp lab01.report.md.in.txt)

target_link_libraries( lab01 ${OpenCV_LIBS} )

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)


# prepare report md file
file(READ lab01.cpp cpp_source)
configure_file(lab01.report.md.in.txt ${CMAKE_CURRENT_BINARY_DIR}/lab01.report.md @ONLY)
add_custom_command(TARGET ${PROJECT_NAME}
  POST_BUILD COMMAND ${CMAKE_COMMAND} -E copy "${CMAKE_CURRENT_BINARY_DIR}/lab01.report.md" "$<TARGET_FILE_DIR:${PROJECT_NAME}>")