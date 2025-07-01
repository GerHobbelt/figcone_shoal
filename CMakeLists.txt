cmake_minimum_required(VERSION 3.18)

project(figcone_shoal VERSION 1.2.0 DESCRIPTION "shoal parser for figcone library")
include(external/seal_lake)

SealLake_v040_IsInstallEnabled(INSTALL_FIGCONE_TREE)
SealLake_v040_Import(
        figcone_tree 2.2.0
        GIT_REPOSITORY https://github.com/kamchatka-volcano/figcone_tree.git
        GIT_TAG        v2.2.0
)

SealLake_v040_Bundle(
        NAME figcone_shoal_eel
        GIT_REPOSITORY https://github.com/kamchatka-volcano/eel.git
        GIT_TAG        v0.3.0
        TEXT_REPLACEMENTS
            "namespace eel" "namespace figcone::shoal::eel"
            EEL_ FIGCONE_SHOAL_EEL_
)

SealLake_v040_ObjectLibrary(
        NAMESPACE figcone
        COMPILE_FEATURES cxx_std_11
        SOURCES
            src/parser.cpp
            src/nodeparser.cpp
            src/paramparser.cpp
            src/stream.cpp
            src/utils.cpp
        LIBRARIES figcone_shoal_eel::figcone_shoal_eel
        INTERFACE_LIBRARIES figcone::figcone_tree
        DEPENDENCIES
            figcone_tree 2.2.0
)

SealLake_v040_OptionalSubProjects(tests)