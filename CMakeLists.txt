# Copyright 2016, akashche at redhat.com
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

cmake_minimum_required ( VERSION 2.8.12 )

# project
include ( ${CMAKE_CURRENT_LIST_DIR}/../../resources/cmake/ojdkbuild_common.cmake )
project ( ojdkbuild_zlib C CXX )
set ( ${PROJECT_NAME}_OJDKBUILD_VERSION 1.2.7-1 )

# static library
ojdkbuild_add_external ( ${OJDKBUILD_DIR}/external/zlib )

add_custom_target ( zlib DEPENDS z )
add_custom_target ( ${PROJECT_NAME} DEPENDS zlib )

# shared pkg-config
set ( ${PROJECT_NAME}_MODULE ojdkbuild_zlib )
set ( ${PROJECT_NAME}_BUNDLE_LIB_PATH ${CMAKE_LIBRARY_OUTPUT_DIRECTORY}/${CMAKE_SHARED_LIBRARY_PREFIX}zlib${CMAKE_SHARED_LIBRARY_SUFFIX} )
set ( ${PROJECT_NAME}_PC_CFLAGS "-I${CMAKE_BINARY_DIR}/external_zlib/zlib_install/include" )
set ( ${PROJECT_NAME}_PC_LIBS "${CMAKE_ARCHIVE_OUTPUT_DIRECTORY}/${CMAKE_STATIC_LIBRARY_PREFIX}z${CMAKE_STATIC_LIBRARY_SUFFIX}" )
configure_file ( ${CMAKE_CURRENT_LIST_DIR}/../../resources/cmake/pkg-config.in 
        ${CMAKE_LIBRARY_OUTPUT_DIRECTORY}/pkgconfig/ojdkbuild_zlib.pc )
