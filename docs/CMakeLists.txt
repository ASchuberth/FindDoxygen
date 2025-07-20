
# Documentation


find_package(Doxygen REQUIRED)


# Directory containing source code for doxygen to parse
set(DOXYGEN_INPUT_DIR ${PROJECT_SOURCE_DIR}/src)

# Output directory of generated doxygen docs
# Gets added to Doxyfile later with configure_file()
set(DOXYGEN_OUTPUT_DIR ${CMAKE_CURRENT_BINARY_DIR}/doxygen)

# Locations of the input Doxyfile.in and where the outputted 
# Doxyfile should go
set(DOXYFILE_IN ${CMAKE_CURRENT_SOURCE_DIR}/Doxyfile.in)
set(DOXYFILE_OUT ${CMAKE_CURRENT_BINARY_DIR}/Doxyfile)

# Sets OUTPUT_DIRECTORY in Doxyfile replacing @DOXYGEN_OUTPUT_DIR@
# and @DOXYGEN_INPUT_DIR@ in Doxyfile.in
configure_file(${DOXYFILE_IN} ${DOXYFILE_OUT} @ONLY)

# Create the output directory, doxygen/, if not already there
file(MAKE_DIRECTORY ${DOXYGEN_OUTPUT_DIR}) 
doxygen_add_docs(doxygen 
                 ${DOXYGEN_INPUT_DIR} # Sets INPUT variable for doxygen
                 ALL 
                 WORKING_DIRECTORY ${DOXYGEN_OUTPUT_DIR} 
                 CONFIG_FILE ${DOXYFILE_OUT})



message("DOXYGEN_INPUT_DIR: ${DOXYGEN_INPUT_DIR}")
message("DOXYGEN_OUTPUT_DIR: ${DOXYGEN_OUTPUT_DIR}")
message("DOXYFILE_IN: ${DOXYFILE_IN}")
message("DOXYFILE_OUT: ${DOXYFILE_OUT}")





