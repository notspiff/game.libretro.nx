project(gameclient.nx)

cmake_minimum_required(VERSION 2.6)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR})

enable_language(CXX)

find_package(xbmc REQUIRED)

include(ExternalProject)

externalproject_add(nx
                    GIT_REPOSITORY https://github.com/libretro/nxengine-libretro
                    GIT_TAG 4070c26
                    PREFIX nx
                    CONFIGURE_COMMAND ""
                    INSTALL_COMMAND ""
                    BUILD_COMMAND make
                    BUILD_IN_SOURCE 1)

set(NX_CUSTOM_BINARY ${PROJECT_BINARY_DIR}/nx/src/nx/nxengine_libretro${CMAKE_SHARED_LIBRARY_SUFFIX}
                     nxengine_libretro${CMAKE_SHARED_LIBRARY_SUFFIX} nx)

build_addon(gameclient.nx NX DEPLIBS)
add_dependencies(gameclient.nx nx)
