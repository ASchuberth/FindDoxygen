
# Documentation


find_package(Doxygen REQUIRED)



set(DOXYGEN_INPUT_DIR ${PROJECT_SOURCE_DIR}/src)
set(DOXYGEN_OUTPUT_DIR ${CMAKE_CURRENT_BINARY_DIR}/doxygen)
set(DOXYGEN_INDEX_FILE ${DOXYGEN_OUTPUT_DIR}/xml/index.xml)
set(DOXYFILE_IN ${CMAKE_CURRENT_SOURCE_DIR}/Doxyfile.in)
set(DOXYFILE_OUT ${CMAKE_CURRENT_BINARY_DIR}/Doxyfile)

#Replace variables inside @@ with the current values
configure_file(${DOXYFILE_IN} ${DOXYFILE_OUT} @ONLY)


file(MAKE_DIRECTORY ${DOXYGEN_OUTPUT_DIR}) #Doxygen won't create this for us
doxygen_add_docs(doxygen ${DOXYGEN_INPUT_DIR} ALL WORKING_DIRECTORY ${DOXYGEN_OUTPUT_DIR} CONFIG_FILE ${DOXYFILE_OUT})



message("DOXYGEN_INPUT_DIR: ${DOXYGEN_INPUT_DIR}")
message("DOXYGEN_OUTPUT_DIR: ${DOXYGEN_OUTPUT_DIR}")
message("DOXYGEN_INDEX_FILE: ${DOXYGEN_INDEX_FILE}")
message("DOXYFILE_IN: ${DOXYFILE_IN}")
message("DOXYFILE_OUT: ${DOXYFILE_OUT}")





