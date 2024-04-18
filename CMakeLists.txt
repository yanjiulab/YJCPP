cmake_minimum_required(VERSION 3.8...3.26)
project(yjcpp)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/lib)

include_directories(include)

# file(GLOB SOURCES "src/app/*.cpp")

# file(GLOB SUB_SOURCES "src/folder1/*.cpp" "src/folder1/*.cpp")

# link_directories(third_party/fmt/lib)
# include_directories(${CMAKE_SOURCE_DIR}/3rd-party/fmt/include)
# include_directories(3rd-party/fmt/include)

# add_executable(yjcpp ${SOURCES})
# target_link_libraries(yjcpp ${CMAKE_SOURCE_DIR}/3rd-party/fmt/lib/libfmt.so)
# target_link_libraries(yjcpp 3rd-party/fmt/lib/libfmt.so)
# target_link_libraries(yjcpp PRIVATE 3rd-party/fmt/lib/libfmt.a)

file(GLOB_RECURSE SOURCES "src/*.cpp")
file(GLOB_RECURSE APP_SOURCES "src/app/*.cpp")
list(REMOVE_ITEM SOURCES ${APP_SOURCES})

foreach(APP_SOURCE ${APP_SOURCES})
    message("app: ${APP_SOURCE}")
    get_filename_component(APP_NAME ${APP_SOURCE} NAME_WE)
    add_executable(${APP_NAME} ${APP_SOURCE})
    target_sources(${APP_NAME} PRIVATE ${SOURCES})
endforeach()
