project(game.libretro.2048)

cmake_minimum_required(VERSION 2.6)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR})

enable_language(CXX)

find_package(Kodi REQUIRED)
find_package(libretro-2048 REQUIRED)

set(DEPLIBS 2048)
set(LIBRETRO_2048_CUSTOM_BINARY ${LIBRETRO_2048_LIB}
                                game.libretro.2048${CMAKE_SHARED_LIBRARY_SUFFIX} 2048)

build_addon(game.libretro.2048 LIBRETRO_2048 DEPLIBS)
