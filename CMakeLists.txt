cmake_minimum_required (VERSION 3.12)


project (SymuVia VERSION 1.0.0)

# Set path for libraries 
set(LIB_DIRECTORIES "/usr/local/opt/buildsymuvia/lib" CACHE PATH "Boost library folder")
set(LIB_OBDC "/usr/local/lib/libodbc.dylib" CACHE PATH "OBDC library folder" )

# Adding headers
set(LIB_INCLUDE_DIRECTORY "/usr/local/opt/buildsymuvia/include" CACHE PATH "Boost headers folder")
set(LIBPYTHON_INCLUDE_DIRECTORY "/usr/local/opt/buildsymuvia/include/python3.6m" CACHE PATH "Python 3.6 headers folder")
include_directories(${LIB_INCLUDE_DIRECTORY}) 
include_directories(${LIBPYTHON_INCLUDE_DIRECTORY}) 

# Special library Xqilla (Only for mac/unix)
set(XQILLA_INCLUDE_DIRECTORY "/usr/local/include" CACHE PATH "XQilla include folder")
include_directories(${XQILLA_INCLUDE_DIRECTORY})

# Define libraries to link
SET(CMAKE_BUILD_WITH_INSTALL_RPATH FALSE)
SET(CMAKE_INSTALL_RPATH ${LIB_DIRECTORIES})
SET(CMAKE_INSTALL_RPATH_USE_LINK_PATH TRUE)

# Activate C++11 support under Linux
if(CMAKE_COMPILER_IS_GNUCXX OR APPLE)
    list( APPEND CMAKE_CXX_FLAGS "-std=c++0x")
endif()

# Function for printing included files
function(print_files list_files)
    foreach(file IN LISTS "${list_files}")
        message(STATUS "File: ${file}")
    endforeach()
endfunction()

# Libraries 
# To optimize 
if(APPLE)
    set(BOOST_DATE_TIME_RELEASE_LIB_NAME "libboost_date_time.dylib" CACHE STRING "Boost date_time release library name")
    set(BOOST_LOCALE_RELEASE_LIB_NAME "libboost_locale.dylib" CACHE STRING "Boost date_time debug library name")
    set(BOOST_SERIALIZATION_RELEASE_LIB_NAME "libboost_serialization.dylib" CACHE STRING "Boost serialization release lib name")
    set(BOOST_WSERIALIZATION_RELEASE_LIB_NAME "libboost_wserialization.dylib" CACHE STRING "Boost wserialization release lib name")
    set(BOOST_PYTHON_RELEASE_LIB_NAME "libboost_python.dylib" CACHE STRING "Boost python release lib name")
    set(BOOST_LOG_RELEASE_LIB_NAME "libboost_log.dylib" CACHE STRING "Boost log release lib name")
    set(BOOST_SYSTEM_RELEASE_LIB_NAME "libboost_system.dylib" CACHE STRING "Boost system release lib name")
    set(BOOST_FILESYSTEM_RELEASE_LIB_NAME "libboost_filesystem.dylib" CACHE STRING "Boost filesystem release lib name")
    set(BOOST_THREAD_RELEASE_LIB_NAME "libboost_thread.dylib" CACHE STRING "Boost thread release lib name")
    set(BOOST_CHRONO_RELEASE_LIB_NAME "libboost_chrono.dylib" CACHE STRING "Boost chrono release lib name")    
    set(GDAL_LIB_NAME "libgdal.dylib" CACHE FILE "Full path of the GDAL x64 lib")
    set(OBDC_RELEASE_LIB_NAME "libobdc.dylib" CACHE FILE "OBDC Library manager" )
else()
    set(BOOST_DATE_TIME_RELEASE_LIB_NAME "libboost_date_time.so" CACHE STRING "Boost date_time release library name")
    set(BOOST_LOCALE_RELEASE_LIB_NAME "libboost_locale.so" CACHE STRING "Boost date_time debug library name")
    set(BOOST_SERIALIZATION_RELEASE_LIB_NAME "libboost_serialization.so" CACHE STRING "Boost serialization release lib name")
    set(BOOST_WSERIALIZATION_RELEASE_LIB_NAME "libboost_wserialization.so" CACHE STRING "Boost wserialization release lib name")
    set(BOOST_PYTHON_RELEASE_LIB_NAME "libboost_python.so" CACHE STRING "Boost python release lib name")
    set(BOOST_LOG_RELEASE_LIB_NAME "libboost_log.so" CACHE STRING "Boost log release lib name")
    set(BOOST_SYSTEM_RELEASE_LIB_NAME "libboost_system.so" CACHE STRING "Boost system release lib name")
    set(BOOST_FILESYSTEM_RELEASE_LIB_NAME "libboost_filesystem.so" CACHE STRING "Boost filesystem release lib name")
    set(BOOST_THREAD_RELEASE_LIB_NAME "libboost_thread.so" CACHE STRING "Boost thread release lib name")
    set(BOOST_CHRONO_RELEASE_LIB_NAME "libboost_chrono.so" CACHE STRING "Boost chrono release lib name")    
    set(GDAL_LIB_NAME "libgdal.dylib" CACHE FILE "Full path of the GDAL x64 lib")
endif()

add_subdirectory(SymuCore)
add_subdirectory(SymuVia)
