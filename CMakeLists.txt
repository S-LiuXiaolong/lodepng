cmake_minimum_required(VERSION 3.5.1)
project(LodePNG)
set(CMAKE_CXX_STANDARD 98)

IF(${UNIX})
    set(MYGE_TARGET_PLATFORM "Linux")
ELSEIF(${WIN32})
    set(MYGE_TARGET_PLATFORM "Windows")
ENDIF(${UNIX})

set(MYGE_EXTERNAL_ROOT ${PROJECT_BINARY_DIR}/../../${MYGE_TARGET_PLATFORM})

include_directories(.)

add_library(lodepng)
target_sources(lodepng PRIVATE
    lodepng.cpp
)

set_target_properties(lodepng
PROPERTIES PUBLIC_HEADER lodepng.h
)

install(TARGETS lodepng
    PUBLIC_HEADER DESTINATION ${MYGE_EXTERNAL_ROOT}/include/lodepng
    ARCHIVE DESTINATION ${MYGE_EXTERNAL_ROOT}/lib/Debug
    CONFIGURATIONS Debug
)

install(TARGETS lodepng
    ARCHIVE DESTINATION ${MYGE_EXTERNAL_ROOT}/lib/Release
    CONFIGURATIONS Release
)

if(MSVC)
    install(FILES ${PROJECT_BINARY_DIR}/Debug/lodepng.pdb
        DESTINATION ${MYGE_EXTERNAL_ROOT}/lib/Debug
        CONFIGURATIONS Debug
        )
endif(MSVC)
