include_directories(
  ${CMAKE_CURRENT_SOURCE_DIR}
  ${BZIP2_INCLUDE_DIR}
)

file(GLOB Sources code/*.cpp)

add_library(umcf STATIC ${Sources})
target_link_libraries(umcf
    ${BZIP2_LIBRARIES}
)

if(WIN32)
  SetSharedRuntime(umcf)
endif()

add_dependencies(umcf bzip2)

SET_PROPERTY(TARGET umcf PROPERTY FOLDER "Static")

if(WIN32)
  add_library(umcf_s STATIC ${Sources})

  target_link_libraries(umcf_s
    ${BZIP2_LIBRARIES_S}
  )

  SET_PROPERTY(TARGET umcf_s PROPERTY FOLDER "Static")
  add_dependencies(umcf_s bzip2_s)
  SetStaticRuntime(umcf_s)
endif()
