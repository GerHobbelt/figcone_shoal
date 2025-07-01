project(test_figcone_shoal)

set(SRC
        test_paramparser.cpp
        test_paramlistparser.cpp
        test_nodeparser.cpp
        test_nodelistparser.cpp
)

if(FIGCONE_SHOAL_TEST_RELEASE)
    add_subdirectory(release)
endif()

SealLake_v040_GoogleTest(
        SOURCES ${SRC}
        COMPILE_FEATURES cxx_std_17
        INCLUDES ../src
        PROPERTIES
            CXX_EXTENSIONS OFF
        LIBRARIES figcone::figcone_shoal
)
