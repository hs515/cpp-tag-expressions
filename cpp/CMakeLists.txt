cmake_minimum_required(VERSION 3.15)
project(Cucumber-Tag-Expressions VERSION 8.1.0 LANGUAGES CXX)

# Set C++ standard
if(NOT DEFINED CMAKE_CXX_STANDARD)
    set(CMAKE_CXX_STANDARD 17)
    set(CMAKE_CXX_STANDARD_REQUIRED ON)
    set(CMAKE_CXX_EXTENSIONS OFF)
elseif(CMAKE_CXX_STANDARD LESS 17)
    message(FATAL_ERROR "C++17 (above) is required")
endif()

###
#
# Options
#
###
option(CUCUMBER_TAG_EXPRESSIONS_TESTS	    "Enable build of the tests" OFF)
option(CUCUMBER_TAG_EXPRESSIONS_COVERAGE	"Enable instrumentation for code coverage" OFF)
option(CUCUMBER_TAG_EXPRESSIONS_STRICT      "Additional and more strict checks" OFF)

if(CUCUMBER_TAG_EXPRESSIONS_COVERAGE)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} --coverage")
endif()

if(CUCUMBER_TAG_EXPRESSIONS_STRICT)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Werror")
endif()

###
#
# Targets
#
###
add_subdirectory(src)
add_subdirectory(example)
add_subdirectory(tests)

###
#
# Installation support
#
###
install(TARGETS cucumber-tag-expressions
    EXPORT cucumber-tag-expressions-targets
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
    RUNTIME DESTINATION bin
    INCLUDES DESTINATION include
)

install(DIRECTORY include/
    DESTINATION include
)

install(EXPORT cucumber-tag-expressions-targets
    FILE cucumber-tag-expressions-targets.cmake
    NAMESPACE cucumber::
    DESTINATION lib/cmake/cucumber-tag-expressions
)

###
#
# Package configuration
#
###
include(CMakePackageConfigHelpers)
write_basic_package_version_file(
    "${CMAKE_CURRENT_BINARY_DIR}/cucumber-tag-expressions-config-version.cmake"
    VERSION ${PROJECT_VERSION}
    COMPATIBILITY AnyNewerVersion
)

configure_file(
    "${CMAKE_CURRENT_SOURCE_DIR}/cmake/cucumber-tag-expressions-config.cmake.in"
    "${CMAKE_CURRENT_BINARY_DIR}/cucumber-tag-expressions-config.cmake"
    @ONLY
)

install(FILES
    "${CMAKE_CURRENT_BINARY_DIR}/cucumber-tag-expressions-config.cmake"
    "${CMAKE_CURRENT_BINARY_DIR}/cucumber-tag-expressions-config-version.cmake"
    DESTINATION lib/cmake/cucumber-tag-expressions
)

