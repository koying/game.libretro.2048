project(game.libretro.2048)

cmake_minimum_required(VERSION 2.6)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR})

enable_language(CXX)

find_package(kodi REQUIRED)

include(ExternalProject)

if(CMAKE_BUILD_TYPE MATCHES Debug)
  set(LIBRETRO_DEBUG DEBUG=1)
endif()

if("${CORE_SYSTEM_NAME}" STREQUAL "windows")
  set(BUILD_COMMAND mingw32-make -f Makefile.libretro platform=win ${LIBRETRO_DEBUG})
elseif("${CORE_SYSTEM_NAME}" STREQUAL "linux")
  set(BUILD_COMMAND make -f Makefile.libretro ${LIBRETRO_DEBUG})
elseif("${CORE_SYSTEM_NAME}" STREQUAL "darwin")
  set(BUILD_COMMAND make -f Makefile.libretro platform=osx ${LIBRETRO_DEBUG})
elseif("${CORE_SYSTEM_NAME}" STREQUAL "ios")
  # TODO
elseif("${CORE_SYSTEM_NAME}" STREQUAL "android")
  # TODO
elseif("${CORE_SYSTEM_NAME}" STREQUAL "rbpi")
  # TODO
elseif("${CORE_SYSTEM_NAME}" STREQUAL "freebsd")
# TODO
endif()

externalproject_add(2048
                    GIT_REPOSITORY https://github.com/libretro/libretro-2048
                    GIT_TAG 5adbbc5
                    PREFIX 2048
                    CONFIGURE_COMMAND ""
                    INSTALL_COMMAND ""
                    BUILD_COMMAND ${BUILD_COMMAND}
                    BUILD_IN_SOURCE 1)

set(2048_CUSTOM_BINARY ${PROJECT_BINARY_DIR}/2048/src/2048/2048_libretro${CMAKE_SHARED_LIBRARY_SUFFIX}
                       game.libretro.2048${CMAKE_SHARED_LIBRARY_SUFFIX} 2048)

build_addon(game.libretro.2048 2048 DEPLIBS)
add_dependencies(game.libretro.2048 2048)

include(CPack)
