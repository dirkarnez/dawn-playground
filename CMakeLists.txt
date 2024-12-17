# cmake_minimum_required(VERSION 3.18)

# add_executable(${PROJECT_NAME}
#     "src/main.c"
# )

# target_link_libraries(${PROJECT_NAME} portaudio_static)
# target_link_options(${PROJECT_NAME} PRIVATE "-static")




cmake_minimum_required(VERSION 3.18) # CMake version check

set(CMAKE_FIND_DEBUG_MODE TRUE)

project("dawn-playground")

set(CMAKE_CXX_STANDARD 20)           # Enable C++20 standard

find_package(Dawn 0.0.0 EXACT REQUIRED)
if(Dawn_FOUND)
    message(STATUS "YES")
else()
    message(STATUS "NO")
endif()

add_executable(${PROJECT_NAME} 
  "src/main.cpp"
)

target_link_libraries(${PROJECT_NAME} PRIVATE dawn::webgpu_dawn) # glfw webgpu_glfw)

# if(EMSCRIPTEN)
#   set_target_properties(${PROJECT_NAME} PROPERTIES SUFFIX ".html")
#   target_link_options(${PROJECT_NAME} PRIVATE "-sUSE_WEBGPU=1" "-sUSE_GLFW=3")
# else()
#   set(DAWN_FETCH_DEPENDENCIES ON)
#   add_subdirectory("dawn" EXCLUDE_FROM_ALL)
#   target_link_libraries(${PROJECT_NAME} PRIVATE dawn::webgpu_dawn glfw webgpu_glfw)
# endif()
