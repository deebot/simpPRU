# Specify minimum cmake version required
cmake_minimum_required(VERSION 3.4)

# CMake project description and project specific settings
project(libprurpmsg 
        VERSION ${CMAKE_PROJECT_VERSION}
        DESCRIPTION "Static library for PRU RPMSG"
        HOMEPAGE_URL "https://github.com/VedantParanjape/simpPRU/")
SET(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${simppru_SOURCE_DIR}/lib")
set_property(GLOBAL PROPERTY USE_FOLDERS ON)

# Set pru-gcc as the compiler
set(CMAKE_SYSTEM_PROCESSOR pru)
set(CMAKE_C_COMPILER pru-gcc)
set(CMAKE_CXX_COMPILER pru-g++)

# Specify Build type
if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Release)
endif()
  
######## SOURCES ########
# Add source files and header files
file(GLOB PROJECT_HEADERS ${simppru_SOURCE_DIR}/include/pru/*.h ${simppru_SOURCE_DIR}/include/pru/am335x/*.h)
file(GLOB PROJECT_SOURCES *.c)
set(PROJECT_FILES
    ${PROJECT_HEADERS}
    ${PROJECT_SOURCES})

######## TARGETS ########
# Add static libraries targets
set(library_name_pru0 prurpmsg0-${CMAKE_PROJECT_VERSION})
set(library_name_pru1 prurpmsg1-${CMAKE_PROJECT_VERSION})

add_library(${library_name_pru0} STATIC ${PROJECT_FILES})
set_target_properties(${library_name_pru0} PROPERTIES COMPILE_FLAGS "-mmcu=am335x.pru0")

add_library(${library_name_pru1} STATIC ${PROJECT_FILES})
set_target_properties(${library_name_pru1} PROPERTIES COMPILE_FLAGS "-mmcu=am335x.pru1")

target_include_directories(${library_name_pru0} PUBLIC 
  $<BUILD_INTERFACE:${simppru_SOURCE_DIR}/include/pru>
  $<BUILD_INTERFACE:${simppru_SOURCE_DIR}/include/am335x/>)

target_include_directories(${library_name_pru1} PUBLIC 
  $<BUILD_INTERFACE:${simppru_SOURCE_DIR}/include/pru>
  $<BUILD_INTERFACE:${simppru_SOURCE_DIR}/include/am335x/>)

######## INSTALL ########
# Install static libraries and headers
set(include_destination "include/pru")
set(lib_destination "lib/")

# install(DIRECTORY ${simppru_SOURCE_DIR}/include/pru DESTINATION ${include_destination})
install(FILES ${PROJECT_HEADERS} DESTINATION ${include_destination})
install(TARGETS ${library_name_pru0} ${library_name_pru1} DESTINATION ${lib_destination})

# Create symlink to remove project version
install(CODE "execute_process(COMMAND ln -sf libprurpmsg0-${CMAKE_PROJECT_VERSION}.a libprurpmsg0.a WORKING_DIRECTORY ${CMAKE_ARCHIVE_OUTPUT_DIRECTORY})")
install(CODE "execute_process(COMMAND ln -sf libprurpmsg1-${CMAKE_PROJECT_VERSION}.a libprurpmsg1.a WORKING_DIRECTORY ${CMAKE_ARCHIVE_OUTPUT_DIRECTORY})")

# Install symlinks of static libraries
install(FILES ${CMAKE_ARCHIVE_OUTPUT_DIRECTORY}/libprurpmsg0.a DESTINATION ${lib_destination})
install(FILES ${CMAKE_ARCHIVE_OUTPUT_DIRECTORY}/libprurpmsg1.a DESTINATION ${lib_destination})
