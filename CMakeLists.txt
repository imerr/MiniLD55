cmake_minimum_required(VERSION 2.8.4)
project(MiniLD55)

include_directories(${VENDOR_PATH}/include ${PROJECT_SOURCE_DIR}/Engine/src)
link_directories(${VENDOR_PATH}/lib)

include_directories(${VENDOR_PATH}/SFML/include)
include_directories(${VENDOR_PATH}/jsoncpp/include)
include_directories(${VENDOR_PATH}/box2d/Box2D)

set(JSONCPP_WITH_TESTS OFF CACHE BOOL "Dont want jsoncpp tests")
set(JSONCPP_WITH_POST_BUILD_UNITTEST OFF CACHE BOOL "Dont want jsoncpp unit tests to be run")
add_subdirectory(${VENDOR_PATH}/jsoncpp ${CMAKE_CURRENT_BINARY_DIR}/vendor/jsoncpp/)
set(BOX2D_BUILD_EXAMPLES OFF CACHE BOOL "Dont want box2d examples")
set(BOX2D_BUILD_STATIC ON CACHE BOOL "Build box2d as static lib")
add_subdirectory(${VENDOR_PATH}/box2d/Box2D ${CMAKE_CURRENT_BINARY_DIR}/vendor/box2d/)
add_subdirectory(${VENDOR_PATH}/SFML ${CMAKE_CURRENT_BINARY_DIR}/vendor/sfml/)
add_subdirectory(Engine ${CMAKE_CURRENT_BINARY_DIR}/engine/)

include_directories(.)

set(SOURCE_FILES main.cpp
                 MiniLD55.cpp
)
add_executable(MiniLD55 ${SOURCE_FILES})

target_link_libraries(MiniLD55 jsoncpp_lib
							   Box2D
                               sfml-window
                               sfml-audio
                               sfml-system
                               sfml-graphics
                               sfml-main
							   SFMLEngine)
