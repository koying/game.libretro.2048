cmake_minimum_required(VERSION 3.1)
project(game.libretro.2048)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR})

find_package(Kodi REQUIRED)
find_package(libretro-2048 REQUIRED)

set(DEPLIBS 2048)
set(LIBRETRO_2048_CUSTOM_BINARY ${LIBRETRO_2048_LIB}
                                ${PROJECT_NAME}${CMAKE_SHARED_LIBRARY_SUFFIX})

build_addon(${PROJECT_NAME} LIBRETRO_2048 DEPLIBS)
