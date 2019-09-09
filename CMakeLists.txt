cmake_minimum_required(VERSION 3.10)

project(maxminddb)

# Target in order to build the library using its Makefile.
add_custom_target(
	${PROJECT_NAME}_built
	WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
	COMMAND ./bootstrap
	COMMAND ./configure
	COMMAND make
	COMMAND make check
	COMMENT "Building maxmind"
)

if(BUILD_SHARED_LIBS)
	add_library(${PROJECT_NAME} SHARED IMPORTED GLOBAL)
	set(${PROJECT_NAME}_LIB_PATH ${CMAKE_CURRENT_SOURCE_DIR}/src/.libs/libmaxminddb.so)
else()
	add_library(${PROJECT_NAME} STATIC IMPORTED GLOBAL)
	set(${PROJECT_NAME}_LIB_PATH ${CMAKE_CURRENT_SOURCE_DIR}/src/.libs/libmaxminddb.a)
endif()

add_dependencies(${PROJECT_NAME} ${PROJECT_NAME}_built)

set_property(TARGET ${PROJECT_NAME}
	PROPERTY IMPORTED_LOCATION
		${${PROJECT_NAME}_LIB_PATH}
)

target_include_directories(${PROJECT_NAME}
	INTERFACE
		${CMAKE_CURRENT_SOURCE_DIR}/include
)

# Unused executable so cmake will generate library and custom target.
add_executable(run ${CMAKE_CURRENT_SOURCE_DIR}/main.cpp)
target_link_libraries(run ${PROJECT_NAME})
