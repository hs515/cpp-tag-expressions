project(Cucumber-Tag-Expressions-Tests)

if(CUCUMBER_TAG_EXPRESSIONS_BUILD_TESTS)
    enable_testing()

    # Find Google Test (if available)
    find_package(GTest QUIET)
    if(GTest_FOUND)
        add_executable(tag_expressions_test
            src/test_errors.cpp
            src/test_evaluations.cpp
            src/test_expression.cpp
            src/test_parser.cpp
            src/test_parsing.cpp
            src/test_precedence.cpp
        )
        
        target_link_libraries(tag_expressions_test
            PRIVATE
                cucumber::tag-expressions
                GTest::gtest
                GTest::gtest_main
        )
        
        add_test(NAME tag_expressions_test COMMAND tag_expressions_test)
    endif()
endif()

