cmake_minimum_required(VERSION 3.0 FATAL_ERROR)
project(torch_cpp CXX)

set(TORCH_URL https://download.pytorch.org/libtorch/cu111/libtorch-cxx11-abi-shared-with-deps-1.8.0%2Bcu111.zip)
set(TORCH_URL_MD5 f6ab838b62fba8f875ccbceeeb71c6cd)

include(ExternalProject)
ExternalProject_Add(torch_archive
  URL               ${TORCH_URL}
  URL_MD5           ${TORCH_URL_MD5}
  PREFIX            torch_archive
  CONFIGURE_COMMAND ""
  BUILD_COMMAND     ""
  INSTALL_COMMAND   ""
)

ExternalProject_Get_Property(torch_archive SOURCE_DIR)

set(TORCH_PATH ${SOURCE_DIR})


add_library(${PROJECT_NAME} SHARED IMPORTED)
add_dependencies(${PROJECT_NAME} torch_ext_archive)

# manually install header, libraries and config files

include(GNUInstallDirs)

install(DIRECTORY ${TORCH_PATH}/include/
    DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
    FILES_MATCHING PATTERN "*.h*"
)

install(DIRECTORY ${TORCH_PATH}/lib/
    DESTINATION ${CMAKE_INSTALL_LIBDIR}
)

install(DIRECTORY ${TORCH_PATH}/share/
    DESTINATION ${CMAKE_INSTALL_DATADIR}
)
