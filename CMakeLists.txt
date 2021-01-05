cmake_minimum_required (VERSION 3.6.3)
project (yahoo-finance CXX)

# Enable C+11
set (CMAKE_CXX_STANDARD 11)

# Library source files
file (GLOB LIB_SOURCES src/*.cpp)
file (GLOB LIB_HEADERS src/*.hpp )
add_library (yahoo-finance ${LIB_SOURCES} ${LIB_HEADERS})

set_target_properties(yahoo-finance PROPERTIES PUBLIC_HEADER "${LIB_HEADERS}")

INSTALL(TARGETS yahoo-finance 
	LIBRARY DESTINATION "/usr/local/lib"
	PUBLIC_HEADER DESTINATION "/usr/local/include/yahoo-finance")

# Example executable
add_executable (example src/example.cpp)
target_link_libraries (example yahoo-finance curl)

# Test
add_subdirectory (test)
enable_testing ()
add_test (NAME TimeUtilsTest
    COMMAND testTimeUtils
    )
add_test (NAME QuoteTest
    COMMAND testQuote
    )

# Documentation
add_subdirectory (doc)
