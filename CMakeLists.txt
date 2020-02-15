cmake_minimum_required (VERSION 3.10)


project (SymuVia VERSION 1.0.0)

# Set path for libraries 
# set(LIB_ENV_DIRECTORY "/usr/local/opt/buildsymuvia/lib" CACHE PATH "Library folder Boost GDAL Rapidjson Odbc Xerces")
if(APPLE)
    set(LOCAL_LIB_DIRECTORY "/usr/local/lib/" CACHE PATH "General library folder" )
    set(BOOST_LIB_DIRECTORY "/usr/local/lib/" CACHE PATH "Boost library folder")
    set(XQILLA_LIB_DIRECTORY "/usr/local/lib/" CACHE PATH "Xqilla library folder")
    set(XERCESC_LIB_DIRECTORY "/usr/local/lib/" CACHE PATH "Xerces-c library folder")  
    set(GDAL_LIB_DIRECTORY "/usr/lib/" CACHE PATH "GDAL lib directory")
    set(ODBC_LIB_DIRECTORY "/usr/local/lib/" CACHE PATH "ODBC lib directory")
    set(PYTHON_LIB_DIRECTORY "/Library/Frameworks/Python.framework/Versions/3.6/lib/" CACHE PATH "Python library folder")
else()
    set(LIB_LOCAL_DIRECTORY "/usr/local/lib/" CACHE PATH "General library folder" )
    set(BOOST_LIB_DIRECTORY "/usr/lib/x86_64-linux-gnu/" CACHE PATH "Boost library folder")
    set(XQILLA_LIB_DIRECTORY "/usr/lib/x86_64-linux-gnu/" CACHE PATH "Xqilla library folder")
    set(XERCESC_LIB_DIRECTORY "/usr/lib/x86_64-linux-gnu/" CACHE PATH "Xerces-c library folder")    
    set(GDAL_LIB_DIRECTORY "/usr/lib/" CACHE PATH "GDAL lib directory")
    set(ODBC_LIB_DIRECTORY "/usr/lib/x86_64-linux-gnu/" CACHE PATH "ODBC lib directory")
    set(PYTHON_LIB_DIRECTORY "/usr/lib/x86_64-linux-gnu/" CACHE PATH "Python library folder")
endif()
# Dynamic linking 
# https://stackoverflow.com/questions/26807329/no-rule-to-make-target-error-in-cmake-when-linking-to-shared-library
# link_directories(${LIB_ENV_DIRECTORY}) 
link_directories(${LIB_LOCAL_DIRECTORY})
link_directories(${BOOST_LIB_DIRECTORY})
link_directories(${XQILLA_LIB_DIRECTORY})
link_directories(${XERCESC_LIB_DIRECTORY})
link_directories(${GDAL_LIB_DIRECTORY})
link_directories(${PYTHON_LIB_DIRECTORY})

# Adding headers
if(APPLE)
    set(BOOST_LIB_INCLUDE_DIRECTORY "/usr/local/opt/buildsymuvia/include" CACHE PATH "Boost headers folder")
    set(PYTHON_LIB_INCLUDE_DIRECTORY "/Library/Frameworks/Python.framework/Versions/3.6/include/python3.6m" CACHE PATH "Python 3.6 headers folder")
    set(XQILLA_LIB_INCLUDE_DIRECTORY "/usr/local/include" CACHE PATH "XQilla include folder")
    set(GDAL_LIB_INCLUDE_DIRECTORY "/usr/include/gdal" CACHE PATH "GDAL include folder")
else()
    set(BOOST_LIB_INCLUDE_DIRECTORY "/usr/include/boost/" CACHE PATH "Boost headers folder")
    set(PYTHON_LIB_INCLUDE_DIRECTORY "/usr/include/python3.6m/" CACHE PATH "Python 3.6 headers folder")
    set(XQILLA_LIB_INCLUDE_DIRECTORY "/usr/include/" CACHE PATH "XQilla include folder")
    set(GDAL_LIB_INCLUDE_DIRECTORY "/usr/include/gdal" CACHE PATH "GDAL include folder")
endif()

include_directories(${BOOST_LIB_INCLUDE_DIRECTORY}) 
include_directories(${PYTHON_LIB_INCLUDE_DIRECTORY}) 
include_directories(${XQILLA_LIB_INCLUDE_DIRECTORY})
include_directories(${GDAL_LIB_INCLUDE_DIRECTORY})



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
    set(BOOST_LOCALE_RELEASE_LIB_NAME "libboost_locale-mt.dylib" CACHE STRING "Boost date_time debug library name")
    set(BOOST_SERIALIZATION_RELEASE_LIB_NAME "libboost_serialization.dylib" CACHE STRING "Boost serialization release lib name")
    set(BOOST_WSERIALIZATION_RELEASE_LIB_NAME "libboost_wserialization.dylib" CACHE STRING "Boost wserialization release lib name")
    set(BOOST_PYTHON_RELEASE_LIB_NAME "libboost_python27.dylib" CACHE STRING "Boost python release lib name")
    set(BOOST_LOG_RELEASE_LIB_NAME "libboost_log.dylib" CACHE STRING "Boost log release lib name")
    set(BOOST_SYSTEM_RELEASE_LIB_NAME "libboost_system.dylib" CACHE STRING "Boost system release lib name")
    set(BOOST_FILESYSTEM_RELEASE_LIB_NAME "libboost_filesystem.dylib" CACHE STRING "Boost filesystem release lib name")
    set(BOOST_THREAD_RELEASE_LIB_NAME "libboost_thread-mt.dylib" CACHE STRING "Boost thread release lib name")
    set(BOOST_CHRONO_RELEASE_LIB_NAME "libboost_chrono.dylib" CACHE STRING "Boost chrono release lib name")    
    set(GDAL_LIB_NAME "libgdal.dylib" CACHE STRING "Full path of the GDAL x64 lib")
    set(OBDC_RELEASE_LIB_NAME "libodbc.dylib" CACHE STRING "OBDC Library name" )
    set(PYTHON_RELEASE_LIB_NAME "libpython3.6m.dylib" CACHE STRING "Python Library name" )  
    set(XERCES_RELEASE_LIB_NAME "libxerces-c-3.2.dylib" CACHE STRING "Xerces Library name") 
    set(XQILLA_RELEASE_LIB_NAME "libxqilla.dylib" CACHE STRING "Xqilla Library name") 
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
    set(GDAL_LIB_NAME "libgdal.so" CACHE FILE "Full path of the GDAL x64 lib")
    set(OBDC_RELEASE_LIB_NAME "libodbc.so" CACHE STRING "OBDC Library name" )
    set(PYTHON_RELEASE_LIB_NAME "libpython3.6m.so" CACHE STRING "Python Library name")  
    set(XERCES_RELEASE_LIB_NAME "libxerces-c.so" CACHE STRING "Xerces Library name")      
    set(XQILLA_RELEASE_LIB_NAME "libxqilla.so.6" CACHE STRING "Xqilla Library name") 
endif()

add_subdirectory(SymuCore)
add_subdirectory(SymuVia)
