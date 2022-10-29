cmake_minimum_required(VERSION 3.20)
project(gameengine)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/")

set(CMAKE_CXX_STANDARD 17)

option(COLLIDER_DEBUG "Collision debug option" OFF)

if(COLLIDER_DEBUG)
    add_definitions(-DENABLE_COLLIDER_DEBUG)
endif()

find_package(SDL2 REQUIRED)
include_directories(${SDL2_INCLUDE_DIRS})

find_package(SDL2_image REQUIRED)
include_directories(${SDL2_IMAGE_INCLUDE_DIRS})

find_package(SDL2_ttf REQUIRED)
include_directories(${SDL2_TTF_INCLUDE_DIRS})

find_package(SDL2_mixer REQUIRED)
include_directories(${SDL2_MIXER_INCLUDE_DIRS})

find_package(Lua REQUIRED)
include_directories(${LUA_INCLUDE_DIR})

file(GLOB_RECURSE MAIN "src/Main.cpp")
file(GLOB_RECURSE GAME "src/Game/*")
file(GLOB_RECURSE LOGGER "src/Logger/*")
file(GLOB_RECURSE ECS "src/ECS/*")
file(GLOB_RECURSE ASSET_STORE "src/AssetManager/*")

set(SOURCES ${MAIN} ${GAME} ${LOGGER} ${ECS} ${ASSET_STORE})

add_executable(${PROJECT_NAME} ${SOURCES})
target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/libs)
target_link_libraries(${PROJECT_NAME}
        ${SDL2_LIBRARIES}
        ${SDL2_IMAGE_LIBRARIES}
        ${SDL2_TTF_LIBRARIES}
        ${SDL2_MIXER_LIBRARIES}
        ${LUA_LIBRARIES}
        )