# LibTorch install script for CMake

This CMake project is basically an install script for LibTorch (PyTorch C++ API). It downloads the binary archieve and installs headers, libraries and CMake configurations files to the corresponding `INCLUDEDIR`, `LIBDIR` and `DATADIR` directories.

The package can be used as part of a pure CMake catkin or colcon workspace by including:
```XML
  <buildtool_depend>cmake</buildtool_depend>
  <depend>torch_cpp</depend>
  <export>
    <build_type>cmake</build_type>
  </export>
```
in your `package.xml`. The relevant files will then be installed within the workspace target folder (`install` or `devel`).

Usage in a CMake project:
```CMake
find_package(Torch REQUIRED)
target_link_libraries(${PROJECT_NAME} PUBLIC torch)
set_property(TARGET ${PROJECT_NAME} PROPERTY CXX_STANDARD 14)
target_link_options(${PROJECT_NAME} PUBLIC ${TORCH_CXX_FLAGS})
```

If you get the error `No CMAKE_CUDA_COMPILER could be found.`, then the CUDA compiler `nvcc` cannot be found in the default search paths (`$PATH`). In this case, you have to set the path to `nvcc` manually:
```sh
export CUDACXX=/usr/local/cuda/bin/nvcc
```
