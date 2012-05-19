include_directories(${COMMON_INCLUDES})

add_library(${PROJECT_NAME_STR} STATIC "example.cxx")

INSTALL(TARGETS lib${PROJECT_NAME_STR} DESTINATION lib)
