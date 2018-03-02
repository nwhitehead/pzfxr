cmake_minimum_required(VERSION 3.1)


### VERSIONING

project(pzfxr)

set(PZFXR_VERSION_MAJOR 1)
set(PZFXR_VERSION_MINOR 0)
set(PZFXR_VERSION_PATCH 0)

option(USE_SANITIZER "Build with address sanitizer checks" OFF)

# Turn on C++11
set(CMAKE_CXX_STANDARD 11)

if (USE_SANITIZER)
    # Turn on address sanitizer
    set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O2 -fsanitize=address -fno-omit-frame-pointer")
endif()


### EXTERNAL PROJECTS

# External libraries location
set(EXTERNAL ${PROJECT_SOURCE_DIR}/external)


### MAIN

# Include directories
include_directories(${EXTERNAL})

# Main executable target
add_executable(pzfxr
    src/pzfxr.cc
    src/Generator.cc
    src/RNG.cc
)

# Installation locations
install(TARGETS pzfxr
    RUNTIME DESTINATION bin
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib)


### PACKAGING

# All platforms get ZIP file
set (CPACK_GENERATOR ZIP)
#set (CPACK_PACKAGE_DESCRIPTION_FILE "${PROJECT_SOURCE_DIR}/DESCRIPTION")
set (CPACK_PACKAGE_VERSION_MAJOR "${PZFXR_VERSION_MAJOR}")
set (CPACK_PACKAGE_VERSION_MINOR "${PZFXR_VERSION_MINOR}")
set (CPACK_PACKAGE_VERSION_PATCH "${PZFXR_VERSION_PATCH}")
set (CPACK_PACKAGE_VENDOR "Nathan Whitehead")
set (CPACK_PACKAGE_EXECUTABLES "pzfxr" "PuzzleScript Sound Effectzor")
# Windows gets custom installer
if(WIN32)
    set (CPACK_GENERATOR ${CPACK_GENERATOR} NSIS)
    set (CPACK_RESOURCE_FILE_LICENSE "${PROJECT_SOURCE_DIR}/LICENSE")
    set (CPACK_NSIS_MODIFY_PATH ON)
endif(WIN32)

include (CPack)
