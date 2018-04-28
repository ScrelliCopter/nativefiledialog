cmake_minimum_required(VERSION 3.10)
project(nfd)

set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 11)

include_directories(src)
include_directories(src/include)

set(SOURCE
		src/include/nfd.h
		src/common.h
		src/nfd_common.h
		src/nfd_common.c)

if (WIN32)
	set(SOURCE ${SOURCE} src/nfd_win.cpp)
elseif (APPLE)
	set(SOURCE ${SOURCE} src/nfd_cocoa.m)
else ()
	set(SOURCE ${SOURCE} src/nfd_gtk.c)
endif()

add_library(nfd ${SOURCE})

project(test_opendialog)
add_executable(test_opendialog src/include/nfd.h test/test_opendialog.c)
target_link_libraries(test_opendialog nfd)

project(test_opendialogmultiple)
add_executable(test_opendialogmultiple src/include/nfd.h test/test_opendialogmultiple.c)
target_link_libraries(test_opendialogmultiple nfd)

project(test_pickfolder)
add_executable(test_pickfolder src/include/nfd.h test/test_pickfolder.c)
target_link_libraries(test_pickfolder nfd)

project(test_savedialog)
add_executable(test_savedialog src/include/nfd.h test/test_savedialog.c)
target_link_libraries(test_savedialog nfd)
