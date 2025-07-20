
# Documentation


find_package(Doxygen REQUIRED)


if(Doxygen_FOUND)


    # Doxyfile Configurations
    
    set(DOXYGEN_INPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/src)
    set(DOXYGEN_OUTPUT_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/doxygen)
    
    set(DOXYGEN_PROJECT_NAME "Find Doxygen Example" )
    
    set(DOXYGEN_FILE_PATTERNS *.cpp *.hpp *.md)
    set(DOXYGEN_FULL_PATH_NAMES "NO")
    set(DOXYGEN_EXTRACT_ALL "YES")
    set(DOXYGEN_EXTRACT_PRIVATE "YES")
    set(DOXYGEN_EXTRACT_PRIV_VIRTUAL "YES")
    set(DOXYGEN_EXTRACT_STATIC "YES")

    set(DOXYGEN_GENERATE_XML "YES")
    
    set(DOXYGEN_GENERATE_LATEX "YES")
    set(DOXYGEN_LATEX_CMD_NAME "latex")
    set(DOXYGEN_USE_MATHJAX "YES")

    set(DOXYGEN_HTML_COLORSTYLE "TOGGLE")
    set(DOXYGEN_HTML_DYNAMIC_MENUS "NO")

    # For future implementation of Sphinx and Breathe
    set(DOXYGEN_INDEX_FILE ${DOXYGEN_OUTPUT_DIRECTORY}/xml/index.xml)


    
    # Create the output directory if not already there
    file(MAKE_DIRECTORY ${DOXYGEN_OUTPUT_DIRECTORY}) 

    doxygen_add_docs(
                        doxygen 
                        ${DOXYGEN_INPUT_DIRECTORY}
                    )



    message("DOXYGEN_INPUT_DIRECTORY: ${DOXYGEN_INPUT_DIRECTORY}")
    message("DOXYGEN_OUTPUT_DIRECTORY: ${DOXYGEN_OUTPUT_DIRECTORY}")
    message("DOXYGEN_INDEX_FILE: ${DOXYGEN_INDEX_FILE}")


endif()













