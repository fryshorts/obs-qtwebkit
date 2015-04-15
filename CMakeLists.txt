cmake_minimum_required(VERSION 2.8.12)

project(obs-qtwebkit)

set(CMAKE_INCLUDE_CURRENT_DIR TRUE)
set(CMAKE_AUTOMOC TRUE)

find_package(LibObs REQUIRED)
find_package(Qt5Widgets REQUIRED)
find_package(Qt5WebKit REQUIRED)
find_package(Qt5WebKitWidgets REQUIRED)
find_package(Qt5Network REQUIRED)

if(NOT MSVC)
	set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=gnu++11")
endif()

set(obs-qtwebkit_SOURCES
	src/qtwebkit-main.cpp
	src/qtwebkit-manager.cpp
	src/qtwebkit-renderer.cpp
	src/qtwebkit-source.cpp)

set(obs-qtwebkit_HEADERS
	src/qtwebkit-manager.hpp
	src/qtwebkit-source.hpp)

add_library(obs-qtwebkit MODULE
	${obs-qtwebkit_SOURCES}
	${obs-qtwebkit_HEADERS})

target_link_libraries(obs-qtwebkit
	libobs
	Qt5::Widgets
	Qt5::WebKit
	Qt5::WebKitWidgets
	Qt5::Network)

set_target_properties(obs-qtwebkit
	PROPERTIES
	PREFIX "")

install(TARGETS obs-qtwebkit
	LIBRARY DESTINATION "${LIBOBS_PLUGIN_DESTINATION}"
	RUNTIME DESTINATION "${LIBOBS_PLUGIN_DESTINATION}")
