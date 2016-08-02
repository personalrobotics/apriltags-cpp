add_library(apriltags SHARED
  CameraUtil.cpp
  DebugImage.cpp
  Geometry.cpp 
  GrayModel.cpp
  MathUtil.cpp 
  Refine.cpp
  TagDetector.cpp 
  TagFamily.cpp
  TagFamilies.cpp
  UnionFindSimple.cpp
)

set(AT_LIBS apriltags)

target_link_libraries(apriltags ${OPENCV_LIBRARIES})

add_executable(camtest camtest.cpp)
target_link_libraries(camtest ${AT_LIBS} ${OPENCV_LIBRARIES})

add_executable(tagtest tagtest.cpp)
target_link_libraries(tagtest ${AT_LIBS} ${OPENCV_LIBRARIES})

add_executable(quadtest quadtest.cpp)
target_link_libraries(quadtest ${AT_LIBS} ${OPENCV_LIBRARIES})

if (GLUT_LIBRARY)

  add_executable(gltest gltest.cpp)
  target_link_libraries(gltest ${GLUT_LIBRARY} ${OPENGL_LIBRARY} ${AT_LIBS} ${OPENCV_LIBRARIES})

endif()

if (CAIRO_FOUND)

  add_executable(maketags maketags.cpp)
  target_link_libraries(maketags ${CAIRO_LIBRARIES} ${AT_LIBS} ${CAIRO_LIBS} ${OPENCV_LIBRARIES})

endif() 

install(TARGETS apriltags DESTINATION lib/)
