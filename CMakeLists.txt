# cmake_minimum_required(VERSION 3.18)

# set(CMAKE_FIND_DEBUG_MODE TRUE)

# project("portaudio-playground")

# find_package(portaudio 19 EXACT REQUIRED) # PATHS "P:\\Downloads\\cpp-libraries\\portaudio\\build\\cmake\\portaudio")

# if(portaudio_FOUND)
#     message(STATUS "YES")
# else()
#     message(STATUS "NO")
# endif()

# add_executable(${PROJECT_NAME}
#     "src/main.c"
# )

# target_link_libraries(${PROJECT_NAME} portaudio_static)
# target_link_options(${PROJECT_NAME} PRIVATE "-static")





cmake_minimum_required(VERSION 3.13) # CMake version check
project(app)                         # Create project "app"
set(CMAKE_CXX_STANDARD 20)           # Enable C++20 standard

add_executable(app "main.cpp")

if(EMSCRIPTEN)
  set_target_properties(app PROPERTIES SUFFIX ".html")
  target_link_options(app PRIVATE "-sUSE_WEBGPU=1" "-sUSE_GLFW=3")
else()
  set(DAWN_FETCH_DEPENDENCIES ON)
  add_subdirectory("dawn" EXCLUDE_FROM_ALL)
  target_link_libraries(app PRIVATE dawn::webgpu_dawn glfw webgpu_glfw)
endif()
