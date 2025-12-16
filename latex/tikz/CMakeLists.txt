cmake_minimum_required(VERSION 3.25)

project(tikz_learning LANGUAGES NONE)

list(APPEND CMAKE_MODULE_PATH 
	"${CMAKE_CURRENT_LIST_DIR}/cmake"
)
	
find_package(LATEX REQUIRED)
find_package(LatexMk REQUIRED)

add_custom_target(pdf ALL
	COMMAND ${LATEXMK_EXECUTABLE} document.tex
		-r "${CMAKE_CURRENT_BINARY_DIR}/latexmkrc"
		-verbose
	WORKING_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}"
	BYPRODUCTS 
		"${CMAKE_CURRENT_BINARY_DIR}/out" 
		"${CMAKE_CURRENT_BINARY_DIR}/aux"
	COMMENT "Building pdf with latexmk"
)
configure_file("${CMAKE_CURRENT_SOURCE_DIR}/latexmkrc.in"
	"${CMAKE_CURRENT_BINARY_DIR}/latexmkrc" @ONLY
)
