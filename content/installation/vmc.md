+++
title = "Installing VMC"
menuTitle = "VMC"
chapter = false
weight = 1
+++

VMC requires [ROOT](https://root.cern.ch/).

The [vmc core package](/user-guide/vmc/vmc-library) was separated from the ROOT source into a new stand-alone [vmc](https://github.com/vmc-project/vmc) package in the GitHub [vmc-project](https://github.com/vmc-project) organization.  The motivation for this step was a gain in flexibility and faster workflow for new developments of multiple engine mode. The `vmc` package in ROOT is deprecated since ROOT version 6.18 (its compilation is optional) and it is going to be removed in the next ROOT version, 6.26. The VMC stand-alone is then needed for building Geant3 and Geant4 VMC when using ROOT compiled with the vmc disabled (default). 

VMC uses [CMake](https://cmake.org/) to configure a build system for compiling and installing the headers, libraries and Cmake configuration files. To install VMC:

1. First get the VMC source from the [Download page](/download/git-vmc). We will assume that the VMC package sits in a subdirectory
```
/mypath/vmc
```

2. Create build directory alongside our source directory
```
$ cd /mypath
$ mkdir vmc_build
$ ls
 vmc vmc_build
```

3. To configure the build, change into the build directory and run CMake:
```
$ cd /mypath/vmc_build
$ cmake -DCMAKE_INSTALL_PREFIX=/mypath/vmc_install /mypath/vmc
```
  - If ROOT environment was defined using `thisroot.{c}sh` script, there is no need to provide the path to its installation. Otherwise, they can be provided using `-DROOT_DIR` cmake option.

  - The VMC library is built by default in `RelWithDebInfo` build mode (Optimized build with debugging symbols). This default can be changed via the standard CMake option `CMAKE_BUILD_TYPE`. The other useful values are <br>
      - `Release` : Optimized build, no debugging symbols <br>
      - `Debug` : Debugging symbols, no optimization <br>

4. After the configuration has run, CMake will have generated Unix Makefiles for building VMC. To run the build, simply execute make in the build directory:
```
$ make -jN
```
where N is the number of parallel jobs you require (e.g. if your machine has a dual core processor, you could set N to 2).

  - If you need more output to help resolve issues or simply for information, run make as
```
$ make -jN VERBOSE=1
```

5. Once the build has completed, you can install VMC to the directory you specified earlier in CMAKE_INSTALL_PREFIX by running
```
$ make install
```
