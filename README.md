
### Laboratory work VI

## Homework
CMakeLists.txt:

```bush
cmake_minimum_required(VERSION 3.22.1)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project(master)

add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/formatter_ex_lib formatter_ex_new_name)

target_include_directories(formatter_ex PUBLIC formatter_ex_lib formatter_lib hello_world_application solver_lib)

add_library(solver ${CMAKE_CURRENT_SOURCE_DIR}/solver_lib/solver.cpp)

add_executable(master ${CMAKE_CURRENT_SOURCE_DIR}/solver_application/equation.cpp)

target_link_libraries(master formatter formatter_ex solver)

install(TARGETS master
RUNTIME DESTINATION bin
)

include(CPackConfig.cmake)
```

CPackConfig.cmake

```bush
include(InstallRequiredSystemLibraries)


set(CPACK_PACKAGE_CONTACT super@student.bmstu.ru)
set(CPACK_PACKAGE_VERSION_MAJOR ${PRINT_VERSION_MAJOR})
set(CPACK_PACKAGE_VERSION_MINOR ${PRINT_VERSION_MINOR})
set(CPACK_PACKAGE_VERSION_PATCH ${PRINT_VERSION_PATCH})
set(CPACK_PACKAGE_VERSION_TWEAK ${PRINT_VERSION_TWEAK})


set(CPACK_PACKAGE_VERSION ${PRINT_VERSION})

set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "lab06")
set(CPACK_SOURCE_INSTALLED_DIRECTORIES "${CMAKE_SOURCE_DIR}; /")

set(CPACK_SOURCE_GENERATOR "TGZ;ZIP")

set(CPACK_RPM_PACKAGE_NAME "solver_lab")
set(CPACK_RPM_PACKAGE_RELEASE 1)


set(CPACK_DEBIAN_PACKAGE_NAME "lab06")
set(CPACK_DEBIAN_FILE_NAME "lab06.deb")
set(CPACK_DEBIAN_PACKAGE_ARCHITECTURE "all")
set(CPACK_DEBIAN_PACKAGE_MAINTAINER "Zerkasasa")
set(CPACK_DEBIAN_PACKAGE_DESCRIPTION "Let`s go")
set(CPACK_DEBIAN_PACKAGE_RELEASE 1)
set(CPACK_GENERATOR "DEB")

include(CPack)
```
cmake.yml:

```bush
name: CMake_Build

on:
  push:
    branches: [master]
  pull_request:
    branches: [master]

jobs: 
 build:
 
  runs-on: ubuntu-latest
  permissions:
    contents: write

  steps:
  - uses: actions/checkout@v4
    
  - name: Build 
    run: |
      cmake -H. -B_build
      cmake --build _build
      
  - name: my_exe
    run: |
      echo -e "1\n2\n1" | ${{github.workspace}}/_build/master
 
  - name: package
    run: cmake --build ${{github.workspace}}/_build --target package
  
  - name: package_source
    run: cmake --build ${{github.workspace}}/_build --target package_source

  - name: Artifact
    uses: actions/upload-artifact@v4
    with:
        name: master
        path: ${{github.workspace}}/_build/master

  - name: Make a release
    uses: ncipollo/release-action@v1.14.0
    with:
        artifacts: "${{github.workspace}}/_build/*.deb,${{github.workspace}}/_build/*.tar.gz,${{github.workspace}}/_build/*.zip"
        tag: 1.0.0
        token: ${{ secrets.GITHUB_TOKEN }}
        allowUpdates: tru
```



```
Copyright (c) 2015-2021 The ISC Authors
```
