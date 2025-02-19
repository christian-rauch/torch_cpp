cmake_minimum_required(VERSION 3.16 FATAL_ERROR)
project(torch_cpp CXX)

set(TORCH_URL       https://download.pytorch.org/libtorch/cu118/libtorch-cxx11-abi-shared-with-deps-2.6.0%2Bcu118.zip)
set(TORCH_URL_MD5   83de2a88feb477d848dc5544bca00e62)

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


# manually install header, libraries and config files

install(DIRECTORY ${TORCH_PATH}/include/
    DESTINATION include
    FILES_MATCHING PATTERN "*.h*"
)

install(DIRECTORY ${TORCH_PATH}/lib/
    DESTINATION lib
)

install(DIRECTORY ${TORCH_PATH}/share/
    DESTINATION share
)
