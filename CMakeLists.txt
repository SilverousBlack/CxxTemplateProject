cmake_minimum_required(VERSION 3.10)

set(
    WORKSPACE_NAME
    CxxTemplateProject # TODO: Workspace Name (i.e. CxxTemplateProject)
)

string(TOUPPER "${WORKSPACE_NAME}" WORKSPACE)

set(
    ${WORKSPACE_NAME}_VERSION_MAJOR
    0 # TODO: Version major
)

set(
    ${WORKSPACE_NAME}_VERSION_MINOR
    0 # TODO: Version minor
)

set(
    ${WORKSPACE_NAME}_VERSION_PATCH
    0 # TODO: Version patch
)

# auto-generated semantic version
set(
    ${WORKSPACE_NAME}_VERSION
    ${${WORKSPACE_NAME}_VERSION_MAJOR}.${${WORKSPACE_NAME}_VERSION_MINOR}.${${WORKSPACE_NAME}_VERSION_PATCH}
)

project(${WORKSPACE_NAME} VERSION ${${WORKSPACE_NAME}_VERSION})

# always use at least C++17
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/out/${CMAKE_SYSTEM_PROCESSOR})

configure_file(${CMAKE_SOURCE_DIR}/src/info/info_template.hxx.in ${CMAKE_SOURCE_DIR}/src/info/info.hxx.in)
configure_file(${CMAKE_SOURCE_DIR}/src/info/info.hxx.in ${CMAKE_SOURCE_DIR}/src/info/info.hxx)

include_directories(src)
include_directories(src/info)

set(
    EXECUTABLES
    sample_executable # TODO: list executables
)

set(
    LIBRARIES
    sample_library # TODO: list libraries
)

set(
    SHARED_LIBRARIES
    sample_shared_library # TODO: list shared libraries
)

foreach(EXECUTABLE ${EXECUTABLES})
    add_subdirectory(src/${EXECUTABLE})
endforeach()

foreach(LIBRARY ${LIBRARIES})
    add_subdirectory(src/${LIBRARY})
endforeach()

foreach(SHARED_LIBRARY ${SHARED_LIBRARIES})
    add_subdirectory(src/${SHARED_LIBRARY})
endforeach()

add_custom_target(
    clean-all
    COMMAND ${CMAKE_COMMAND} --build ${CMAKE_BINARY_DIR} --target clean
)

add_custom_target(build-all)

foreach(config ${CMAKE_CONFIGURATION_TYPES})
    add_custom_command(
        TARGET build-all
        COMMAND ${CMAKE_COMMAND} --build ${CMAKE_BINARY_DIR} --config ${config}
        COMMENT "Building ${config} configuration"
    )
endforeach()
