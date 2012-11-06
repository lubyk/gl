# --------------------------------------------------------------
#  gl_luagl, gl_luaglu
#  
#  expects:
#    MODULE_NAME defined in the CMakeLists for the module
#
#  provides:
#    gl/luagl.so
#    gl/luaglu.so
# --------------------------------------------------------------

find_package(OpenGL REQUIRED)

add_library(luagl MODULE LuaGL.c luagl_util.c)
set_target_properties(luagl
  PROPERTIES
  LINK_FLAGS ${PLAT_OBJ_FLAGS}
  PREFIX ""
  SUFFIX ".so"
)  
target_link_libraries(luagl ${OPENGL_LIBRARIES})

add_library(luaglu MODULE luaglu.c)
set_target_properties(luaglu
  PROPERTIES
  LINK_FLAGS ${PLAT_OBJ_FLAGS}
  PREFIX ""
  SUFFIX ".so"
)  
target_link_libraries(luaglu ${OPENGL_LIBRARIES})

add_dependencies(${MODULE_NAME} luagl luaglu)

# --------------------------------------------------------------
#  install                                     
# --------------------------------------------------------------
install(TARGETS luagl luaglu
  DESTINATION ${LUBYK_LIB}/lib/${MODULE_NAME}
)

