#  Copyright 2020 Tangent Animation
#
#  Licensed under the Apache License, Version 2.0 (the "License");
#  you may not use this file except in compliance with the License.
#  You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
#  Unless required by applicable law or agreed to in writing, software
#  distributed under the License is distributed on an "AS IS" BASIS,
#  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied,
#  including without limitation, as related to merchantability and fitness
#  for a particular purpose.
#
#  In no event shall any copyright holder be liable for any damages of any kind
#  arising from the use of this software, whether in contract, tort or otherwise.
#  See the License for the specific language governing permissions and
#  limitations under the License.

set(PXR_PREFIX "")
set(PXR_PACKAGE ndrCycles)

add_custom_target(shared_libs)

if(USE_LEGACY_HOUDINI)
  include_directories(${HOUDINI_INCLUDE_DIRS})
  link_directories(${HOUDINI_LIB_DIRS})
  link_libraries(${HOUDINI_LIBRARIES_DEPS})
endif()

if(USE_OPENGL)
  include_directories(${GLEW_INCLUDE_DIR} ${OPENGL_INCLUDE_DIR})
  link_libraries(${OPENGL_gl_LIBRARY} ${GLEW_LIBRARY})
endif()

pxr_plugin(${PXR_PACKAGE}
  LIBRARIES
    ${USD_LIBRARIES}
    ${TBB_LIBRARIES}
    ${Boost_LIBRARIES}
    ${HBoost_LIBRARIES}
    ${Python_LIBRARIES}            
    ${CYCLES_LIBRARIES}
    ${PNG_LIBRARIES}
    ${ZLIB_LIBRARIES}
    ${TIFF_LIBRARY}
    ${PTHREADS_LIBRARIES}
    ${OPENJPEG_LIBRARIES}
    ${OIIO_LIBRARIES}
    ${OPENEXR_LIBRARIES}

  INCLUDE_DIRS
    ${USD_INCLUDE_DIR}
    ${Boost_INCLUDE_DIRS}
    ${HBoost_INCLUDE_DIRS}
    ${Python_INCLUDE_DIRS}
    ${PYTHON_INCLUDE_DIR}
    ${CYCLES_INCLUDE_DIRS}
    ${OIIO_INCLUDE_DIRS}
    ${OPENEXR_INCLUDE_DIRS}
    ${TBB_INCLUDE_DIRS}

  PUBLIC_CLASSES
    discovery
    parser

  PUBLIC_HEADERS
    api.h

  RESOURCE_FILES
    plugInfo.json

  DISABLE_PRECOMPILED_HEADERS
)
