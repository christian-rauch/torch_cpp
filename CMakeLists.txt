cmake_minimum_required(VERSION 3.0 FATAL_ERROR)
project(torch_cpp CXX)

set(TORCH_URL       https://download.pytorch.org/libtorch/cu118/libtorch-cxx11-abi-shared-with-deps-2.1.2%2Bcu118.zip)
set(TORCH_URL_MD5   9a895fc9c942c63154edbc48ae700adb)

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
