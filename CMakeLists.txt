# НАСТРОЙКИ CMAKE
cmake_minimum_required(VERSION 3.29 FATAL_ERROR)

# Экспортировать комманды компилятора, если проект имеет статус "Debug"
if(CMAKE_BUILD_TYPE STREQUAL "Debug")
    set(CMAKE_EXPORT_COMPILE_COMMANDS)
endif()

# Папки для вывода таргетов проекта 
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib) 
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_Fortran_MODULE_DIRECTORY ${CMAKE_BINARY_DIR}/fortran_modules)

# =============================================

# Настройки проекта

project(project_name LANGUAGES Fortran)

target_include_directories(
    project_name PRIVATE ${CMAKE_CURRENT_BINARY_DIR}/fortran_modules
)

# Подключение директории с исходным кодом
target_include_directories(
    project_name PUBLIC $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/source>
                        $<INSTALL_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/source>
)

set_target_properties(
    project_name
    PROPERTIES Fortran_STANDARD 2018
               Fortran_STANDARD_REQUIRED on
               Fortran_EXTENSIONS off
)

# =============================================
# Добавление поддиректорий и сторонних библиотек
add_subdirectory(source)
