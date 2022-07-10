cmake_minimum_required(VERSION 3.0.2)
add_definitions("-D SOPHUS_USE_BASIC_LOGGING")
project(mvg)
set(CMAKE_CXX_STANDARD 17)
find_package(OpenCV COMPONENTS core highgui calib3d REQUIRED)
find_package(Ceres REQUIRED)
include_directories( ${CERES_INCLUDE_DIRS})


find_package (Eigen3 REQUIRED)
INCLUDE_DIRECTORIES ( "${EIGEN3_INCLUDE_DIR}" )
message("EIGEN3_INCLUDE_DIR" ${EIGEN3_INCLUDE_DIR})



add_subdirectory(3rd/glfw/)

include_directories(
  include
  3rd/Sophus
  3rd/glfw/include
  3rd/glm
)

find_package(OpenGL REQUIRED)


include_directories(
        ${CMAKE_CURRENT_SOURCE_DIR} ${OpenCV_INCLUDE_DIRS}
        ${OPENGL_INCLUDE_DIR} ${GLEW_INCLUDE_DIRS} ${GLFW3_INCLUDE_DIR} 
)
Message(STATUS, "GLFW3_INCLUDE_DIR ${GLFW3_INCLUDE_DIR}")
Message(STATUS, "GLEW_INCLUDE_DIRS ${GLEW_INCLUDE_DIRS}")
Message(STATUS, "OpenCV_INCLUDE_DIRS ${OpenCV_INCLUDE_DIRS}")



include_directories(GL 3rd 3rd/imgui 3rd/imgui/backends)

#"/usr/local/Cellar/glfw/3.3.7/include/",
#"/usr/local/Cellar/glm/0.9.9.8/include/",
#"/usr/local/Cellar/glew/2.2.0_1/include/"

add_library(GL_Codes
        # imgui
        3rd/imgui/imgui.cpp 3rd/imgui/imgui_demo.cpp 3rd/imgui/imgui.cpp
        3rd/imgui/imgui_draw.cpp 3rd/imgui/imgui_widgets.cpp 3rd/imgui/imgui_tables.cpp
        3rd/imgui/backends/imgui_impl_opengl3.cpp 3rd/imgui/backends/imgui_impl_glfw.cpp
        )


add_executable(imgui_demo main.cpp)
target_link_libraries(imgui_demo GL_Codes  glfw ${OPENGL_LIBRARIES} )