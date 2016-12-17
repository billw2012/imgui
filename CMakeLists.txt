cmake_minimum_required(VERSION 3.5)

set(header_files imgui.h imgui_internal.h stb_rect_pack.h stb_textedit.h stb_truetype.h)
set(src_files imgui.cpp imgui_draw.cpp)
file(GLOB_RECURSE example_files examples/*.cpp examples/*.h)

add_library(imgui ${src_files} ${header_files} ${example_files})

set_source_files_properties(${example_files} PROPERTIES HEADER_FILE_ONLY true)

source_group("src" FILES src_files)
source_group("include" FILES header_files)

foreach(file IN LISTS example_files)
    get_filename_component(file_dir "${file}" DIRECTORY)
	file(RELATIVE_PATH relative_path "${CMAKE_CURRENT_SOURCE_DIR}" "${file_dir}")
    string(REPLACE "/" "\\" path_msvc "${relative_path}")
    source_group("${path_msvc}" FILES ${file})
endforeach()
