cmake_minimum_required(VERSION 3.18)

project(figcone_shoal VERSION 1.2.0 DESCRIPTION "shoal parser for figcone library")
include(seal_lake.cmake)

SealLake_v040_IsInstallEnabled(INSTALL_FIGCONE_TREE)
find_package(figcone_tree 2.2.0 QUIET)
if (NOT TARGET figcone::figcone_tree)
    add_subdirectory(deps/figcone_tree)
endif()

SealLake_v040_LoadDirectory(deps/figcone_shoal_eel)

SealLake_v040_ObjectLibrary(
        NAMESPACE figcone
        COMPILE_FEATURES cxx_std_11
        SOURCES
            src/parser.cpp
            src/nodeparser.cpp
            src/paramparser.cpp
            src/stream.cpp
            src/utils.cpp
        INTERFACE_LIBRARIES
            figcone::figcone_tree
        LIBRARIES
            figcone_shoal_eel::figcone_shoal_eel
        DEPENDENCIES
            figcone_tree 2.2.0
)
