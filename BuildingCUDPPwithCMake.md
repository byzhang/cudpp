Note this applies to CUDPP 2.0 and later only.

# Introduction #

To generate makefiles for OS X or Linux, or MS Visual Studio files for Windows, you can either run cmake at the command line or launch cmake-gui.

# Installing CMake #

Just download a CMake installer from here:
http://www.cmake.org/cmake/resources/software.html

# Command Line #

` cmake <path to CUDPP source tree> `.

If the current directory is the CUDPP source tree, you will perform an in-source build, which can clutter up the source tree with intermediate files and cmake scripts.  It is preferable to  run cmake from a different directory outside the source tree, known as an [out-of-source build](http://www.vtk.org/Wiki/CMake_FAQ#Out-of-source_build_trees).

If you need to set any options for the build script/makefile generation, you can run cmake interactively with the following command.

` cmake -i <path to CUDPP source tree> `

# cmake-gui #

The cmake gui can be used to interactively configure and generate CUDPP build files.  Just run cmake-gui, then set the path to the CUDPP source tree in the field "Where is the source code", and set the path to where you want the build files generated in "Where to build the binaries".

Then press "Configure".  You will see a list of options you can set. Click "Advanced" to see advanced options.  Click "grouped" to logically group them.

Once you have set the necessary options (see below), click "Generate" to generate makefiles.

Go to the directory you set in "Where to build the binaries", and run make (` * `nix), or open the cudpp.sln (Windows).

# Options #

Useful options to set:
  * CMAKE\_BUILD\_TYPE: set to Debug for debug builds, Release (or blank) for release builds.  Not needed on Windows.
  * BUILD\_APPLICATIONS: set to on to build the CUDPP example applications and testrig in addition to CUDPP libraries.
  * BUILD\_SHARED\_LIBS: set to on to build dynamic/shared CUDPP libraries, off to build static libraries
  * CUDA\_VERBOSE\_BUILD: Print out commands run while compiling CUDA source files
  * CUDA\_VERBOSE\_PTXAS: Print out the output of --ptxas-options=-verbose, which displays details of shared memory, registers, and constants used by CUDA device kernels.

## Debug vs. Release builds ##

The default cmake build is release.  To generate debug CUDPP libraries, use

cmake -DCMAKE\_BUILD\_TYPE=Debug

# Example cmake interactive transcript #

The following shows a transcript of generating an [out-of-source build tree](http://www.vtk.org/Wiki/CMake_FAQ#Out-of-source_build_trees) for CUDPP on Windows 7.

```
C:\src>mkdir cudpp_test

C:\src>cd cudpp_test

C:\src\cudpp_test>cmake -i ../cudpp/trunk
Would you like to see advanced options? [No]:
Please wait while cmake processes CMakeLists.txt files....

-- Building for: Visual Studio 9 2008


Variable Name: BUILD_APPLICATIONS
Description: If on, builds the sample applications.
Current Value: OFF
New Value (Enter to keep current value): ON

Variable Name: BUILD_SHARED_LIBS
Description: On to build shared libraries, off for static libraries.
Current Value: OFF
New Value (Enter to keep current value): ON

Variable Name: CMAKE_INSTALL_PREFIX
Description: Install path prefix, prepended onto install directories.
Current Value: C:/Program Files (x86)/cudpp
New Value (Enter to keep current value): c:/temp/cudpp

Variable Name: CUDA_BUILD_CUBIN
Description: Generate and parse .cubin files in Device mode.
Current Value: OFF
New Value (Enter to keep current value):

Variable Name: CUDA_BUILD_EMULATION
Description: Build in Emulation mode
Current Value: OFF
New Value (Enter to keep current value):

Variable Name: CUDA_SDK_ROOT_DIR
Description: Path to a file.
Current Value: CUDA_SDK_ROOT_DIR-NOTFOUND
New Value (Enter to keep current value):

Variable Name: CUDA_TOOLKIT_ROOT_DIR
Description: Toolkit location.
Current Value: C:/Program Files/NVIDIA GPU Computing Toolkit/CUDA/v4.0
New Value (Enter to keep current value):

Variable Name: CUDA_VERBOSE_BUILD
Description: Print out the commands run while compiling the CUDA source file.  W
ith the Makefile generator this defaults to VERBOSE variable specified on the co
mmand line, but can be forced on with this option.
Current Value: OFF
New Value (Enter to keep current value): ON

Variable Name: CUDA_VERBOSE_PTXAS
Description: On to enable verbose output from the PTXAS assembler.
Current Value: OFF
New Value (Enter to keep current value): ON

Variable Name: EXECUTABLE_OUTPUT_PATH
Description: Directory where all executables will be stored
Current Value: C:/src/cudpp_test/bin
New Value (Enter to keep current value):

Variable Name: LIBRARY_OUTPUT_PATH
Description: Directory where all the libraries will be stored
Current Value: C:/src/cudpp_test/lib
New Value (Enter to keep current value):

Please wait while cmake processes CMakeLists.txt files....



Variable Name: GLEW_INCLUDE_PATH
Description: The directory where GL/glew.h resides
Current Value: C:/src/cudpp/trunk/apps/common/include
New Value (Enter to keep current value):

Variable Name: GLEW_LIBRARY
Description: The GLEW library
Current Value: C:/src/cudpp/trunk/apps/common/lib/glew32.lib
New Value (Enter to keep current value):

Please wait while cmake processes CMakeLists.txt files....



CMake complete, run make to build project.

```

On Windows, rather than running make, you just open the generated cudpp.sln in your source directory.