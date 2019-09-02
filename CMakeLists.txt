cmake_minimum_required(VERSION 3.10)

project(maxminddb LANGUAGES C)

# execute_process(COMMAND ./bootstrap)
# execute_process(COMMAND ./configure)
# execute_process(COMMAND ./make)
# execute_process(COMMAND ./make check)
ADD_CUSTOM_COMMAND(
	OUTPUT bootstrap_out
	WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
	COMMAND ./bootstrap
	COMMAND ./configure
	COMMAND ./make
	COMMAND ./make check
	COMMENT "Building maxmind"
)
