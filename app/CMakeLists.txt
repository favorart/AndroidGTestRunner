cmake_minimum_required(VERSION 3.4.1)

include(FetchContent)
#-----------------------------------------------------------------------------------
set(CMAKE_FOLDER "googletest")
FetchContent_Declare(
	googletest
	GIT_REPOSITORY    https://github.com/google/googletest.git
	GIT_TAG           v1.15.2
)
# For Windows: Prevent overriding the parent project's compiler/linker settings
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)
unset(CMAKE_FOLDER)
#-----------------------------------------------------------------------------------

#add_subdirectory(src/main/cpp/gtest)
add_library(GTestRunner SHARED
  src/main/cpp/GTestRunnerJNI.cpp
  src/main/cpp/tests.cpp
)
target_link_libraries(GTestRunner
  log
  #gtest
	GTest::gtest_main
 )

include(GoogleTest)
gtest_discover_tests(signilex-facade-test)
