set(
    PROJECT_NAME 
    sample_shared_library # TODO: Project mame
)

string(TOUPPER "${PROJECT_NAME}" PROJECT)

set(
    ${PROJECT_NAME}_VERSION_MAJOR
    0 # TODO: Version major
)

set(
    ${PROJECT_NAME}_VERSION_MINOR
    0 # TODO: Version minor
)

set(
    ${PROJECT_NAME}_VERSION_PATCH
    0 # TODO: Version patch
)

# auto-generated semantic version
set(
    ${PROJECT_NAME}_VERSION
    ${${PROJECT_NAME}_VERSION_MAJOR}.${${PROJECT_NAME}_VERSION_MINOR}.${${PROJECT_NAME}_VERSION_PATCH}
)

configure_file(${CMAKE_SOURCE_DIR}/src/${PROJECT_NAME}/info_template.hxx.in ${CMAKE_SOURCE_DIR}/src/${PROJECT_NAME}/info.hxx.in)
configure_file(${CMAKE_SOURCE_DIR}/src/${PROJECT_NAME}/info.hxx.in ${CMAKE_SOURCE_DIR}/src/${PROJECT_NAME}/info.hxx)

set(
    SOURCE_FILES
    ${PROJECT_NAME}.cxx #TODO: list source files
)

add_library(${PROJECT_NAME} SHARED ${SOURCE_FILES})

target_include_directories(${PROJECT_NAME} PUBLIC include)

set_target_properties(${PROJECT_NAME} PROPERTIES
    VERSION ${PROJECT_VERSION}
    SOVERSION ${PROJECT_VERSION_MAJOR}
)

install(TARGETS ${PROJECT_NAME}
    LIBRARY DESTINATION lib
)
install(DIRECTORY include/ DESTINATION include)
