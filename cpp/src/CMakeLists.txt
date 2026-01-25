project(Cucumber-Tag-Expressions-Lib)

add_library(cucumber-tag-expressions)
add_library(cucumber::tag-expressions ALIAS cucumber-tag-expressions)

target_sources(cucumber-tag-expressions
    PRIVATE
        lib/expression.cpp
        lib/parser.cpp
)

target_include_directories(cucumber-tag-expressions
    PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/../include>
        $<INSTALL_INTERFACE:include>
)

