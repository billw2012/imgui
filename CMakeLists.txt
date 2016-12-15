cmake_minimum_required(VERSION 3.5)

file(GLOB_RECURSE header_files imgui.h imgui_internal.h stb_rect_pack.h stb_textedit.h stb_truetype.h)
file(GLOB_RECURSE src_files imgui.cpp imgui_draw.cpp)

add_library(imgui ${src_files} ${header_files})

foreach(file IN LISTS src_files)
    get_filename_component(file_dir "${file}" DIRECTORY)
	file(RELATIVE_PATH relative_path "${CMAKE_CURRENT_SOURCE_DIR}" "${file_dir}")
    string(REPLACE "/" "\\" path_msvc "${relative_path}")
    source_group("${path_msvc}" FILES ${file})
endforeach()
foreach(file IN LISTS header_files)
    get_filename_component(file_dir "${file}" DIRECTORY)
	file(RELATIVE_PATH relative_path "${CMAKE_CURRENT_SOURCE_DIR}" "${file_dir}")
    string(REPLACE "/" "\\" path_msvc "${relative_path}")
    source_group("${path_msvc}" FILES ${file})
endforeach()
