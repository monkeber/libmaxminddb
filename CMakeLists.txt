cmake_minimum_required(VERSION 3.10)

project(maxminddb)
message(${CMAKE_CURRENT_BINARY_DIR})
message(${CMAKE_CURRENT_SOURCE_DIR})
ADD_CUSTOM_target(
	maxminddb
	WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
	COMMAND ./bootstrap
	COMMAND ./configure
	COMMAND make
	COMMAND make check
	COMMENT "Building maxmind"
)
add_executable(run main.cpp)
add_dependencies(run maxminddb)
