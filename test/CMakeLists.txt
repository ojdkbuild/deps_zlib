
cmake_minimum_required ( VERSION 2.8.12 )

# project
include ( ${CMAKE_CURRENT_LIST_DIR}/../../../resources/cmake/ojdkbuild_common.cmake )
project ( ojdkbuild_zlib_test CXX )

# dependencies
ojdkbuild_add_subdirectory ( ${CMAKE_CURRENT_LIST_DIR}/../../zlib )
set ( ${PROJECT_NAME}_DEPS zlib )
ojdkbuild_pkg_check_modules ( ${PROJECT_NAME}_DEPS_PC REQUIRED ${PROJECT_NAME}_DEPS )

# tests
enable_testing ( )
# zlib_test
add_executable ( zlib_test ${CMAKE_CURRENT_LIST_DIR}/zlib_test.cpp )
target_include_directories ( zlib_test BEFORE PRIVATE ${${PROJECT_NAME}_DEPS_PC_INCLUDE_DIRS} )
target_link_libraries ( zlib_test ${${PROJECT_NAME}_DEPS_PC_LIBRARIES} )
target_compile_options ( zlib_test PRIVATE ${${PROJECT_NAME}_DEPS_PC_CFLAGS_OTHER} )
set_target_properties ( zlib_test PROPERTIES FOLDER "test" )
if ( DEFINED CMAKE_MEMORYCHECK_COMMAND )
    add_test ( zlib_test 
            ${CMAKE_MEMORYCHECK_COMMAND} ${CMAKE_MEMORYCHECK_COMMAND_OPTIONS} 
            ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/zlib_test )
else ( )
    add_test ( zlib_test ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/zlib_test )
endif ( )
