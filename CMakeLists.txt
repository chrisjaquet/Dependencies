CMAKE_MINIMUM_REQUIRED(VERSION 2.6)
PROJECT(ClementineWindowsDependencies)

# This script is only for building on windows
IF(NOT ${CMAKE_SYSTEM_NAME} MATCHES "Windows")
    MESSAGE(FATAL_ERROR "This CMake script is only for building on windows")
ENDIF()

# Determine architecture bitness
IF(CMAKE_SIZEOF_VOID_P EQUAL 4)
    SET(ARCH_BITNESS "32")
ELSEIF(CMAKE_SIZEOF_VOID_P EQUAL 8)
    SET(ARCH_BITNESS "64")
ELSE()
    MESSAGE(FATAL_ERROR "Could not determine bitness (32 or 64) of architecture.")
ENDIF()

# Find a working version of patch
FIND_PROGRAM(PATCH_BINARY "patch" HINTS "bin" DOC "The patch executable used to patch source files using a diff file" NO_DEFAULT_PATH)
FIND_PROGRAM(PATCH_BINARY "patch")
IF(NOT PATCH_BINARY)
    MESSAGE(FATAL_ERROR "A patch program is required.")
ENDIF()

# Specify the downloaded source location
SET(DOWNLOADS_FOLDER ${CMAKE_CURRENT_SOURCE_DIR}/"downloads" CACHE STRING "Location of dowloaded source archives.")

# Find the downloader python file
FIND_FILE(DOWNLOADER_PY "downloader.py" HINTS "downloader" DOC "The downloader.py file used to obtain the dependencies' source archives.")
IF(NOT DOWNLOADER_PY)
    MESSAGE(FATAL_ERROR "Downloader.py python script could not be found.")
ENDIF()
FIND_PACKAGE(PythonInterp REQUIRED)

INCLUDE("DependencyData.cmake")

ADD_CUSTOM_TARGET(DownloadDependencies
        ${PYTHON_INTERP} ${DOWNLOADER_PY} --output "${DOWNLOADS_FOLDER}"
        COMMENT "Download the dependencies from the remote source")

# Now extract all the various 


	python $(src)/downloader/downloader.py --output "$(downloads)"
	python $(src)/downloader/downloader.py --output "$(downloads)"
	python $(src)/downloader/downloader.py --output "$(downloads)"


