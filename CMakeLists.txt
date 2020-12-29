CMAKE_MINIMUM_REQUIRED(VERSION 3.6)
PROJECT(FileWatcher  LANGUAGES C CXX)

option(BUILD_DEMO_CPP "BUILD_DEMO_CPP, default off." OFF)


set(headers
	./FileWatcher.h
	./FileWatcherImpl.h
	./FileWatcherLinux.h
	./FileWatcherWin32.h
	./FileWatcherOSX.h
)

set(sources
	./source/FileWatcher.cpp
	./source/FileWatcherLinux.cpp
	./source/FileWatcherOSX.cpp
	./source/FileWatcherWin32.cpp
)

include_directories(${CMAKE_CURRENT_SOURCE_DIR})
add_library(FileWatcher  ${headers} ${sources})

if(BUILD_DEMO_CPP)
	add_executable(SimpleDemo ./source/demo/SimpleDemo.cpp)
	ADD_CUSTOM_COMMAND(TARGET SimpleDemo POST_BUILD
            COMMAND ${CMAKE_COMMAND}  -E make_directory ${CMAKE_CURRENT_BINARY_DIR}/test
            )
	TARGET_LINK_LIBRARIES(SimpleDemo FileWatcher)
endif()
