cmake_minimum_required(VERSION 3.10)

project(maxminddb LANGUAGES C)

execute_process(COMMAND "./bootstrap")
execute_process(COMMAND "./configure")
execute_process(COMMAND "./make")
execute_process(COMMAND "./make check")
