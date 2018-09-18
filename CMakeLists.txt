cmake_minimum_required(VERSION 2.8.5)
project(Airstrike)

# Adhere to GNU filesystem layout conventions
include(GNUInstallDirs)

# Lowercase project name for binaries and packaging
string(TOLOWER ${PROJECT_NAME} PROJECT_NAME_LOWER)

# Additional CMake modules
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${PROJECT_SOURCE_DIR}/cmake)

# Version number in format X.YY.ZZ
set(VER_X  1)
set(VER_YY 00)
set(VER_ZZ 00)
set(VER_FULL "${VER_X}.${VER_YY}.${VER_ZZ}")

if(AROS)
    # AROS will provide the SDL dependency via makefile.
else()
    find_package(SDL 1.2 REQUIRED)
    find_package(SDL_image 1.2 REQUIRED)
    find_package(SDL_mixer 1.2 REQUIRED)
    find_package(PNG REQUIRED)
    find_package(JPEG REQUIRED)

    if(WARPOS)
        find_package(TIFF REQUIRED)
    endif()
endif()

set(
    SOURCES
    src/sprite_types/parachute.c
    src/sprite_types/bomb.c
    src/sprite_types/puff.c
    src/sprite_types/hangar.c
    src/sprite_types/dust.c
    src/sprite_types/message.c
    src/sprite_types/bonusmachine.c
    src/sprite_types/bullet.c
    src/sprite_types/bird.c
    src/sprite_types/airballoon.c
    src/sprite_types/biplane.c
    src/sprite_types/cloud.c
    src/sprite_types/bouncer.c
    src/sprite_types/energymeter.c
    src/sprite_types/blueplane.c
    src/sprite_types/smoke.c
    src/sprite_types/mark.c
    src/sprite_types/fire.c
    src/sprite_types/missile.c
    src/sprite_types/zeppelin.c
    src/sprite_types/cannon.c
    src/sprite_types/explosions.c
    src/support/maths.c
    src/support/names.c
    src/support/console.c
    src/support/text.c
    src/sprite/sprite.c
    src/sprite/sdlutils.c
    src/sprite/animation.c
    src/sprite/dirty.c
    src/sprite/global.c
    src/sprite/bitmask.c
    src/players.c
    src/sound.c
    src/level.c
    src/winds.c
    src/sprite_types.c
    src/config.c
    src/mech.c
    src/control.c
    src/airstrike.c
)

include_directories(
    ${SDL_INCLUDE_DIR}
    ${PROJECT_SOURCE_DIR}/src
    ${PROJECT_SOURCE_DIR}/src/sprite_types
    ${PROJECT_SOURCE_DIR}/src/support
    ${PROJECT_SOURCE_DIR}/src/sprite
)

# Linux/other UNIX get a lower-case binary name
set(TARGET_NAME ${PROJECT_NAME_LOWER})
add_executable(${TARGET_NAME} ${SOURCES} ${HEADERS})
if(MORPHOS OR AMIGAOS3 AND NOT WARPOS)
    target_link_libraries(${TARGET_NAME} ${SDL_LIBRARY} ${SDL_IMAGE_LIBRARY} ${PNG_LIBRARY} ${JPEG_LIBRARY} ${ZLIB_LIBRARY} -ldebug)
elseif(AROS)
    target_link_libraries(${TARGET_NAME} -lSDL)
else()
    if(WARPOS)
        target_link_libraries(${TARGET_NAME} ${SDL_LIBRARY} ${SDL_IMAGE_LIBRARY} ${PNG_LIBRARY} ${TIFF_LIBRARY} ${JPEG_LIBRARY} ${ZLIB_LIBRARY})
    else()
        target_link_libraries(${TARGET_NAME} ${SDL_LIBRARY} ${SDL_IMAGE_LIBRARY} ${PNG_LIBRARY} ${JPEG_LIBRARY} ${ZLIB_LIBRARY})
    endif()
endif()

set(INSTALL_DEST ${CMAKE_INSTALL_BINDIR})
install(TARGETS ${TARGET_NAME} DESTINATION ${INSTALL_DEST})


