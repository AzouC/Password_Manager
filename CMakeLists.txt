# Password_Manager/CMakeLists.txt
cmake_minimum_required(VERSION 3.16)
project(PasswordManager VERSION 1.0.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# Options
option(BUILD_TESTS "Build tests" ON)
option(BUILD_DOCS "Build documentation" ON)

# Configuration OpenSSL (CRITIQUE)
find_package(OpenSSL REQUIRED)
include_directories(${OPENSSL_INCLUDE_DIR})

# Inclure les sous-répertoires core d'abord
add_subdirectory(core)

# Ensuite les applications
add_subdirectory(apps/task_manager)
add_subdirectory(apps/password_manager)

# Tests (optionnel)
if(BUILD_TESTS)
    enable_testing()
    add_subdirectory(tests)
endif()

# Documentation Doxygen
if(BUILD_DOCS)
    find_package(Doxygen)
    if(Doxygen_FOUND)
        doxygen_add_docs(docs ${CMAKE_CURRENT_SOURCE_DIR})
    endif()
endif()
