# FindDoxygen and doxygen_add_docs() Example

Simple example on using CMake to run Doxygen automatically.


## OS/Versions Used

OS: Windows 11, Ubuntu

CMake Version: 3.28.3 (Ubuntu) and 4.1.0-rc2 (Windows)

CMake Generator: Ninja Multi-Config (Ubuntu) and Visual Studio 17 2022 (Windows)

Doxygen Version: 1.9.8 and 1.14.0






## Setting up Doxygen using custom Doxyfile

Save your settings for Doxygen in a Doxyfile using the terminal or 
with Doxywizard. The default name is "Doxyfile".

Terminal:
```
doxygen -g <config-file-name>
```

The CONFIG_FILE parameter for doxygen_add_docs() is used to point to 
the desired Doxyfile.

CMakeLists.txt:
```
set(DOXYGEN_INPUT_DIR ${PROJECT_SOURCE_DIR}/src)
set(DOXYGEN_OUTPUT_DIR ${CMAKE_CURRENT_BINARY_DIR}/doxygen)



file(MAKE_DIRECTORY ${DOXYGEN_OUTPUT_DIR}) 
doxygen_add_docs(doxygen 
                 ${DOXYGEN_INPUT_DIR} 
                 ALL 
                 WORKING_DIRECTORY ${DOXYGEN_OUTPUT_DIR} 
                 CONFIG_FILE path/to/Doxyfile)
```
You can also control different settings in CMake directly by
using configure_file().
Change the extension of the Doxyfile to .in (Doxyfile.in)
and replace any settings with CMake variables surrounded by
@cmake_variable_name@.

Doxyfile.in Example:
```
INPUT                  = "@DOXYGEN_INPUT_DIR@"

...

OUTPUT_DIRECTORY       = @DOXYGEN_OUTPUT_DIR@

```

Setting DOXYGEN_INPUT_DIR and DOXYGEN_OUTPUT_DIR and then configuring this
.in file will replace what is between these @'s in the .in file and
create a Doxyfile in the desired location.

CMakeLists.txt

```
set(DOXYGEN_INPUT_DIR ${PROJECT_SOURCE_DIR}/src)
set(DOXYGEN_OUTPUT_DIR ${CMAKE_CURRENT_BINARY_DIR}/doxygen)


set(DOXYFILE_IN ${CMAKE_CURRENT_SOURCE_DIR}/Doxyfile.in)
set(DOXYFILE_OUT ${CMAKE_CURRENT_BINARY_DIR}/Doxyfile)


configure_file(${DOXYFILE_IN} ${DOXYFILE_OUT} @ONLY)


file(MAKE_DIRECTORY ${DOXYGEN_OUTPUT_DIR}) 
doxygen_add_docs(doxygen 
                 ${DOXYGEN_INPUT_DIR} 
                 ALL 
                 WORKING_DIRECTORY ${DOXYGEN_OUTPUT_DIR} 
                 CONFIG_FILE ${DOXYFILE_OUT})
```

## Setting up Doxygen settings using CMake variables

Older versions of CMake did not have doxygen_add_docs(), so a custom CMake command
was created to run Doxygen.  This required configuring the custom Doxyfile with
CMake.  However, now the Doxygen settings can be controlled in CMake without
configuring a custom Doxyfile.  Instead, just create CMake variables with the
prefix "DOXYGEN_" and the name of the Doxygen setting name in the Doxyfile.

When done this way, only the target name and input directory need to be supplied to
doxygen_add_docs().  

For Example,

Doxyfile:
```
GENERATE_LATEX = NO

...

USE_MATHJAX = NO
```
> [!NOTE]
> This Doxyfile is just to show example Doxygen setting names.  There is no need to create 
> this Doxyfile when using this method. CMake will generate the Doxyfile internally.


CMakeLists.txt:
```
set(DOXYGEN_GENERATE_LATEX "YES")
set(DOXYGEN_USE_MATHJAX "YES")

doxygen_add_docs(doxygen 
                 ${DOXYGEN_INPUT_DIR})

```

