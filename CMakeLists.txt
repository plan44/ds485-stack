cmake_minimum_required(VERSION 3.15)
project(ds485-stack C)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# Enable CMAKE + Ninja
set(CMAKE_GENERATOR "Ninja")

# Enable folders in IDEs
set_property(GLOBAL PROPERTY USE_FOLDERS ON)

# collect headers in the way the dS sources require
# - Specify the destination for the unified "digitalSTROM" folder
set(DIGITALSTROM_INCLUDE_DIR ${CMAKE_BINARY_DIR}/include)

# - Create the "digitalSTROM" directory inside build
file(MAKE_DIRECTORY ${DIGITALSTROM_INCLUDE_DIR}/digitalSTROM)

# - Collect all header files from ds485-core/include, ds485-netlib/include, etc.
file(GLOB HEADERS_TO_COPY
    ${CMAKE_SOURCE_DIR}/ds485-core/include/*.h
    ${CMAKE_SOURCE_DIR}/ds485-netlib/include/*.h
    ${CMAKE_SOURCE_DIR}/ds485-client/include/*.h
    ${CMAKE_SOURCE_DIR}/libdsuid/src/*.h
)

# - Copy the headers to the new "digitalSTROM" folder
foreach(header ${HEADERS_TO_COPY})
    file(COPY ${header} DESTINATION ${DIGITALSTROM_INCLUDE_DIR}/digitalSTROM)
endforeach()


# Add subprojects
#add_subdirectory(libdsuid)
#add_subdirectory(ds485-core)
#add_subdirectory(ds485-netlib)
#add_subdirectory(ds485d)
add_subdirectory(ds485-client)
