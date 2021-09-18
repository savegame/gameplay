cmake_minimum_required(VERSION 2.8)

project(GamePlay)

set(GAMEPLAY_VERSION 3.0.0)
set(CMAKE_C_COMPILER_INIT g++)

# debug
message( "CMAKE_BUILD_TYPE: ${CMAKE_BUILD_TYPE}" )
if ( "${CMAKE_BUILD_TYPE}" STREQUAL "DEBUG" )
    add_definitions(-D_DEBUG)
endif()

# architecture
if ( CMAKE_SIZEOF_VOID_P EQUAL 8 )
set(ARCH_DIR "x64")
else()
set(ARCH_DIR "x86")
endif()

#additional include diretories
find_package(PkgConfig REQUIRED)

pkg_check_modules(OPENAL REQUIRED openal)

pkg_check_modules(BULLET REQUIRED bullet)
include_directories(${BULLET_INCLUDE_DIRS})

pkg_check_modules(OGG REQUIRED ogg)
include_directories(${OGG_INCLUDE_DIRS})

pkg_check_modules(VORBIS REQUIRED vorbis)
include_directories(${VORBIS_INCLUDE_DIRS})

# pkg_check_modules(VORBIS REQUIRED vorbisenc)

pkg_check_modules(VORBISFILE REQUIRED vorbisfile)
include_directories(${VORBISFILE_INCLUDE_DIRS})

# luacompat 
include_directories(libs/luacompat)

pkg_check_modules(LUAJIT REQUIRED luajit)
include_directories(${LUAJIT_INCLUDE_DIRS})

# gameplay library
add_subdirectory(gameplay)

# gameplay samples
add_subdirectory(samples)

# gameplay encoder
# A pre-compiled executable can be found in 'gameplay/bin'. Uncomment to build yourself.
#add_subdirectory(tools/encoder)
#add_subdirectory(tools/luagen)
